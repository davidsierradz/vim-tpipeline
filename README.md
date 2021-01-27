# vim-tpipeline

Outsource your vim statusline to tmux!

# Installation

Using **vim-plug**:

```vim
Plug 'vimpostor/vim-tpipeline'
```

Put this in your `~/.tmux.conf`:

```bash
set -g status-bg default
set -g status-right '#(tail -f #{socket_path}-\#{session_id}-vimbridge)'
set -g status-right-length 120
set -g status-interval 1
```

Restart tmux and now you should see your vim statusline inside tmux.

`vim-tpipeline` is compatible with most statuslines and can be used together with other statusline plugins like *lightline*. If it doesn't work with yours, file a bug report.

# Configuration

By default `vim-tpipeline` will copy your standard vim `statusline`. If your `statusline` is empty, the default *tpipeline statusline* from the screenshot above is used.
If you want to use a different statusline just for tmux, you can set it manually:

```vim
let g:tpipeline_statusline = '%!tpipeline#stl#line()'
" You can also use standard statusline syntax, see :help stl
let g:tpipeline_statusline = '%f'
```

By default `vim-tpipeline` flattens the statusline into one continuous chunk. If you would like to keep the left part and right part separate, then set `let g:tpipeline_split = 1` in your `.vimrc` and use the following tmux block instead:

```bash
set -g status-bg default
set -g status-left '#(tail -f #{socket_path}-\#{session_id}-vimbridge)'
set -g status-left-length 120
set -g status-right '#(tail -f #{socket_path}-\#{session_id}-vimbridge-R)'
set -g status-right-length 120
set -g status-interval 1
set -g status-justify centre # optionally put the window list in the middle
```

If you use the default *tpipeline statusline*, then you can set the length of the progress widget using:

```vim
let g:tpipeline_progresslen = 10
```

# FAQ

## Can I use the default *tpipeline statusline* outside of tmux as well?

Yes, use `set stl=%!tpipeline#stl#line()` in your `~/.vimrc`. In fact this plugin uses *Vim*'s autoload mechanism to lazily load features, i.e. if you don't use tmux, you can still use the statusline inside vim without a performance penalty.
