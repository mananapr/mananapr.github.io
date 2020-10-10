# Ameliorating Windows 10

So recently I got myself a M.2 SSD to get on the SSD bandwagon. I decided to do a fresh install of both Windows and Arch Linux rather than copying over my existing partitions to the SSD.
One of the reasons for doing this was to try out Windows 10 Ameliorated<sup>[1]</sup>. The "Build Yourself" process of AME is pretty long so I decided to take a shortcut

If you go through the AME docs, they tell you to only use Windows 1903 and to not setup Internet on your fresh Windows Install. According to the docs, If Windows Update gets internet
connectivity, then we'll have to do a fresh install once again -
<blockquote>
It is again very vital to mention that no internet connection be established during the entire installation!
</blockquote>

I quickly went through the AME Script to see what it does. To put it simply, it just uses fzf to search for installed file locations of programs like *Cortana*, *Update* etc. It then recursively
deletes those paths. It makes no sense to me why enabling internet would get in the way of this process. I suppose they have mentioned it for users who don't want to ping Microsoft Servers even once.

Anyway, I decided to take a shortcut - I installed Windows 10 LTSC and used Windows Update to get the latest updates and drivers. Once my system was up to date, I proceeded to install MS Office 2019. I did this before
the Amelioration process because I had read that AME only supports Office 2007. So I wanted to try this to see if it would work Post-Amelioration. Once Office was set up, I went ahead with the Amelioration
process as mentioned in the Docs (minus the manual updating and drivers part).

The Amelioration process finished within 30 minutes for me. Once I booted into Windows, I tried running Office 2019 and it seems to be working well 😀 -
<picture>
  <img src="/images/win10_ame0.png" alt="Office 2019 on Windows 10 AME">
</picture>

The actual setup is exactly the same as my LTSC setup that I had shared in an earlier post<sup>[2]</sup>.
<picture>
  <img src="/images/win10_ame1.png" alt="Windows 10 AME Setup">
</picture>

Opening the Windows 10 Settings app I was surprised to see how empty it looked. No Cortana, No Updates, No Xbox -
<picture>
  <img src="/images/win10_ame2.png" alt="Windows 10 AME Settings">
</picture>

Because Cortana gets removed, the search functionality in the default Start Menu gets broken. So a replacement needs to be installed. The Amelioration script installs Classic Shell<sup>[3]</sup> by default.
I customized it to look like a fusion of Windows 7 and Windows 10 Start Menu -
<picture>
  <img src="/images/win10_ame3.png" alt="Windows 10 AME Start Menu">
</picture>

I also installed Cygwin<sup>[4]</sup> this time as a replacement for WSL. I haven't really properly setup my Cygwin installation yet but so far it seems really good. I've installed lf<sup>[5]</sup>, my file manager
of choice and it seems to be working pretty well in Cygwin.
<picture>
  <img src="/images/win10_ame4.png" alt="Windows 10 AME Cygwin">
</picture>

Even though my Windows install is much leaner now, installing a SSD hasn't really improved boot times in a major way. But at an overall level it has become much more snappier.
<br>
There has been a very noticeable improvement in boot times for my Arch Linux install though. It boots up in less than 6seconds. At an overall level, my Arch installation has always been pretty
snappy but I did notice a major improvement in app launch times after a cold boot.

All in all, I'm pretty happy with the purchase and with my current setup. There have been some changes in my Linux setup as well so I might make a post on that.

---

Sources:

- `[1]`: <https://ameliorated.info>
- `[2]`: <https://mananapr.github.io/win10_ltsc.html>
- `[3]`: <http://classicshell.net/>
- `[4]`: <https://cygwin.com/>
- `[5]`: <https://github.com/gokcehan/lf>

<br>
<center><i>
comments and questions can be left [here](https://github.com/mananapr/mananapr.github.io/issues)
</i></center>
