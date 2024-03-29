# 打造理想 Vim 编辑器
{2015-12-23}
尝试过很多种编辑器，Emacs，Notepad++，Sublime Text，Komodo Edit，EditPlus等。都因种种原因始终难以顺手。最终还是走上了 Vim 这条道路。这里介绍一下如何把 Vim 打造成理想的编辑器。  
当然，这里只介绍 Vim 相关的信息，不涉及编辑器之战。

## Vim 操作

关于 Vim 的操作有能找到很多优秀的资料，这里就不追述了。比较推荐 Vim 自带的教程 `Vim tutor`。大约 30 钟左右的联系即可学会 Vim 的基本操作。满足日常工作使用。
 
## 认识 Vim

Vim 是一个学习曲线陡峭的编辑器，上手难度大。Vim 的强大在于普通模式下的命令。要想驾驭 Vim 就要熟练掌握哪些命令。  
同样 Vim 还是可高度定制化的编辑器，可以根据自己的习惯配置它，或者通过插件来扩展 Vim 的功能。
Vim 同样支持终端和 GUI 模式下使用。在 GUI 模式的 Vim 一般都叫 GVim   
*Unix 系统一般默认都有 Vim 如果需要安装 GUI 版本的，可以在这里下载: [Windows GVim](http://www.vim.org/download.php#pc), [MacVim](https://github.com/b4winckler/macvim/releases)
Linux 用户我相信都有自己解决这个问题的能力。
### 配置文件
在 *Unix 环境下，`/etc/vim/vimrc` 是全局配置文件，修改这个文件会对所有用户生效。(会因不同的版本目录有所不同)  
在 `~/.vimrc` 目录下时针对当前用户的生效的配置。如果想仅对 GUI 版本生效，命名 .gvimrc 这样，这个文件只会在 GUI 版本中生效。 后面会附上 我的 vimrc 配置

### 目录
一般安装插件，主题等的时候，不需要在安装目录进行安装，我们可以在  `~/.vim/` 目录下进行安装，在 Vim 运行的时候，会自动去这个目录寻找插件文件。
在 Win 环境下，这个目录在安装目录下的 `vimfiles` 目录。

在安装插件和配置 Vim 的时候在 `~/.vimrc` 和 `~/.vim/` 目录进行。优点是我们在重新安装或者转移机器的时候，只需要复制配置文件，和目录过去即可。方便易用。   
打开这个 目录会看到很多子目录


    autoload
    colors
    doc
    ftdetect
    lib
    plugin
    syntax

安装插件和主题的时候，把配置插件内容复制到这些目录即可。重启 Vim 生效。

## 配置 Vim

修改 Vim  的默认配置可以在 vimrc  文件中修改
以下是常用配置信息说明  

    syntax on " 开启高亮
    set background=dark " 默认使用 dark 模式
    set number " 显示行号
    set tabstop=4 " tab 的宽度
    set shiftwidth=4 "自动缩进的时候 tab 的宽度
    set softtabstop=4 "退格键的时候 tab 宽度
    set cindent " 设置自动缩紧
    hi Pmenu guibg=darkslategray " 下拉菜单的颜色
    set scrolloff=2 " 当光标距离下面两行的时候就进行滚动
    set number " 显示行号
    set hlsearch " 搜索高亮
    set cursorline " 突出显示当前行
    set lines=40 columns=130 " 设置默认启动窗口大小
    set cc=80 " 设置第80 列显示一根线
    set guifont=Monaco:h13 " 设置字体， 如果多种字体，用 "," 隔开
    hi ColorColumn ctermbg=darkgray guibg=darkgray " 设置第 80 行线的颜色
    set helplang=cn " 默认使用中文
    filetype on " 自动检测文件类型                                 
    filetype plugin on " 插件支持文件类型帮助信息
    set laststatus=2 " 默认显示状态栏 
    set statusline=%<%f\ %LL\ %m%r%h%w%{(&fenc!=''?&fenc:&enc).':'.&ff}\ %Y%=%04l,%04v\ %p%%\ " 设置状态栏显示内容
    set ruler " 在编辑过程中，在右下角显示光标位置的状态行
    
    if version >= 700 " 进入插入模式时改变状态栏颜色（仅限于Vim 7）
            au InsertEnter * hi StatusLine guibg=darkred guifg=darkgray gui=none
            au InsertLeave * hi StatusLine guibg=darkgreen guifg=darkgray gui=none
    endif
    
    "alt+数字切换Table快捷键设置
    :nn <M-1> 1gt
    :nn <M-2> 2gt
    :nn <M-3> 3gt
    :nn <M-4> 4gt
    :nn <M-5> 5gt
    :nn <M-6> 6gt
    :nn <M-7> 7gt
    :nn <M-8> 8gt
    :nn <M-9> 9gt
    :nn <M-0> :tablast<CR>

### 状态栏配置
状态栏可以自定义显示一些内容，方便自己查看一些常用的信息

    set laststatus=2 " 默认显示状态栏 
    set statusline=%<%f\ %LL\ %m%r%h%w%{(&fenc!=''?&fenc:&enc).':'.&ff}\ %Y%=%04l,%04v\ %p%%\ " 设置状态栏显示内容
    set ruler " 在编辑过程中，在右下角显示光标位置的状态行

对应的，会在底部的状态栏显示出

    index.php 60L utf-8:unix PHP             0036,0016 60%

    这样的信息分表代表着
    index.php 是文件的路径  
    60L 是文件的总行数  
    utf-8 是文件使用的编码格式
    unix PHP 是文件类型  
    0036,0016 是当前光标所在为在位置第 36 行，第16个字符
    60％ 是当前光标所在行，在文件中的位置百分比
    当然还可以显示文件大小，字符数等等信息，可以根据自己的需求去配置


|  参数  |  意义  |
| ----- | --------|
| %(…%) |定义一个项目组|
| %{n}* |%对其余的行使用高亮显示组 Usern，直到另一个 %n*。数字 n 必须从 1 到9。用 %* 或 %0* 可以恢复正常的高亮显示|
| %&lt; |如果状态行过长，在何处换行。缺省是在开头|
| %=    |左对齐和右对齐项目之间的分割点|
| %     |字符 %|
| %B    |光标下字符的十六进制形式|
| %F    |缓冲区的文件完整路径|
| %H    |如果为帮助缓冲区则显示为 HLP|
| %L    |缓冲区中的行数|
| %M    |如果缓冲区修改过则显示为 +|
| %N    |打印机页号|
| %O    |以十六进制方式显示文件中的字符偏移|
| %P    |文件中光标前的 %|
| %R    |如果缓冲区只读则为 RO|
| %V    |列数。如果与 %c 相同则为空字符串|
| %W    |如果窗口为预览窗口则为 PRV|
| %Y    |缓冲区的文件类型，如 Vim|
| %a    |如果编辑多行文本，这个字行串就是({current} of {arguments})，例如：(5 of 18)。如果在命令行中只有一行，这个字符串为空|
| %b    |光标下的字符的十进制表示形式|
| %c    |列号|
| %f    |缓冲区的文件路径|
| %h    |如果为帮助缓冲区显示为[Help]|
| %l    |行号|
| %m    |如果缓冲区已修改则表示为[+]|
| %n    |缓冲区号|
| %o    |在光标前的字符数（包括光标下的字符）|
| %p    |文件中所在行的百分比|
| %r    |如果缓冲区为只读则表示为[RO]|
| %t    |文件名(无路径)|
| %v    |虚列号|
| %w    |如果为预览窗口则显示为[Preview]|
| %y    |缓冲区的文件类型，如[vim]|
| %{expr}|   表达式的结果|

### 状态栏颜色

状态除了可以定制展示内容还可以定制在不同模式下的颜色。
为了方便的区分插入模式和普通模式配置在不同的模式下现实不同的颜色


    if version >= 700 " 进入插入模式时改变状态栏颜色（仅限于Vim 7）
        au InsertEnter * hi StatusLine guibg=darkred guifg=darkgray gui=none
        au InsertLeave * hi StatusLine guibg=darkgreen guifg=darkgray gui=none
    endif


### 状态栏插件
如果你不想折腾，那么也有现成的插件可以去直接使用优秀的配置方案。
[Powerline](https://github.com/powerline/powerline) ，[vim-airline](https://github.com/vim-airline/vim-airline) 两个插件都有漂亮优秀的状态栏配置。
### <leader> 前缀键
在各类 Vim 插件帮助文档中经常出现 <leader>，即，前缀键。Vim 自带有很多快捷键，再加上各类插件的快捷键，大量快捷键出现在单层空间中难免引起冲突，为缓解该问题，引入了前缀键 <leader>。
默认情况下 <leader> 是 ` \ ` 键。当遇到需要 <leader>cc快捷键的时候可以快速的按下 `\cc` 实现
如果想要修改前缀键可以添加配置

    let mapleader=";"


### 快捷键配置
Vim 操作过程中希望把操作过程给予简化，可以自定义一些快捷键

## Vim 插件

如果默认的 Vim 满足不了需求，可以通过安装插件来满足需求，下面介绍一些常用的插件。

### 中文帮助信息
下载[Vimcdoc](http://sourceforge.net/projects/vimcdoc/files/) 根据自己系统选择不同的文件，下载并安装。重启 Vim ，执行 `help` 即可看到中文帮助信息。

### NERDTree 目录浏览

NERDTree 基本是必备插件，它可以显示目录与文件结构。方便浏览。同时它也支持书签（Bookmark）可以方便的保存项目路径。  
同时，NERDTree 也支持插件，可以显示 git 状态等。插件目录位于 `~/.vim/nerdtree_plugin/`  
下载地址 [NERDTree](https://github.com/scrooloose/nerdtree)  
下载完成后把文件复制到 `~/.vim/` 在配置文件里添加一下配置  
这里推荐两个插件 [vim-nerdtree-tabs](https://github.com/jistr/vim-nerdtree-tabs)，可以使文件与窗口之间的操作更加方便。[nerdtree-git-plugin](https://github.com/Xuyuanp/nerdtree-git-plugin)可以在目录结构里面直接展示 Git 状态。


    autocmd VimEnter * NERDTree " 在 vim 启动的时候默认开启NERDTree（autocmd 可以缩写为 au）
    nmap <F2> :NERDTreeTabsToggle<CR> " 按下 F2 调出/隐藏 NERDTree

    “ 如果你也使用Vim diff ，但是不想在这个时候自动启动 NERDTree 的时候
    if &diff                                                                    
        autocmd VimEnter * NERDTreeClose                                        
    else                                                                        
        autocmd VimEnter * NERDTree " 默认启动 NERDTree                         
        let NERDTreeShowBookmarks=1 " 默认显示书签                              
        let NERDTreeWinSize=30 " 设置目录窗口宽度                               
        let g:nerdtree_tabs_open_on_console_startup=1                           
        let g:nerdtree_tabs_focus_on_files=1 " 设置 打开文件后文件窗口获得焦点  
        let g:nerdtree_tabs_smart_startup_focus=1 " 启动时焦点自动调整          
        let NERDTreeMinimalUI=1 " 不显示帮助信息                                
    endif


### NERDCommenter 快速注释插件
NERDCommenter 是 NERDTree 作者的另一插件，可以在各种文档中实现方便快捷的注释功能。

|   快捷键     | 作用     |
| --------   | --------|
|<leader>ca  | 在可选的注释方式之间切换，比如C/C++ 的块注释/* */和行注释//|
|<leader>cc  | 注释当前行|
|<leader>c空格| 切换注释/非注释状态|
|<leader>cs  | 以”性感”的方式注释|
|<leader>cA  | 在当前行尾添加注释符，并进入Insert模式|
|<leader>cu  | 取消注释|

Normal模式下，几乎所有命令前面都可以指定行数。
Visual模式下执行命令，会对选中的特定区块进行注释/反注释

### Indent Guides 对齐线
[Indent Guides](http://www.vim.org/scripts/script.php?script_id=3361) 对齐线插件
### Gitgutter 显示 Git 修改状态

Gitgutter 是一个可以显示每行的 Git 状态的插件。和nerdtree-git-plugin 不同的是，前者可以具体每行的变换。后者只能显示目录和文件的状态。  
下载 [vim-Gitgutter](https://github.com/airblade/vim-gitgutter) 下载后，把文件复制到 `~/.vim／` 目录即可。当然，你必须已经安装的有git。  
在这里可以得到更为详细的帮助信息[Gitgutter 帮助文档](https://github.com/airblade/vim-gitgutter#usage)

### Vim-Signify 显示 SVN 状态
和 Git gutter 一样 Signify 是一个针对 SVN 的插件功能和需求一样，安装之前，也需要你本地安装有 SVN 客户端 

下载地址 [Vim-Signify](https://github.com/mhinz/vim-signify)，帮助信息[Signify Documentation](https://github.com/mhinz/vim-signify#installation--documentation)

### Neocomplcache 自动补全插件

自动补全可以提高代码的书写效率，和其他 IDE 一样 Vim 也可以提供一样的功能，设置还能补全目录结构。  
当然如果有折腾的精力，可以了解下坐着另一个作品 [neocomplete.vim](https://github.com/Shougo/neocomplete.vim)  
下载地址 [neocomplcache.vim](https://github.com/Shougo/neocomplcache.vim) 
下载后安装到 `~/.vim/` 目录，并在 vimrc 文件中添加以下配置 


    let g:neocomplcache_enable_at_startup = 1 " 默认启动 Neocomplcache 
    inoremap <expr><TAB>  pumvisible() ? "\<C-n>" : "\<TAB>"  "支持 Tab 选择补全项


## 周边

习惯了 Vim 的操作方式后，会觉得非常方便，尤其对我这种用鼠标手疼的人来说简直就是福音。
如果能在浏览网页的时候也能使用 Vim 的操作该多好，vimium 插件就是来实现这个功能的。  
下载地址[Vimium 插件](https://chrome.google.com/webstore/detail/dbepggeogbaibhgnhhndojpepiihcmeb) 

## 我的配置

附上我的 vim 配置，里面有带注释，可以参考。[.vim](https://github.com/laomafeima/.vim)
