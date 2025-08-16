You can configure some of the basic features of IceNvim which functions without plugins.

## Keymaps

You can customize keymaps via the `Ice.keymap` table. Note that these do not include plugin-related keymaps. Those can be modified via the `keys` table in a plugin config spec or, for some plugins, via the `opts` table.

Each item in the `Ice.keymap` table is a table that consists of the arguments passed to `vim.keymap.set`. That is, it contains: `mode` / `lhs` / `rhs` / (optional) `opts`. The name for each item is converted to the `desc` option for that keymap. For example, I have this in my custom config that opens a url in qutebrowser:

```lua
Ice.keymap.open_in_qutebrowser = {
    { "n", "v" },
    "<leader>uq",
    function()
        local mode = vim.api.nvim_get_mode().mode

        local target = ""
        if mode == "n" then
            target = vim.fn.expand "<cWORD>"
        else
            local start_pos = vim.fn.getpos "'<"
            local end_pos = vim.fn.getpos "'>"
            local selection = vim.fn.getregion(start_pos, end_pos)
            if #selection == 1 then
                target = selection[1]
            end
        end

        local url = string.match(target, "[%w]+://[%w-_%.%?%.:/%+=&]+")
        if url ~= nil then
            vim.system { "qutebrowser", url, "--target", "tab" }
        else
            vim.notify("Target is not a valid url", vim.log.levels.WARN)
        end
    end,
}
```

This would add an entry with the desc "open in qutebrowser" in which-key.

## FileType-Specific Configuration

Of course we can do this via neovim's ftplugin feature. No big deal. That, however, requires you to write vimscript, which I am strongly against under most scenarios. IceNvim provides a seperate interface instead: `Ice.ft["<filetype>"]`.

For example, you can do this:

```lua
Ice.ft.lua = function()
    vim.wo.colorcolumn = "120"
end
```

This has the down side, though, of overriding any filetype-specific configuration IceNvim has made. Another approach would be to use the `Ice.ft:set` method. For example:

```lua
Ice.ft:set("python", function()
    vim.cmd "compiler python"
    vim.keymap.set("n", "<F9>", ":silent make | copen<CR>", { buffer = 0 })
end)
```

## Automatic Directory Switching

IceNvim automatically switches the cwd to your project directory if possible. It works better than neovim's default `autochdir`. However, if you do not like this feature, you can disable it by doing this:

```lua
Ice.auto_chdir = false
```

By default, it is disabled for buffers with the filetype of `NvimTree` and `help` and with the buftype of `terminal` and `nofile`. You can override these options via the `Ice.chdir_exclude_filetype` and `Ice.chdir_exclude_buftype` tables.

IceNvim automatically switches dir by trying to detect for certain file / directory patterns: `.git` / `package.json` / `.prettierrc` / `tsconfig.json` / `pubspec.yaml` / `.gitignore` / `stylua.toml` / `README.md`. You can override this via the `Ice.chdir_root_pattern` table.


!!! warning
    `Ice.chdir_exclude_filetype`, `Ice.chdir_exclude_buftype` and `Ice.chdir_root_pattern` do not exist by default! You can only set their value but cannot modify their values initially.
