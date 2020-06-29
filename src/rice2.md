# Minimal Linux Desktop Update

It has been nearly 8 months since I last wrote about my linux desktop. Since then I've made a lot of changes.

<picture>
  <img src="/images/rice2_1.png" alt="desktop">
</picture>

So as you can see in the screenshot above I've moved back to Arch Linux.
Not because I was unhappy with Alpine or KISS Linux, but because I had to install a lot of other applications dependent on KDE.

So here I am back on Arch again. But this time I am running Suckless's DWM (Dynamic Window Manager) instead of Openbox.
<br>
It's lightweight, has tiling and above all - very customizable because it has a source based configuration.
<br>
Rather than enabling options on or off in the config file, in DWM - the source code is the config file.
You download patches for the functionality you need and patch it into the source code. So each user's DWM build is going to be unique and will have no bloat at all.
<br>
If you are interested in testing out my build of `st` or `dwm` - I'll link to my build in the sources.

<picture>
  <img src="/images/rice2_2.png" alt="desktop">
</picture>

For IRC - I've switched from `irssi` to `Weechat` mainly because Weechat is in active development while irssi hasn't received a commit in quite a while.
<br>
Weechat has better plugin support as well. I mostly hangout on `#rice` and `#8chan` on the Rizon IRC Network though I sometimes visit Lainchan's IRC network as well.

<picture>
  <img src="/images/rice2_3.png" alt="desktop">
</picture>

I mostly use the default stack layout in DWM but I do have the CentredMaster and Fibonacci Layouts patched as well. I might remove them later because I haven't used them even once.
<br>
I guess that's because I don't like to keep more than 3 windows in one workspace.

Talking about workspaces - I am not using the default numeric tags. I've named them as 3-4 letter words describing the purpose of that workspace:

- **web**: Icecat (because Firefox broke on me)
- **tor**: Tor-Browser
- **irc**: Weechat
- **dev**: Windows related to project work and programming
- **fun**: Music, Movies etc
- **misc**: Miscellaneous
- **mail**: neomutt
- **chat**: signal desktop

<picture>
  <img src="/images/rice2_4.png" alt="desktop">
</picture>

I've also started using `newsboat`, which is a RSS reader for the terminal. It's really customizable and looks great.

Also, I've switched `lf` as my file manager and no longer use `monaco` as my terminal font. Instead, I've been using `Iosevka`
and it did take me some time to get used to its narrow look but I absolutely adore it now.
<br>
I am using a patched version of the font that supports Nerd Fonts glyphs. These glyphs include Powerline symbols which I use in neomutt and
icons which I use in `lf`.

---

Sources:

- `dotfiles`: <https://github.com/mananapr/dotfiles>
- `dwm`: <https://github.com/mananapr/dwm-stuff>
- `st`: <https://github.com/mananapr/st>
- `lf`: <https://github.com/gokcehan/lf>
- `newsboat`: <https://github.com/newsboat/newsboat>
- `neomutt`: <https://github.com/neomutt/neomutt>
- `Iosevka`: <https://github.com/be5invis/Iosevka>
- `Nerd Fonts`: <https://github.com/ryanoasis/nerd-fonts>

<br>
<center><i>
comments and questions can be left [here](https://github.com/mananapr/blog/issues)
</i></center>
