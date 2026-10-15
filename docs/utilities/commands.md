IceNvim has created a number of commands:

- `IceAbout`: opens a float window that displays the info about IceNvim
- `IceColorscheme`: selects a IceNvim-builtin colorscheme that also takes care of things like transparency; persists across sessions
- `IceHealth`: runs a health check on the prerequisites for IceNvim
- `IceProfile`: shows the plugins profile dashboard
- `IceRepeat`: makes a command repeatable when creating a keymap; for instance, `vim.keymap.set("n", "<leader>zz", ":IceRepeat :tabnew<CR>")` allows you to prefix a count before <kbd>&lt;leader&gt;zz</kbd> 
- `IceTokei`: counts the number of lines of codes in pwd and displays the output in a float window; needs the `tokei` executable installed
- `IceUpdate`: updates IceNvim itself and the plugins
- `IceView`: views the output of a command in a new buffer; for instance, `:IceView :lua print(123)` displays `123` in a new buffer; you can use this command without any argument to view the previous output generated with this command
- `IceYank`: yanks the output of a command into system clipboard
