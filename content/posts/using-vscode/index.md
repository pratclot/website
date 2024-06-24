+++
title = 'Using VSCode'
date = 2024-06-24T09:40:52+02:00
draft = false
+++

Here are some actions and their shortcuts that will make you effective with VSCode.

| action                           | shortcut            | notes                                                                                                                                                                                                                                                                      |
| -------------------------------- | ------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| search symbols                   | ctrl + shift + o    | shows a searchable document structure, super handy for `yaml` or other long files navigation                                                                                                                                                                               |
| go to one of previous files      | ctrl + tab          | hold `ctrl` to observe a list of those                                                                                                                                                                                                                                     |
| find file by name                | ctrl + p            | makes it easy to navigate between files                                                                                                                                                                                                                                    |
| search any action                | ctrl + shift + p    | use this if you want to do something, but to not know a shortcut yet, or do not care to learn one                                                                                                                                                                          |
| open settings                    | ctrl + ,            |
| add a new line after current one | ctrl + enter        |
| reformat document                | ctrl + shift + i    | there is nothing more daunting than formatting files by hand, this is not needed at all when you have "standard" formatting conventions. This shortcut will make you happy and productive. `esbenp.prettier-vscode` helped me to structure this table without going insane |
| open preview for a markdown file | ctrl + shift + v    | it helps a lot to see a rendered file                                                                                                                                                                                                                                      |
| "close" file                     | ctrl + w            | this one feels natural for a browser user, but can be very unpleasant if you also like to use this key combo to delete a word, like you can do in `bash`                                                                                                                   |
| delete current line              | ctrl + shift + k    | this is fastest way to delete a line, do not underestimate it                                                                                                                                                                                                              |
| enable word wrapping             | alt + z             | very useful when you have lengthy lines, it removes the need to scroll horizontally to read them . This can also be enabled globally, search for "Word Wrap"                                                                                                               |
| show keybindings                 | ctrl + k, ctrl + s  | allows to change some shortcuts if you like IDEA ones for example (like go back and forward)                                                                                                                                                                               |
| open extensions                  | ctrl + shift + x    | a quick way to install more productivity helpers                                                                                                                                                                                                                           |
| show project files               | ctrl + shift + e    | it also helps to enable "Auto Reveal" setting if you feel more comfortable knowing where you are in the workspace now                                                                                                                                                      |
| toggle left bar                  | ctrl + b            |
| delete word                      | ctrl + backspace    | it is better than holding backspace                                                                                                                                                                                                                                        |
| open terminal                    | ctrl + `            | this one really sucks on Mac                                                                                                                                                                                                                                               |
| add cursor                       | alt + click         | allows you to edit text in multiple places at once, do not forget to use this                                                                                                                                                                                              |
| rectangular selection            | alt + shift + click | useful to know that something like this exists                                                                                                                                                                                                                             |
| comment current line             | ctrl + /            | IDEA also moves to the next line after commenting, which I find to be a superior implementation                                                                                                                                                                            |
| show suggestions                 | ctrl + space        | this is one of the best features of any text editor or IDE                                                                                                                                                                                                                 |
| open new window                  | ctrl + shift + n    | may be needed when you are working with multiple unrelated directories                                                                                                                                                                                                     |
| move line up                     | alt + up            |
| show quick fixes                 | ctrl + .            |
| go to next error                 | f8                  | this one is better in IDEA (f2), but I can live with that                                                                                                                                                                                                                  |
| rename symbol or file            | f2                  |
| find in file                     | ctrl + f            |
| replace in file                  | ctrl + h            | you can also use selections to limit replacement scope                                                                                                                                                                                                                     |

I like very much the shortcuts in IDEA on a Mac, mainly because it is way easier to press `cmd` button than `ctrl + shift` (IDEA's Linux and Windows keymap blows, and I am wondering if I should also use `alt` on Linux instead of `ctrl`. I did this for Android Studio and could not have been happier). On the other hand, I do not like customizing things too much because it will make me dependent on a certain environment, and will surely render me unproductive outside of it. It was not easy to shift from Android Studio to VSCode for me, but I am happy that I did not try to overwrite all of the shortcuts and instead learned the standard ones in VSCode. There are a few that are ridiculously better in IDEA on a Mac though, here are the important ones that I use all the time:

| action                           | shortcut | notes                                                                                                                                                                                                                                        |
| -------------------------------- | -------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| show signature / parameter hints | alt + p  | I use a custom shortcut that matches what I would _physically_ press in IDEA                                                                                                                                                                 |
| go forward                       | alt + ]  |
| go back                          | alt + [  |
| duplicate line                   | alt + d  | this one is super good because it does not require you to overwrite your clipboard. Speaking of clipboards, `CopyQ` is an excellent free tool that will serve as a backup for you memory, please include something like this in your arsenal |

Then there are a few super shortcuts that I like from default `bash` configuration. Those come from `emacs` actually, but I never it used, lol. You can configure this at OS-level on a Mac and Linux (they are handy in a browser too), in my case I had to overwrite those shortcuts in VSCode.

| action        | shortcut | notes                                                                                                                                                              |
| ------------- | -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| go line end   | ctrl + e |
| go line start | ctrl + a | one huge downside is that you will need to use something else for `select all` action, in my case I configured `alt + a` for VSCode, and use `ctrl + /` in browser |

A useful feature built into IDEA is bookmarks. It allows you to select certain places in a few of files you are currently working with, and quickly move between them. I use `alefragnani.Bookmarks` to have a similar functionality.

| action         | shortcut | notes |
| -------------- | -------- | ----- |
| place bookmark | f3       |
| list bookmarks | alt + f3 |

Another helpful OS-level thing is to increase "key repeat" speed (and also decrease delay for it). You will anyway use arrows to navigate horizontally at some point, so why not make it faster and less annoying?

Lastly, if you are writing a lot of readable text it is handy to have at least a spellchecker. I use `ban.spellright` as it claims to do everything offline. It does not check if your sentences are constructed properly though, another extension could probably help with that.
