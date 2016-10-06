# NeoSolarized
Another solarized color theme for truecolor neovim / vim.
![Screenshot-dark](http://ww3.sinaimg.cn/large/5d4db8f9gw1f88o0e8r6mj21kw11hqcx.jpg)
![Screenshot-light](http://ww3.sinaimg.cn/large/5d4db8f9gw1f8bkj8fnghj21kw11n7et.jpg)
Fork from [vim-colors-solarized](https://github.com/altercation/vim-colors-solarized), Featrues:
- truecolor support for neovim/vim terminal, and works well in Gvim/MacVim certainly.
- [Neomake](https://github.com/neomake/neomake) signs support
- [gitgutter](https://github.com/airblade/vim-gitgutter) signs support
- [signature](https://github.com/kshenoy/vim-signature) signs support

## Requirements
- [terminal](https://gist.github.com/XVilka/8346728) which support truecolor
- neovim or Gvim/MacVim or vim ≥ 7.4.1799
- add the line below to your init.vim/.vimrc

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
- Plugin managers: [vim-plug](https://github.com/junegunn/vim-plu://github.com/junegunn/vim-plug):
    - add `Plug 'iCyMind/NeoSolarized'` to your init.vim or .vimrc file
    - run `:PluginInstall` after resource/relaunch

When installtation is done, config it as your colorscheme, put in your init.vim / .vimrc:

```vim
colorscheme NeoSolarized
```
## Options
Remove some options of origin solarized, rename options name to avoid config conflict. Make sure put those lines before "colorscheme NeoSolarized" in init.vim / .vimrc

```vim
" default value is "normal", Setting this option to "high" or "low" does use the 
" same Solarized palette but simply shifts some values up or down in order to 
" expand or compress the tonal range displayed.
let g:neosolarized_contrast = "normal"

" Special characters such as trailing whitespace, tabs, newlines, when displayed 
" using ":set list" can be set to one of three levels depending on your needs. 
" Default value is "normal". Provide "high" and "low" options.
let g:neosolarized_visibility = "normal"

" If you wish to enable/disable NeoSolarized from displaying bold, underlined or italicized 
" typefaces, simply assign 1 or 0 to the appropriate variable. Default values:  
let g:neosolarized_bold = 1
let g:neosolarized_underline = 1
let g:neosolarized_italic = 1
```

## More info
### Plugins which use in the screenshot

- [NERDTree](https://github.com/scrooloose/nerdtre://github.com/scrooloose/nerdtree)
- [vim-airline](https://github.com/vim-airline/vim-airline)
- [neomake](https://github.com/neomake/neomak://github.com/neomake/neomake)
- [vim-gitgutter](https://github.com/airblade/vim-gitgutter)
- [vim-signature](https://github.com/kshenoy/vim-signature)

### Truecolor test
You can run this scrip to test if your terminal has support. If the colors smoothly blend like:
![truecolor](http://ww3.sinaimg.cn/large/5d4db8f9gw1f8inp80my1j20h907daba.jpg)
Then you know that you have True Color support.
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
You may need same hack to make vim works well in tmux. Put this lines to your .vimrc:  
```vim
set t_8f=^[[38;2;%lu;%lu;%lum
set t_8b=^[[48;2;%lu;%lu;%lum
```
The '^[' represent the escape char. You should press <kbd>Ctrl-v</kbd> + <kbd>Esc</kbd> to input actual escape. If the ^[ is two characters (^ and [), it's wrong. If it is one character, it's okay. When you delete the character with backspace, you will find that ^[ is deleted at once. Please also check
:help c_CTRL-V (and :help i_CTRL-V).
check [issue](https://github.com/vim/vim/issues/993#issuecomment-241676971) and [issue](https://github.com/vim/vim/issues/981#issuecomment-242893385) for more information.


neovim works perfect without this config.  If you meet a color issue when using tmux. Make sure:  
- using lastest tmux (v2.2)
- your $TERM variable set to "xterm-256color"
- add the line below to your .tmux.conf file.

    ```tmux
    set-option -ga terminal-overrides ",xterm-256color:Tc"
    ```

see this [article](https://deductivelabs.com/en/2016/03/using-true-color-vim-tmux/) for more tmux detail.
