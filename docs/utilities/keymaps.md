IceNvim has set up a lot of reasonable and easy-to-remember keymaps already. Almost all of them can be checked out via the awesome `which-key.nvim` plugin either when you are typing them or by explicitly calling the `WhichKey` command.

This page lists only those keymaps that IceNvim has added. Some of the default keymaps that come with plugins are not included.

## Core Keymaps

These keymaps do not rely on external plugins. The details can be viewed in `lua/core/keymap.lua`.

| key | description | modes |
| :-: | :---------: | :---: |
| <kbd>gcO</kbd> | add comment above current line | normal |
| <kbd>gco</kbd> | add comment below current line | normal |
| <kbd>gcA</kbd> | add comment after current line | normal |
| <kbd>J</kbd> | if in normal mode, join `v_count` + 1 lines | normal / visual |
| <kbd>\\</kbd> | black hole register | normal / visual |
| <kbd>&lt;A-b&gt;</kbd> | open current html / markdown / typst file | normal |
| <kbd>&lt;A-o&gt;</kbd> | insert line below current line and remain in normal mode | normal |
| <kbd>&lt;A-O&gt;</kbd> | insert line above current line and remain in normal mode | normal |
| <kbd>&lt;C-g&gt;</kbd> | clear command line | normal / insert / visual / terminal |
| <kbd>&lt;C-s&gt;</kbd> | save file | normal / insert / visual |
| <kbd>&lt;C-t&gt;</kbd> | open terminal | normal |
| <kbd>&lt;C-z&gt;</kbd> | undo | normal / insert / visual / terminal / command |

## Command Mode Keymaps

These are keymaps that are aimed at enhancing editting experience in the command line. You might notice some resemblance to emacs.

| key | description |
| :-: | :---------: |
| <kbd>&lt;C-f&gt;</kbd> | move forward |
| <kbd>&lt;C-b&gt;</kbd> | move backward |
| <kbd>&lt;C-a&gt;</kbd> | start of the line |
| <kbd>&lt;C-e&gt;</kbd> | end of the line |
| <kbd>&lt;A-f&gt;</kbd> | move forward one word |
| <kbd>&lt;A-b&gt;</kbd> | move backward one word |

## Plugin-Related Keymaps

These keymaps are only available when the corresponding plugins are loaded. If you start neovim with the `--noplugin` flag, they would not work. You can check them out in `lua/plugins/keymap.lua` and `lua/plugins/config.lua`.

These keymaps are mostly prefixed with the leader key (<kbd>&lt;SPC&gt;</kbd> ) and an additional key that gives you a glimpse of what the keymap might do. They include:

| prefix | group |
| :----: | :---: |
| <kbd>&lt;leader&gt;a</kbd> | avante |
| <kbd>&lt;leader&gt;b</kbd> | bufferline |
| <kbd>&lt;leader&gt;g</kbd> | git |
| <kbd>&lt;leader&gt;h</kbd> | hop |
| <kbd>&lt;leader&gt;l</kbd> | lsp |
| <kbd>&lt;leader&gt;t</kbd> | telescope |
| <kbd>&lt;leader&gt;u</kbd> | utils |

The full list of these keymaps include:

### Avante

| key | description | modes |
| :-: | :---------: | :---: |
| <kbd>&lt;leader&gt;awc</kbd> | focus selected code | normal |
| <kbd>&lt;leader&gt;awi</kbd> | focus input | normal |
| <kbd>&lt;leader&gt;awa</kbd> | focus result | normal |
| <kbd>&lt;leader&gt;aws</kbd> | focus selected files | normal |
| <kbd>&lt;leader&gt;awt</kbd> | focus todo | normal |

### Bufferline

This part relies on the bufferline.nvim plugin.

| key | description | modes |
| :-: | :---------: | :---: |
| <kbd>&lt;leader&gt;bc</kbd> | bufferline pick close | normal |
| <kbd>&lt;leader&gt;bd</kbd> | bufferline close current buffer | normal |
| <kbd>&lt;leader&gt;bh</kbd> | bufferline previous buffer | normal |
| <kbd>&lt;leader&gt;bl</kbd> | bufferline next buffer | normal |
| <kbd>&lt;leader&gt;bo</kbd> | bufferline close other buffers | normal |
| <kbd>&lt;leader&gt;bp</kbd> | bufferline pick buffer | normal |
| <kbd>&lt;leader&gt;bm</kbd> | bufferline move buffer rightwards | normal |
| <kbd>&lt;leader&gt;bM</kbd> | bufferline move buffer leftwards | normal |

### Git

This part relies on the gitsigns.nvim and neogit plugins.

| key | description | modes |
| :-: | :---------: | :---: |
| <kbd>&lt;leader&gt;gB</kbd> | stage buffer | normal |
| <kbd>&lt;leader&gt;gb</kbd> | git blame | normal |
| <kbd>&lt;leader&gt;gl</kbd> | git blame line | normal |
| <kbd>&lt;leader&gt;gn</kbd> | go to next hunk | normal |
| <kbd>&lt;leader&gt;gP</kbd> | preview hunk | normal |
| <kbd>&lt;leader&gt;gp</kbd> | go to previous hunk | normal |
| <kbd>&lt;leader&gt;gr</kbd> | restore hunk | normal |
| <kbd>&lt;leader&gt;gs</kbd> | stage hunk | normal |
| <kbd>&lt;leader&gt;gt</kbd> | open neogit | normal |
| <kbd>&lt;leader&gt;gu</kbd> | undo stage | normal |

### Hop

This part relies on the hop.nvim plugin.

| key | description | modes |
| :-: | :---------: | :---: |
| <kbd>&lt;leader&gt;hp</kbd> | hop word | normal |

### Lsp

The keymaps would only work if the corresponding lsp / formatter / ... is set up properly.

| key | description | modes |
| :-: | :---------: | :---: |
| <kbd>&lt;leader&gt;lc</kbd> | code action | normal |
| <kbd>&lt;leader&gt;ld</kbd> | go to definition | normal |
| <kbd>&lt;leader&gt;lf</kbd> | format code | normal |
| <kbd>&lt;leader&gt;lh</kbd> | view hover doc | normal |
| <kbd>&lt;leader&gt;li</kbd> | go to implementation | normal |
| <kbd>&lt;leader&gt;ln</kbd> | go to next diagnostic | normal |
| <kbd>&lt;leader&gt;lP</kbd> | show line diagnostic | normal |
| <kbd>&lt;leader&gt;lp</kbd> | go to previous diagnostic | normal |
| <kbd>&lt;leader&gt;lR</kbd> | show references | normal |
| <kbd>&lt;leader&gt;lr</kbd> | rename | normal |
| <kbd>&lt;leader&gt;lt</kbd> | toggle trouble.nvim | normal |
| <kbd>&lt;leader&gt;ly</kbd> | yank line diagnostic | normal |


### Telescope

This part relies on the telescope.nvim plugin.

| key | description | modes |
| :-: | :---------: | :---: |
| <kbd>&lt;leader&gt;t&lt;C-f&gt;</kbd> | find in pwd | normal |
| <kbd>&lt;leader&gt;tf</kbd> | find file | normal |

### Utils

| key | description | modes |
| :-: | :---------: | :---: |
| <kbd>&lt;leader&gt;uc</kbd> | select config file | normal |
| <kbd>&lt;leader&gt;uf</kbd> | toggle nvim-tree | normal |
| <kbd>&lt;leader&gt;ug</kbd> | use grug-far to find and replace | normal |
| <kbd>&lt;leader&gt;ul</kbd> | open lazy panel | normal |
| <kbd>&lt;leader&gt;ut</kbd> | find todo items | normal |
| <kbd>&lt;leader&gt;uu</kbd> | toggle undo tree | normal |

### Misc

| key | description | modes |
| :-: | :---------: | :---: |
| <kbd>&lt;C-k&gt;&lt;C-t&gt;</kbd> | open colorscheme picker | normal |
