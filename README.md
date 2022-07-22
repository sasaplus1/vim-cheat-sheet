# vim-cheat-sheet

my Vim cheat sheet

## How to use

Needs [fzf](https://github.com/junegunn/fzf) and [fzf.vim](https://github.com/junegunn/fzf.vim):

```vim
function! s:fzf_my_cheat_sheet(query) abort
  let command = executable('rg') ?
        \ 'rg --color=always --column --line-number --no-heading --smart-case -- %s || true' :
        \ 'git grep --ignore-case -- %s || true'

  let options = {
        \ 'dir' : '/path/to/vim-cheat-sheet/cheatsheet',
        \ 'options' : [
        \   '--bind', 'change:reload:' . printf(command, '{q}'),
        \   '--disabled',
        \   '--preview-window', 'top,80%',
        \   '--prompt', 'CheatSheet> ',
        \   '--query', a:query,
        \ ],
        \ 'window' : {
        \   'height' : 0.6,
        \   'width' : 0.6,
        \ },
        \ }

  call fzf#vim#grep(
        \ printf(command, shellescape('title:')),
        \ 0,
        \ fzf#vim#with_preview(options)
        \ )
endfunction

command! -nargs=* MyCheatSheet call s:fzf_my_cheat_sheet(<q-args>)

nnoremap <silent> ,ch :<C-u>MyCheatSheet<CR>
```

## Demo

https://user-images.githubusercontent.com/309466/180336633-48d867a5-9581-4599-a739-45a8227fb588.mov

## License

The MIT license
