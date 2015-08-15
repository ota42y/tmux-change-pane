# tmux-change-pane
Change tmux panes

![](/img/demo.gif)

This software change current pane to other pane.  
This is inspired by [swap-pane](https://github.com/abicky/swap-pane).  

# Installation

## 1. Add files to your PATH

```
git clone git@github.com:ota42y/tmux-change-pane.git
cp * /path/to/your/bin/
```

## 2. Install pero (or percol)

change-pane depend on [peco](https://github.com/peco/peco), so you must install it.

If you use Mac OS X/Homebrwe, you can install this command.
```
brew install peco
```

Otherwise, you should check [peco](https://github.com/peco/peco) installation section.  
Most of the time, download birany and set it to your PATH.

This software support [percol](https://github.com/mooz/percol), so you can use it instead of peco.

```
pip install percol
```

## 3. Add the following lines in your .zshrc and .tmux.conf

### .zshrc

```
autoload -U add-zsh-hook

if [ "$TMUX" ]; then
function _set-pane-name() {
local max_cmd_length=20
local cmd=$1
if [ $#cmd -gt $max_cmd_length ]; then
cmd="${cmd:0:$max_cmd_length}..."
fi
printf "\033]2;${PWD/$HOME/~}: $cmd\033\\"
}

add-zsh-hook preexec _set-pane-name
add-zsh-hook precmd _set-pane-name
fi
```

### .tmux.conf
You can change hotkey.

```
bind-key b run-shell 'change-pane'
bind-key B run-shell 'new-pane'
```


# Usage
If you change current  pane, execute `change-pane` command or type `<tmux prefix> b`.

This command opens a temporary window to select an existing pane, so you can swap the current pane even if its process is not finished yet.

You can also execute `new-pane` or type `<tmux prefix> B` to swap the current pane with a new pane.

# Difference to `swap-pane`

## use 1 pane only
This is inspired by [swap-pane](https://github.com/abicky/swap-pane).  
When you select change pane `swap-pane` open new window and overwarp all tmux pane.  
So if you split window, new pane hide other panes.  

The `change-pane` not overwrap other pane.  
This command create new pane to select an existing pane and change new pane to current pane.  
So, you can look other pane when select pane.

## peco support
This software support peco and percol.

# Author

ota42y

# Copyright and License

Copyright (c) 2014 Takeshi Arabiki licensed under the [MIT license](http://opensource.org/licenses/MIT).
