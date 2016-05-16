" 定义快捷键的前缀，即<Leader>
let mapleader=","

" 开启文件类型侦测
filetype on
" 根据侦测到的不同类型加载对应的插件
filetype plugin on

" 让配置变更立即生效
"autocmd BufWritePost $MYVIMRC source $MYVIMRC

" 开启实时搜索功能
set incsearch
" 搜索时大小写不敏感
set ignorecase
" 关闭兼容模式
set nocompatible
" vim自身命令行模式智能补全
set wildmenu

" vundle环境设置
" git clone https://github.com/VundleVim/Vundle.vim.git ~/.vim/bundle/Vundle.vim
" 安装命令 
" :PluginInstall
" 删除命令，首先从配置文件中删除，然后执行下面命令
" :PluginClean
" 更新命令
" :PluginUpdate
filetype off
set rtp+=~/.vim/bundle/Vundle.vim
" vundle管理的插件列表必须位于vundle#begin()和vundle#end()之间
call vundle#begin()
Plugin 'VundleVim/Vundle.vim'
Plugin 'altercation/vim-colors-solarized'
Plugin 'tomasr/molokai'
Plugin 'vim-scripts/phd'
Plugin 'toupeira/vim-desertink'
Plugin 'derekwyatt/vim-fswitch' "接口与实现快速切换
Plugin 'nathanaelkane/vim-indent-guides' "可视化代码缩进
Plugin 'majutsushi/tagbar' "标签列表
Plugin 'fholgado/minibufexpl.vim' "多文档编辑
Plugin 'scrooloose/nerdtree' "工程文件浏览
" 插件列表结束
call vundle#end()
filetype plugin indent on

" 配色方案
set background=dark
colorscheme desertink
"colorscheme solarized
"colorscheme molokai
"colorscheme phd

" 设置gvim显示字体
set guifont=Consolas:h19

" 禁止光标闪烁
set gcr=a:block-blinkon0
" 禁止显示滚动条
set guioptions-=l
set guioptions-=L
set guioptions-=r
set guioptions-=R
" 禁止显示菜单和工具条
set guioptions-=m
set guioptions-=T

" 将外部命令wmctrl控制窗口最大化的命令行参数封装成一个vim的函数
fun! ToggleFullScreen()
    call system("wmctrl -ir " . v:windowid . " -b toggle,fullscreen")
endf
" 全屏开/关快捷键
map <silent> <F11> :call ToggleFullScreen()<CR>
" 启动vim时自动全屏
" autocmd VimEnter * call ToggleFullScreen()

" 总是显示状态栏
set laststatus=2
" 显示光标当前位置
set ruler
" 开启行号显示
set number
" 高亮显示当前行/列
set cursorline
set cursorcolumn
" 高亮显示搜索结果
set hlsearch

" 禁止折行
set nowrap

" 设置状态栏主题风格
let g:Powerline_colorscheme='solarized256'

" 开启语法高亮功能
syntax enable
" 允许用指定语法高亮配色方案替换默认方案
syntax on

" 自适应不同语言的智能缩进
filetype indent on
" 将制表符扩展为空格
set expandtab
" 设置编辑时制表符占用空格数
set tabstop=4
" 设置格式化时制表符占用空格数
set shiftwidth=4
" 让vim把连续数量的空格视为一个制表符
set softtabstop=4

" 多层缩进
" 随vim自启动
let g:indent_guides_enable_on_vim_startup=1
" 从第二层开始可视化显示缩进
let g:indent_guides_start_level=2
" 色块宽度
let g:indent_guides_guide_size=1
" 快捷键i开/关缩进可视化
:nmap <silent> <Leader>i <Plug>IndentGuidesToggle

" 基于缩进或语法进行代码折叠
" za:打开或关闭当前折叠，zM:关闭所有折叠,zR:打开所有折叠
"set foldmethod=indent
set foldmethod=syntax
" 启动vim时关闭折叠代码
set nofoldenable

" *.cpp 和 *.h 间切换
nmap <silent> <Leader>ch :FSHere<cr>

" 回车打开选中文件，r刷新工程目录文件列表
" 使用NERDTree插件查看工程文件，设置快捷键，速记：file list
nmap <Leader>fl :NERDTreeToggle<CR>
" 设置NERDTree子窗口宽度
let NERDTreeWinSize=22
" 设置NERDTree子窗口位置
let NERDTreeWinPos="right"
" 显示隐藏文件
let NERDTreeShowHidden=1
" NERDTree子窗口中不显示冗余帮助信息
let NERDTreeMinimalUI=1
" 删除文件时自动删除文件对应buffer
let NERDTreeAutoDeleteBuffer=1

" 显示/隐藏MiniBufExplorer窗口
map <Leader>bl :MBEToggle<CR>
" buffer切换快捷键
" ctrl-tab正向遍历buffer，ctrl-shift-tab逆向遍历
" 在某个buffer上键入d删除光标所在的buffer
map <Leader>bn :MBEbn<CR>
map <Leader>bp :MBEbp<CR>
" 在某个buffer上键入s将该buffer对应window与先前的window上下排列
" 在某个buffer上键入v将该buffer对应window与先前的window左右排列

" vsplit垂直打开一个新窗口
" vertical resize N命令可以调整窗口的宽度

" 设置tagbar子窗口的位置出现在编辑区的左边
let tagbar_left=1
" 设置显示/隐藏标签列表子窗口的快捷键。速记：tag list
nnoremap <Leader>tl :TagbarToggle<CR>
" 设置标签子窗口的宽度
let tagbar_width=22
" tagbar子窗口中不显示冗余帮助信息
let g:tagbar_compact=1
