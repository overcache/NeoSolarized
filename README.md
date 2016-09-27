# NeoSolarized
Another solarized color theme for truecolor vim.
![Screenshot](http://ww3.sinaimg.cn/large/5d4db8f9gw1f88o0e8r6mj21kw11hqcx.jpg)
Fork from [vim-colors-solarized](), Featrues:
- truecolor support for neovim/vim terminal
- [Neomake](https://github.com/neomake/neomake) signs support
- [gitgutter](https://github.com/airblade/vim-gitgutter) signs support
- [signature](https://github.com/kshenoy/vim-signature) signs support

### Requirements
- [terminal](https://gist.github.com/XVilka/8346728) which support truecolor
- neovim or Gvim/MacVim or vim ≥ 7.4.1799
- `set termguicolors` in your init.vim/.vimrc

### Installation
- Manual install  
Move NeoSolarized.vim to your vim RunTimePath directory:

    ```bash
    cd NeoSolarized/colors
    mv NeoSolarized.vim ~/.config/nvim/colors/
    ```
    or
    ```bash
    cd NeoSolarized/colors
    mv NeoSolarized.vim ~/.vim/colors/
    ```
- Plugin managers: [vim-plug](https://github.com/junegunn/vim-plu://github.com/junegunn/vim-plug):
    - add `Plug 'iCyMind/NeoSolarized'` to your init.vim or .vimrc file
    - run `:PluginInstall` after resource/relaunch

### Info
##### truecolor test
You can run this scrip to test if your terminal has support. If the colors smoothly blend, then you know that you have True Color support.
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
#### tmux
Currently, vim can not work well in tmux. But neovim works perfect.  
If you meet a color issue when using tmux. Make sure:
- using lastest tmux (v2.2)
- your $TERM variable set to "xterm-256color"
- add `set-option -ga terminal-overrides ",xterm-256color:Tc"` to your .tmux.conf file.

see this [article](https://deductivelabs.com/en/2016/03/using-true-color-vim-tmux/) for more tmux detail.
