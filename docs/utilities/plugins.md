IceNvim uses a variety of plugins to guarantee a smooth editing experience.

## Plugin Manager

IceNvim uses [lazy.nvim](https://github.com/folke/lazy.nvim) as plugin manager. It is modern, powerful, and extremely easy to use.

Beware that the way IceNvim uses Lazy is slightly different from the official approach, which we shall see later in the [customization](./Customization) section. The majority, though, remains unchanged, which is why a little knowledge on how to use this plugin manager would be helpful should you wish to further customize Lazy in IceNvim.

## Colorscheme and UI

IceNvim comes with the following colorschemes (and their variants; for details, check out the corresponding repositories):

- [github theme](https://github.com/projekt0n/github-nvim-theme)
- [gruvbox theme](https://github.com/ellisonleao/gruvbox.nvim)
- [kanagawa theme](https://github.com/rebelot/kanagawa.nvim)
- [miasma theme](https://github.com/xero/miasma.nvim)
- [nightfox theme](https://github.com/EdenEast/nightfox.nvim)
- [tokyonight theme](https://github.com/folke/tokyonight.nvim) (this is the first theme I used for neovim btw)

As well as some other UI-related plugins, including:

- [bufferline](https://github.com/akinsho/bufferline.nvim): displays opened buffers at the top
- [dashboard](https://github.com/nvimdev/dashboard-nvim): provides a welcome screen when opening neovim
- [fidget](https://github.com/j-hui/fidget.nvim): displays pretty notifications
- [indent-blankline](https://github.com/lukas-reineke/indent-blankline.nvim): adds indentation lines
- [lualine](https://github.com/nvim-lualine/lualine.nvim): displays various info about neovim at the bottom
- [nvim-scrollview](https://github.com/dstein64/nvim-scrollview): displays a scroll bar
- [nvim-transparent](https://github.com/xiyaowong/nvim-transparent): makes most background colors of neovim transparent
- [rainbow-delimiters](https://github.com/hiphish/rainbow-delimiters.nvim): use different colors for paired parentheses
- [winsep](https://github.com/nvim-zh/colorful-winsep.nvim): indicates the window currently being focused

## Improving Editting Experience

IceNvim uses various plugins for better editting experience:

- [grug-far](https://github.com/MagicDuck/grug-far.nvim): better find / replace
- [hop](https://github.com/smoka7/hop.nvim): hops to the desired position with a few key presses
- [nvim-autopairs](https://github.com/windwp/nvim-autopairs): automatically closes pairs such as parentheses
- [surround](https://github.com/kylechui/nvim-surround): surround text with parentheses or tags easily
- [ufo](https://github.com/kevinhwang91/nvim-ufo): better folding
- [undotree](https://github.com/mbbill/undotree): visualize your edits so that you can undo them with much ease

## Useful Tools for Development

Apart from the necessary plugins for basic editting, IceNvim also includes several useful plugins that boost development efficiency:

- [avante](https://github.com/yetone/avante.nvim): use neovim like using using Cursor AI IDE; **disabled by default**
- [colorizer](https://github.com/NvChad/nvim-colorizer.lua): colorize rgb / hex / ... colors
- [gitsigns](https://github.com/lewis6991/gitsigns.nvim): git integration for buffers
- [markdown-preview](https://github.com/iamcco/markdown-preview.nvim): live preview for markdown files
- [neogit](https://github.com/NeogitOrg/neogit): an extremely powerful and handy git interface
- [nvim-tree](https://github.com/nvim-tree/nvim-tree.lua): displays file tree
- [nvim-treesitter](https://github.com/nvim-treesitter/nvim-treesitter): build a syntax tree and enable better highlighting, and much much more
- [telescope](https://github.com/nvim-telescope/telescope.nvim): find, filter, preview, pick... you name it
- [todo-comments](https://github.com/folke/todo-comments.nvim): highlight todo / warn / fix / perf / ... comments
- [trouble](https://github.com/folke/trouble.nvim): a pretty list for showing diagnostics, references, etc.

Auto completions, diagnostics, formatting, etc., are managed by these extra plugins:

- [blink-cmp](https://github.com/saghen/blink.cmp): incredibly fast completion
- [mason](https://github.com/mason-org/mason.nvim): manage lsp / formatter sources
- [null-ls](https://github.com/nvimtools/none-ls.nvim): code formatter; IceNvim actually uses none-ls, a fork of the original null-ls project
- [lspsaga](https://github.com/nvimdev/lspsaga.nvim): collection of useful lsp utilities like hover docs and displaying diagnostics

Some languages also require extra plugins (**disabled by default**):

- [flutter-tools.nvim](https://github.com/akinsho/flutter-tools.nvim): flutter development
- [rustaceanvim](https://github.com/mrcjkb/rustaceanvim): rust development
- [typst-preview.nvim](https://github.com/chomosuke/typst-preview.nvim): writing with typst
