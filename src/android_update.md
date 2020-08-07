# Further Hardening and De-Bloating my Android Setup

So I wrote a [post](/android.html) about my android setup quite a while back and since then I've made a lot of changes.

It all started when I upgraded my phone to Lineage OS 17.1 (based on Android 10) but this time I decided to not install `microG`.
So, i wouldn't be able to run applications that are heavily dependent on Google Play Services and I wouldn't be able to use network location as well.
I haven't faced any issues so far and my battery life has gone up as well.

<picture>
  <img src="/images/android_update.png" alt="android_update">
</picture>

Coming to the apps I use, the major change has been that I no longer have `Whatsapp` installed. As a replacement, I've been using `Signal` and it does the job well.
`Signal Desktop` is a little clunky but nothing too bad. Sadly, I do sometimes have to install `Whatsapp` for official reasons but it's still better than using it for personal reasons as well.
One complaint I have with `Signal` is that it's not available on `F-Droid`. So I would recommend you download the APK from their site rather than the Play Store.

For navigation I'm still using `Fluid NG` (with `AFWall+` to restrict internet access) because Android 10's default navigation gestures are crap.

I've also removed some apps like `Clover` and `KO Reader` because I wasn't using them all that often anyway.
I've also stopped using a dedicated Music Player App and use `mpv` with the `autoload.lua` for that purpose as well.

Other major change has been switching to `Posidon` as my launcher. It's completely Open Source and available on F-Droid. Lineage OS's default launcher has no customizability and I couldn't get a minimal look
using that. Not only does `Posidon` helps me in giving a more minimal look, it has other fancy options like app drawer blur and color, font, icon customizability.

Another thing I forgot to mention in my earlier post was about my password manager. I use `pass` as my password manager. It is just bash script around gpg so It can also be run on `Termux`.
I also have `rclone` installed on my `Termux` environment so I can sync my password store with my nextcloud instance as well.

---

Sources:

- `Signal`: <https://signal.org/download/>
- `Posidon`: <https://f-droid.org/en/packages/posidon.launcher/>

<br>
<center><i>
comments and questions can be left [here](https://github.com/mananapr/mananapr.github.io/issues)
</i></center>
