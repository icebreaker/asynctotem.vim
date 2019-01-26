asynctotem.vim
==============
A lean and mean _async command runner_ for [Vim 8][0] and later.

Please note, that only **one** command can be _running_ at any given time. **This is by design**.

### Mappings
```vim
map <C-b> :call asynctotem#run(&makeprg)<CR>
map <C-r> :call asynctotem#run(&makeprg, 'release')<CR>
map <C-r> :call asynctotem#run('random command')<CR>
map <C-r> :call asynctotem#run('random command', 'random arguments')<CR>
```

### Commands
```vim
command! -nargs=+ -complete=shellcmd Arun call asynctotem#run(<q-args>)
command! -nargs=+ -complete=shellcmd Amake call asynctotem#run(&makeprg, <q-args>)
command! -nargs=+ -complete=shellcmd Agrep call asynctotem#run(&grepprg, <q-args>)
```

### Status
The `asynctotem#status()` function, can be used in order to display the _run status_ in
a _configurable_ statusline plugin like [lightline][1].

```vim
let g:lightline =
      \ {
      \   'active': {
      \     'left': [['mode', 'paste'], ['gitbranch'], ['asynctotem', 'readonly', 'filename', 'modified']]
      \   },
      \   'component_function': {
      \     'gitbranch': 'fugitive#head',
      \     'asynctotem': 'asynctotem#status'
      \   }
      \ }
```

### Customization
There are a couple of _global_ variables that can be used to alter some of the
default behavior.

#### let g:asynctotem\_copen\_keymap
Set this to 0, in order to stop `q` being mapped to `:cclose` and `ctrl+c` to the `asynctotem#kill()`
function in the `Quickfix` window.

The default is 1.

#### let g:asynctotem\_cclose\_on\_kill
Set this to 1, in order to close the `Quickfix` window when `asynctotem#kill()` is called.

The default is 0.

#### let g:asynctotem\_cclose\_on\_no\_error
Set this to 1, in order to close the `Quickfix` window when there are no errors.

The default is 0.

#### let g:asynctotem\_cclose\_delay
Set this to the desired amount of milliseconds after which the `Quickfix` window
will be closed, when `g:asynctotem_cclose_on_kill` or `g:asynctotem_cclose_on_no_error`
are set to 1.

The default is 1000ms (1 second).

Contribute
----------
* Fork the project.
* Make your feature addition or bug fix.
* Do **not** bump the version number.
* Send me a pull request. Bonus points for topic branches.

License
-------
Copyright (c) Mihail Szabolcs. Distributed under the same terms as Vim itself. See
:help license.

[0]: https://www.vim.org
[1]: https://github.com/itchyny/lightline.vim
