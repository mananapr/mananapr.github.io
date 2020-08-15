# Windows 10 LTSC is GOAT

I think it's pretty much settled that Windows 10 is one of the worst products by Microsoft, if not the worst. Even though it's a paid (and expensive) software, it still has ads, telemetry and forced
updates. I was running a Windows 10 Pro installation alongside my Linux install mainly for games and occasional MS Office. I had disabled telemetry and removed bloat like OneDrive, Xbox etc. but goddamn was
it still bloated. After some research I found the perfect Windows 10 edition - LTSC aka Long Term Support Channel.

This version of Windows is meant for enterprise use but unlike Windows 10 Enterprise, this doesn't comes with any bloat and has no forced updates. Speaking of updates, the only updates it gets are critical
security updates and not feature updates which is super nice. There are no ads as well and telemetry is at a low level out of the box (which can be completely disabled using the DisableWinTracking<sup>[1]</sup>
tool).

This is how my LTSC installed looked when I first booted into it -

<picture>
  <img src="/images/win10_ltsc_1.png" alt="Stock Win10 LTSC">
</picture>

As you can see, it's super barebones - no Edge, no OneDrive, no Microsoft Store. Don't worry, you won't have to install the drivers yourself. For me, the drivers got installed in the background automatically.

Now before you go to Microsoft website to download the ISO, wait a second, It's not that simple. The thing is, Microsoft only provides an evaluation ISO on their website. This means, the OS will only work for 90days,
after which it will start shutting down after one hour of usage. There is no way to activate this ISO. Instead, we need to use the Windows Enterprise ISO and convert it into a LTSC ISO using SFV patching. This works
becuase Enterprise license is valid for LTSC as well.
<br>
Now I know that not everyone can do this. So I recommend you get a pre-made ISO. Make sure you get a legit ISO and stay away from pre-activated ISOs. You can find a safe link at a subreddit that sounds a lot like
r/privacy. The ISO name and SHA-1 checksum should be as follows -
```
SW_DVD5_WIN_ENT_LTSC_2019_64-bit_English_MLF_X21-96425.iso
D5B2F95E3DD658517FE7C14DF4F36DE633CA4845
```

Once you get the ISO, make a bootable USB using rufus<sup>[2]</sup> and install Windows as usual. After you boot into it, you can activate it using either a self hosted KMS server (about which I made a [post](/microsoft_activation.html))
or use someone else's KMS server or use something like *KMS38* that uses a local server. You're all set!

I enabled the dark mode and set an overall greyish tone for my installation as shown below -

<picture>
  <img src="/images/win10_ltsc_5.png" alt="My Win10 Setup">
</picture>

<picture>
  <img src="/images/win10_ltsc_3.png" alt="My Win10 Setup">
</picture>

## Installing a Package Manager

Installing all of your software manually is going to get a little annoying, specially for LTSC. So I would recommend you install Chocolatey<sup>[3]</sup> - a nice package manager for Windows.

It installed all of my software in one go -
```
choco install 7zip mpv ffmpeg youtube-dl ungoogled-chromium pass-winmenu imageglass qbittorrent
```

<picture>
  <img src="/images/win10_ltsc_2.png" alt="Win10 Start Menu">
</picture>

As you can see, everything has been installed with proper menu entries and PATH variables were also set automatically.

I use *pass*<sup>[4]</sup> as my password manager. It has a windows client in the chocolatey repos called *pass-winmenu* that is very handy.
Just pressing `Ctrl` `Alt` `P` opens up a nice popup menu with all my password entries.

<picture>
  <img src="/images/win10_ltsc_4.png" alt="Pass Winmenu">
</picture>

IMO this is how Windows 10 should have been released. This is one of the best editions of Windows out there, if not the best.

---

Sources:

- `[1]`: <https://github.com/10se1ucgo/DisableWinTracking>
- `[2]`: <https://rufus.ie/>
- `[3]`: <https://chocolatey.org/>
- `[4]`: <https://www.passwordstore.org/>

<br>
<center><i>
comments and questions can be left [here](https://github.com/mananapr/mananapr.github.io/issues)
</i></center>
