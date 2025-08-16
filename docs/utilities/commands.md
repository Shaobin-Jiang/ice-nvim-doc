IceNvim has created a number of commands:

- `IceAbout`: opens a float window that displays the info about IceNvim
- `IceCheckIcons`: opens a float window that displays a number of nerd icons; you can use this to check whether you have correctly set up your nerd font
- `IceCheckPlugins`: opens a float window that displays plugins that have not been updated for more than 30 days
- `IceUpdate`: updates IceNvim itself (**not updating the plugins**)
- `IceHealth`: run a health check on the prerequisites for IceNvim
- `IceRepeat`: make a command repeatable when creating a keymap; for instance, `vim.keymap.set("n", "<leader>zz", ":IceRepeat :BufferLineMovePrev<CR>")` allows you to prefix a count before <kbd>&lt;leader&gt;zz</kbd> 
- `IceView`: views the output of a command in a new buffer; for instance, `:IceView :lua print(123)` displays `123` in a new buffer; you can use this command without any argument to view the previous output generated with this command
