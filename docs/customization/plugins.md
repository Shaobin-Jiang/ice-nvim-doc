You can customize the plugins via the `Ice.plugins` table.

## Customizing a Plugin

Each plugin installed corresponds to a key-value pair in `Ice.plugins`. For example, if you want to customize `hop.nvim`, just make modifications to `Ice.plugins.hop`. The names used in `Ice.plugins` can be found in the [utilities/plugins](../../utilities/plugins) section, but with auto-completion enabled default, you can just navigate through the completion menu after typing `Ice.plugins.` to find the field name of a certain plugin.

Each value in these pairs is a lazy.nvim-compatible plugin spec. Pretty much everything is the same as when you are using lazy, but instead of returning it, we are storing it in `Ice.plugins`.

You can also remove a plugin by setting it to `nil` or add a plugin that is not present in IceNvim.

For example:

```lua
local view = Ice.plugins["nvim-tree"].opts.view
view.number = true
view.relativenumber = true

Ice.plugins.bufferline = nil -- disables bufferline

-- Field name does not matter when adding a new plugin
Ice.plugins.aaa = {
    "folke/zen-mode.nvim",
}
```

!!! warning

    Most of the time, IceNvim only uses configuration included by the original plugin. The only exception is nvim-treesitter.

    In a recent update, nvim-treesitter removed the `ensure_installed` field. IceNvim, however, persists on using this field to automatically install parser. It is also highly unrecommended to use other ways to install parser, e.g., via the `TSInstall` command, because IceNvim has made special tweaks to only enable treesitter support for buffers whose filetype has a corresponding parser.

    For example, you can install the parser for swift like this:

    ```lua
    table.insert(Ice.plugins["nvim-treesitter"].opts.ensure_installed, "swift")
    ```

## Lazy Loading a Plugin

If you are familiar with lazy.nvim, you should know about the `VeryLazy` event and how it is used to lazy load a plugin. IceNvim is built with performance in mind and also further provides some custom events to help boost loading.

### `IceLoad` Event

`IceLoad` is triggered after the colorscheme is loaded and well after the `VeryLazy` event. However, if the current buffer is an unnamed buffer or it is the dashboard, the triggering of `IceLoad` will be postponed to the next time we enter a buffer. If the next buffer is still a dashboard / unnamed buffer, the triggering is further postponed.

Note that `IceLoad` is a custom event, so when using it in the lazy.nvim `event` field, it should be prefixed with a `User `. For example:

```lua
Ice.plugins.bufferline.event = "User IceLoad"
```

### `IceAfter` Event

`IceAfter` is intended for scenarios where the loading order of two plugins are critical.

For example, in IceNvim, rainbow-delimiter loads with nvim-treesitter as it requires a tree-sitter parser to work. Another plugin, indent-blankline, requires rainbow-delimiter to load first to enable colorful indentation markers. Therefore, IceNvim needs to ensure that indent-blankline loads after nvim-treesitter.

With `IceAfter`, this would be easy. You can just fire a `User IceAfter nvim-treesitter` event after nvim-treesitter is loaded and set the `event` for indent-blankline to `User IceAfter nvim-treesitter`:

```lua
Ice.plugins["nvim-treesitter"] = {
    -- ...
    config = function (_, opts) {
      -- Setting up nvim-treesitter
      vim.api.nvim_exec_autocmds("User", { pattern = "IceAfter nvim-treesitter" })
    },
}

Ice.plugins["indent-blankline"].event = "User IceAfter nvim-treesitter"
```

IceNvim also fires the `IceAfter colorscheme` after the colorscheme is set, so you can also use `User IceAfter colorscheme` to load a plugin after the colorscheme is ready (differing from `IceLoad` in that this does not care about whether you are viewing the dashboard).

## Language-Specific Configuration

As mentioned above, you can disable any plugin by setting the corresponding field to `nil`. However, it would be better if you use a different approach with a few of them. These plugins are exclusively responsible for development in a certain language, and IceNvim has a different mechanism for managing them.

IceNvim supports development for these languages: Bash / C / C++ / C# / Flutter / Go / CSS / HTML / JavaScript / Typescript / JSON / Lua / Python / Typst / Rust. Among these, some are managed by plugins while others are supported via LSPs and formatters. To provide a universal interface to managing them, IceNvim introduces the `Ice.lsp` table. Each language corresponds to a field in this table:

- `emmet-ls`
- `pyright`: python
- `tinymist`: typst
- `bash-language-server`
- `rust`
- `gopls`: go
- `clangd`: C / C++
- `css-lsp`
- `typescript-language-server`
- `html-lsp`
- `json-lsp`
- `lua-language-server`
- `omnisharp`: C#
- `flutter`

By default, only `lua-language-server` is enabled. To enable support for a language, just set `enabled = true`:

```lua
Ice.lsp.flutter.enabled = true
```

And if you want to enable support for all these languages above, just do this:

```lua
for _, lsp in pairs(vim.tbl_keys(Ice.lsp)) do
    Ice.lsp[lsp].enabled = true
end
```

Each language has a config table. If the table has `managed_by_plugin = true`, that language is managed by a plugin, and configuration for that language go to the corresponding `Ice.plugins` table:

- flutter: flutter-tools
- rust: rustaceanvim

Others are managed by LSPs and formatters. In this case, each table can optionally have a `formatter` and a `setup` field, where `formatter` is the name you can find by running the command `Mason` and `setup` is the configuration available to the language server. You can find the latter [here](https://github.com/neovim/nvim-lspconfig/blob/master/doc/configs.md) (Most of the time you really do not need that, though).

You might notice that some of these languages have strange names. Why not just name it `bash` instead of `bash-language-server`? That is because these are names from `Mason` LSPs. Should you wish to add support for other languages without using a plugin, you should use the name of the LSP from `Mason` as its field name. For example, haskell's LSP is named `haskell-language-server` if you look it up in Mason. To add support for haskell, do this:

```lua
Ice.lsp["haskell-language-server"] = {} -- `formatter` and `setup` can be omitted
```

## Snippets

IceNvim supports VsCode-styled snippets. For example, if you want to create snippets that take effect in markdown files, just create `custom/snippets/markdown.json` and write whatever code you like in there.

For more information on how to write such snippets, refer to the [official documentation](https://code.visualstudio.com/docs/editing/userdefinedsnippets).

## Colorschemes

Conventionally, we use the `colorscheme` command to set colorschemes. In IceNvim, as you ought to remember from the [utilities/keymaps](../../utilities/keymaps) section, we use the <kbd>&lt;C-k&gt;&lt;C-t&gt;</kbd> keymap to open a colorscheme picker. This is quite handy in that it persists across sessions.

For a colorscheme to appear in this picker, you need not only to install the colorscheme plugin itself, but also register it in the `Ice.colorschemes` (notice the `s` at the end) table. Each table must have a `name` value which can be used with `:colorscheme name` and a `background` field that is either `"dark"` or `"light"`. Optionally you can have a `setup` field that can be passed to the plugin's setup function. For example:

```lua
-- gruvbox-light will appear in the colorscheme picker
Ice.colorschemes["gruvbox-light"] = {
    name = "gruvbox",
    setup = {
        italic = {
            strings = true,
            operators = false,
            comments = true,
        },
        contrast = "hard",
    },
    background = "light",
},
```

You can also set the colorscheme via `Ice.colorscheme`. It is a string value that is one of the available colorschemes from `Ice.colorschemes`.
