# vimrc

```shell
syntax on

set noerrorbells
set relativenumber
set tabstop=4 softtabstop=4
set shiftwidth=4
set expandtab
set smartindent
set nu
set nowrap
set smartcase
set noswapfile
set nobackup
set undodir=~/.vim/undodir
set undofile
set incsearch
set ai
set cursorline
set hlsearch
set wildmenu
set showmatch
set showcmd
set ignorecase

set cmdheight=2

set colorcolumn=80
highlight ColorColumn ctermbg=0 guibg=lightgrey

let NERDTreeShowHidden = 1

let g:NERDSpaceDelims = 1

call plug#begin('~/.vim/plugged')

Plug 'scrooloose/nerdtree'
Plug 'jremmen/vim-ripgrep'
Plug 'kien/ctrlp.vim'
Plug 'vim-syntastic/syntastic'
Plug 'mattn/emmet-vim'
Plug 'jiangmiao/auto-pairs'
Plug 'danro/rename.vim'
Plug 'morhetz/gruvbox'
Plug 'Valloric/YouCompleteMe', { 'do': './install.py'  }
Plug 'mbbill/undotree'
Plug 'preservim/nerdcommenter'

call plug#end()

colorscheme gruvbox
set background=dark

let g:ctrlp_user_command = ['.git', 'git --git-dir=%s/.git ls-files -oc --exclude-standard']
let g:ctrlp_working_path_mode='ra'
let mapleader = " "
let g:netrw_browse_split=2
let g:netrw_banner=0
let g:netrw_winsize=25

let g:ctrp_use_cache=0

" sync open file with NERDTree
" Check if NERDTree is open or active
function! IsNERDTreeOpen()
    return exists("t:NERDTreeBufName") && (bufwinnr(t:NERDTreeBufName) != -1)
endfunction

" Call NERDTreeFind if NERDTree is active, current window contain a modifiable
" file, and we're not in vimdiff

function! SyncTree()
    if &modifiable && IsNERDTreeOpen() && strlen(expand('%')) > 0 && !&diff
        NERDTreeFind
        wincmd p
    endif
endfunction
" Hightlight currently open buffer in NERDTree
autocmd BufEnter * call SyncTree()

map <C-n> :NERDTreeToggle<CR>

nnoremap <leader>h :wincmd h<CR>
nnoremap <leader>j :wincmd j<CR>
nnoremap <leader>k :wincmd k<CR>
nnoremap <leader>l :wincmd l<CR>
nnoremap <leader>u :UndotreeShow<CR>
nnoremap <leader>pv :wincmd v<bar> :Ex <bar> :vertical resize 30<CR>
nnoremap <leader>ps :Rg<SPACE>
nnoremap <silent> <leader>+ :vertical resize +5<CR>
nnoremap <silent> <leader>- :vertical resize -5<CR>

" YCM
" The best part
nnoremap <silent> <leader>gd :YcmCompleter GoTo<CR>
nnoremap <silent> <leader>gf :YcmCompleter FixIt<CR>
```
