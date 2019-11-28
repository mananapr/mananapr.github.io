# Moving from Alpine to KISS Linux

After using Alpine for quite a while, I reinstalled Arch on a separate partition
and was able to achieve a similar package count as Alpine. Plus I had other advantages like
the AUR, better community support and timely package updates.

So, I decided to move to something even lighter. Searching online, I found a reddit post about KISS Linux.
After checking out the website, I was sold. I immediately formatted my Alpine partition
and installed KISS.

<picture>
  <img src="/blog/images/kiss1.png" alt="kiss">
</picture>

KISS is a source based distro that like Alpine, uses `musl` libc. Yes, compiling packages
takes a **LOT** of time, but I like how I can customize packages to my needs as well, unlike binary packages.
For example, I modified the vim build script so that it compiles vim with `xterm_clipboard` support.
Distros like Arch serve vim binaries that have been compiled without clipboard support.

The packaging system is also pretty simple and straightforward, following the KISS philosophy.
All of the utilities like the package manager for example, have been written in POSIX compliant shell script.

<picture>
  <img src="/blog/images/kiss2.png" alt="kiss">
</picture>

The KISS package manager doesn't handles the kernel. That means you have to download the kernel source (and firmware blobs if needed)
and compile it yourself. Configuring the kernel can be a complicated process as there are a lot of options to go through. But once
you have a working config, you can reuse the config file for kernel updates.
Also, the resulting size of the kernel image is much smaller when compared to distros like Arch.
My kernel image for v5.4 is 9MB while on Arch, it's 60+MB for v5.13.

I also switched from `openbox` to `sowm`, which is also made by the same guy who made KISS.
`sowm` is not EWMH compliant, that means my tiling script (rtile) doesn't works on `sowm`.
But I have gotten used to the floating only workflow, thanks to tmux :)

<picture>
  <img src="/blog/images/kiss3.png" alt="kiss">
</picture>

This project is single-handedly managed and maintained by Dylan Araps.
He is the same guy who made `sowm`, `fff`, `neofetch`, `pywal` and other cli utilities.
Not only is he a very talented programmer, he is extremely helpful as well. He hangs out on the
`#kisslinux` irc channel on `freenode`, where he is prompt to answer any doubts or queries.
I asked him if he would create me an icon for KISS so that I can use it for my bootloader.He sent me an icon within minutes :)

He also has a Patreon that I'll link in the bottom.

---

Sources:

- `KISS Website`: <https://getkiss.org>
- `KISS Github`: <https://github.com/kisslinux>
- `Dylan's Github`: <https://github.com/dylanaraps>
- `Dylan's Patreon`: <https://www.patreon.com/dyla>
- `sowm`: <https://github.com/dylanaraps/sowm>
