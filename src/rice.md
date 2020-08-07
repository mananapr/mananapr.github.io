# Minimal Linux desktop

My laptop runs Alpine Linux with Openbox as its window manager. The only GUI applications that run are my web browser(`firefox`) and my password manager(`KeepassXC`). The rest of the system is controlled and used through the terminal.

```
   /\ /\        manan@miku
  // \  \       os     Alpine Linux edge
 //   \  \      host   HP ProBook 450 G3
///    \  \     kernel 4.19.78-1-vanilla
//      \  \    uptime 1d 9h 31m
         \      pkgs   484
                memory 317M / 7878M
```

I don't use an automatic wallpaper based colorscehme generator like `pywal` but have it installed to manage my static colorschemes.

<picture>
  <img src="/images/rice1.png" alt="desktop">
</picture>

The system information tool I use is a simple bash script called [`pfetch`](https://github.com/dylanaraps/pfetch). I don't use a bar but have a simple [shell script](https://github.com/mananapr/dotfiles/blob/master/bin/bar) to display a popup that shows me information like time and battery.

<picture>
  <img src="/images/rice2.png" alt="desktop">
</picture>

My text editor is `vim` using the `goyo` plugin to hide the user interface and center the file's contents. I will write more about my vim setup in a separate post. The music player is `mpv` running inside of my local music library. I do not need a fancy program to provide a library, playlists and metadata.

The big upside to `mpv` is that my video player, image viewer and music player are all the same program. The configuration is unified between the three and the hotkeys are all the same.

<picture>
  <img src="/images/rice3.png" alt="desktop">
</picture>

I talk primarily over IRC using the `irssi` irc client, with most of its interafce hidden. To stay logged into the IRC servers all the time I run `irssi` on a raspberry pi which stays on 24x7. I can then ssh into the pi to use irc.

<picture>
  <img src="/images/rice4.png" alt="desktop">
</picture>

Resource usage is extremely low and time on battery is high. So far I have been loving Alpine Linux. After 3 years of using Arch, I wanted to try a distro wihout `systemd` and `dbus` and decided to go with Alpine considering it's incredibly small base install size.

That being said Alpine has it's negatives too. Some proprietary applications like games for eg, are compiled against `glibc` but as Alpine uses `musl` as it's libc they won't work on Alpine. Also packages are not updated in a timely manner and the project suffers from a lack of maintainers.

<picture>
  <img src="/images/rice5.png" alt="desktop">
</picture>

I used to use `i3-gaps` as my WM before switching to `Openbox` and to make up for i3's tiling capabilities I have been using a tiling script called `rtile`.

---

Sources:

- `dotfiles`: <https://github.com/mananapr/dotfiles>
- `rtile`: <https://github.com/xhsdf/rtile>

<br>
<center><i>
comments and questions can be left [here](https://github.com/mananapr/mananapr.github.io/issues)
</i></center>
