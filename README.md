# NeoSolarized
Another solarized color theme for truecolor neovim / vim.
![Screenshot-dark](http://ww3.sinaimg.cn/large/5d4db8f9gw1f88o0e8r6mj21kw11hqcx.jpg)
![Screenshot-light](http://ww3.sinaimg.cn/large/5d4db8f9gw1f8bkj8fnghj21kw11n7et.jpg)
Fork from [vim-colors-solarized](https://github.com/altercation/vim-colors-solarized), Features:
- truecolor support for neovim/vim terminal, and works well in Gvim/MacVim.
- define color for neovim's embed terminal.
- define color for [Neomake](https://github.com/neomake/neomake), [GitGutter](https://github.com/airblade/vim-gitgutter), [ALE](https://github.com/w0rp/ale)

## Requirements
- A [terminal](https://gist.github.com/XVilka/8346728) which supports truecolor
- neovim or Gvim/MacVim or vim ≥ 7.4.1799
- The following line in your `init.vim` or `.vimrc` file:

    ```vim
    set termguicolors
    ```

## Installation
- Manual install
Move NeoSolarized.vim to your vim RunTimePath directory:

    ```bash
    cd NeoSolarized/colors
    mv NeoSolarized.vim ~/.config/nvim/colors/
    ```
    or for vim
    ```bash
    cd NeoSolarized/colors
    mv NeoSolarized.vim ~/.vim/colors/
    ```
- Plugin managers: [vim-plug](https://github.com/junegunn/vim-plug):
    - Add `Plug 'overcache/NeoSolarized'` to your `init.vim` or `.vimrc` file.
    - Run `:PlugInstall` after resourcing/relaunching.

After the installation, configure it as your colorscheme by putting the following line into your `init.vim` or `.vimrc` file:
```vim
colorscheme NeoSolarized
```
## Options
Some options of the original solarized theme were removed or renamed to avoid config conflicts.
Make sure to put configuration before the line `colorscheme NeoSolarized` in `init.vim` or `.vimrc`.

```vim
" Default value is "normal", Setting this option to "high" or "low" does use the
" same Solarized palette but simply shifts some values up or down in order to
" expand or compress the tonal range displayed.
let g:neosolarized_contrast = "normal"

" Special characters such as trailing whitespace, tabs, newlines, when displayed
" using ":set list" can be set to one of three levels depending on your needs.
" Default value is "normal". Provide "high" and "low" options.
let g:neosolarized_visibility = "normal"

" I make vertSplitBar a transparent background color. If you like the origin
" solarized vertSplitBar style more, set this value to 0.
let g:neosolarized_vertSplitBgTrans = 1

" If you wish to enable/disable NeoSolarized from displaying bold, underlined
" or italicized" typefaces, simply assign 1 or 0 to the appropriate variable.
" Default values:
let g:neosolarized_bold = 1
let g:neosolarized_underline = 1
let g:neosolarized_italic = 0

" Used to enable/disable "bold as bright" in Neovim terminal. If colors of bold
" text output by commands like `ls` aren't what you expect, you might want to
" try disabling this option. Default value:
let g:neosolarized_termBoldAsBright = 1
```


To enable the dark version of the theme add the line
```vim
set background=dark
```
For more information check out the documentation in `NeoSolarized.vim`.


## More info
### Plugins used in the screenshot

- [NERDTree](https://github.com/scrooloose/nerdtree)
- [vim-airline](https://github.com/vim-airline/vim-airline)
- [neomake](https://github.com/neomake/neomake)
- [vim-gitgutter](https://github.com/airblade/vim-gitgutter) (make sure you have: `let g:gitgutter_override_sign_column_highlight = 0` in your init.vim/.vimrc)
- [vim-signature](https://github.com/kshenoy/vim-signature)

### Truecolor test
You can run this script to test if your terminal is supported. If the colors blend smoothly like: ![colortest](http://ww3.sinaimg.cn/large/5d4db8f9gw1f8into8gvgj20hf00o0sv.jpg), then you know that you have True Color support.
```bash
awk 'BEGIN{
    s="/\\/\\/\\/\\/\\"; s=s s s s s s s s;
    for (colnum = 0; colnum<77; colnum++) {
        r = 255-(colnum*255/76);
        g = (colnum*510/76);
        b = (colnum*255/76);
        if (g>255) g = 510-g;
        printf "\033[48;2;%d;%d;%dm", r,g,b;
        printf "\033[38;2;%d;%d;%dm", 255-r,255-g,255-b;
        printf "%s\033[0m", substr(s,colnum+1,1);
    }
    printf "\n";
}'
```
### Tmux
You may need the same hack to make vim work well in tmux. Put these lines into your .vimrc:
```vim
set t_8f=^[[38;2;%lu;%lu;%lum
set t_8b=^[[48;2;%lu;%lu;%lum
```
The '^[' represent the escape char. You should press <kbd>Ctrl-v</kbd> + <kbd>Esc</kbd> to input actual escape. If the ^[ is two characters (^ and [), it's wrong. If it is one character, it's okay. When you delete the character with backspace, you will find that ^[ is deleted at once. Please also check
:help c_CTRL-V (and :help i_CTRL-V).
check [issue](https://github.com/vim/vim/issues/993#issuecomment-241676971) and [issue](https://github.com/vim/vim/issues/981#issuecomment-242893385) for more information.


neovim works perfect without this config.  If you encounter a color issue using tmux, make sure that:
- you are using the latest version of tmux (v2.2)
- your $TERM variable is set to "xterm-256color"
- add the line below to your .tmux.conf file:

    ```tmux
    set-option -ga terminal-overrides ",xterm-256color:Tc"
    ```

See this [article](https://deductivelabs.com/blog/tech/using-true-color-vim-tmux/) for more details on tmux.
