IceNvim grants you almost infinite ability to customize. This sounds like no big deal, but what is special about this is that IceNvim allows you to do so without messing the original repo.

Some neovim distros "allow" you to override the defaults by directly modifying the original config files. This messes the git repo and makes keeping track of upstream updates somewhat difficult. IceNvim uses a different approach by introducing a `custom` module in the config dir. The entire directory is not tracked by git and by placing any customization code inside this dir, you can modify the default behaviors of IceNvim while also being able to keep up with any update made upstream.

This page and the rest parts in this section will show to you how to utilize this great customization ability.

## How the `custom` Module Works

If you have taken a look at the directory structure of the IceNvim config, you can see that it looks something like this:

```txt
📂 nvim
|-- 📂 lua
    |-- 📂 core
    |-- 📂 custom
    |-- 📂 lsp
    |-- 📂 plugins
|-- 📂 screenshots
|-- 📄 .gitignore
|-- 📄 .stylua.toml
|-- 📄 LICENSE
|-- 📄 README.md
|-- 📄 init.lua
```

IceNvim first loads the config in `core` which includes basic functions that do not require a plugin. If you run neovim with the `--noplugin` flag, by default only the configuration in here is used.

The `lsp` and `plugins` modules are both responsible for functions that are only available when plugins are enabled. These two modules are loaded after `core`. However, when I say "loaded" here, I am not talking about the **loading of plugins**. Rather, what these modules do is storing the configuration spec (for details, you might check the documentation of [lazy.nvim](https://lazy.folke.io/spec)) in a global variable called `Ice`.

What comes last is the `custom` module. Here, you can make modifications to options that come with neovim (such as fields in `vim.o` and `vim.g`) as well as the `Ice` table. Since `custom` comes after `core`, `plugins` and `lsp`, any default settings made by IceNvim in these modules can be overridden.

After `custom` loaded, we have a final `Ice` table. Now, IceNvim will use this table to load plugins, set keymaps, etc.

!!! warning
    Again, I must stress the fact that **plugins are not yet available when `custom` files are loaded**. This means that, should you use functionalities that require a plugin in your `custom` files, it would not work and some hedious errors would be thrown causing IceNvim to cease to work. For example, this is bad:

    ```lua
    Ice.plugins.hop.opts.hint_position = require("hop.hint").HintPosition.END
    ```

    As said above, `hop` is currently not loaded and neovim cannot find a module named `hop.hint`. You have two options to avoid this. Option 1 is removing the module:


    ```lua
    Ice.plugins.hop.opts.hint_position = 3 -- equal to require("hop.hint").HintPosition.END
    ```

    Option 2 is to postpone the calling to the module. For example, you can use the `config` function to load the plugin:

    ```lua
    Ice.plugins.hop.config = function (_, opts)
        opts.hint_position = require("hop.hint").HintPosition.END
        require("hop").setup(opts)
    end
    ```

## Getting Started with the `custom` Module

You can place any number of files inside `custom`, but one `init.lua` file is essential. Do not worry, though. Even if it is missing, IceNvim will create it for you.

But there is more to that. We know that neovim looks for such folders as `queries`, `compiler`, `spell`, etc., in your `runtimepath`. Typically, if one wishes to override the default treesitter queries or ftplugins or other things already set up by neovim, they would need to create the corresponding directory under their config directory.

However, IceNvim users do not need to do that. IceNvim has added `custom` to `runtimepath` so you can just create these folders there. For example, where you should have `~/.config/nvim/queries/markdown/highlights.scm`, with IceNvim, it should be placed at `~/.config/nvim/queries/lua/custom/queries/markdown/highlights.scm`:

```txt
📂 nvim
|-- 📂 lua
    |-- 📂 core
    |-- 📂 custom
        |-- 📄 init.lua
        |-- 📂 queries
            |-- 📂 markdown
                |-- 📄 highlights.scm
    |-- 📂 lsp
    |-- 📂 plugins
```
