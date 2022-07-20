# vim-cheat-sheet

my Vim cheat sheet

## How to use

Needs [fzf](https://github.com/junegunn/fzf) and [fzf.vim](https://github.com/junegunn/fzf.vim):

```vim
function! s:fzf_my_cheat_sheet(query) abort
  let command = 'git grep -- %s'
  let options = {
        \ 'dir' : '/path/to/vim-cheat-sheet',
        \ 'options' : [
        \   '--bind', 'change:reload:' . printf(command, '{q}'),
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
        \ printf(command, shellescape(a:query)),
        \ 0,
        \ fzf#vim#with_preview(options)
        \ )
endfunction

command! -nargs=* MyCheatSheet call s:fzf_my_cheat_sheet(<q-args>)

nnoremap <silent> ,ch :<C-u>MyCheatSheet<CR>
```

## Demo

https://user-images.githubusercontent.com/309466/179929271-9d58855b-225c-44bb-b3f8-2d9bcef455a0.mov

## License

The MIT license
