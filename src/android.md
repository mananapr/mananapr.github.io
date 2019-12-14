# Android Phone Setup

<picture>
  <img src="/images/android.png" alt="android">
</picture>

I have a Xiaomi Note 5 Pro with bootloader unlocked. Xiaomi phones have an exceptional
ROM support so finding a good ROM wasn't hard at all.

After unlocking the bootloader, I flashed the AOSP Extended Custom ROM that doesn't comes with Google Apps by default.
To enable root, I flashed Magisk.

I didn't flash GApps because I didn't want to run Google Botnet on my phone.
To replace Google Play Serivces, I installed `microG`.

`microG` provides FOSS APIs for Google Play Services so that apps that require Play Services can function
even if GApps are not installed. It also provides various location backends. I use the Mozilla backend and it works fine most of the times.

To download and keep my APKs up to date, I use `Aurora Store`. It acts as a proxy to Google Play Store, so I can download apps
from the Play Store without having to login. If you want to download paid apps, It also provides an option to login using your
google account.
I also use `F-Droid` to download FOSS apps. Most of the apps on my phone are FOSS and downloaded from `F-Droid`.

For booking cabs, Uber and Ola's web apps are good enough.

I still haven't found a good replacement for Google Maps but `maps.me` comes close. It uses OpenStreetMaps for the Map Data
but the app itself is partially proprietary. Therefore, I have downloaded the maps for offline use and disabled the app's
internet access using `AFWall+`. A lot of places are not available in the Map, so I use the web app of Google Maps
in that case. Once I have the co-ordinates of the required location from GMaps webapp, I plug those in `maps.me`.

To replace GMail, I use `K-9 Mail`. It may not look great, but it works and has a dark theme, so that's good enough for me.

`NewPipe` is an excellent application for YouTube. Not only is it FOSS, it has all the features of YouTube Pro like background mode
and popup mode. It does not uses YouTube's APIs and instead uses web scraping and `youtube-dl`.
Also, it doesn't requires users to sign in to subscribe to channels, which is really cool.

Apart from the apps listed above, I also have the following apps installed:

 - **Fennec F Droid** (Firefox with Telemetry Disabled) [F-Droid App]

 - **Fluid NG** (To hide the navbar)

 - **KO Reader** (EBook Reader) [F-Droid App]

 - **Clover** (Browsing Imageboards) [F-Droid App]

 - **LibreOffice** (Office) [F-Droid App]

 - **LibreTorrent** (Torrent Client) [F-Droid App]

 - **mpv** (Video Player) [FOSS. APK Available on Github]

 - **Open Camera** (Camera App) [F-Droid App]

 - **Orgzly** (Notes) [F-Droid App]

 - **QKSMS** (Messaging) [F-Droid App]

 - **SecScanQR** (QR Code Scanner/Generator) [F-Droid App]

 - **Termux** (Linux Environment) [F-Droid App]

 - **Vinyl** (Music Player) [F-Droid App]

 - **WhatsApp** (Instant Messaging) [Proprietary App]

These are all the apps I have.

Of all the apps mentioned above, I would really like to get rid of WhatsApp
because it is proprietary and invades people's privacy. It saddens me that even though
a lot of alternatives are available with even some being better than WhatsApp,
people still use it.

Overall, I am pretty happy with my current setup because it's minimal and I don't have google play services
but `microG` is a little buggy. For example, some apps that require location, sometimes crash the whole System UI that
leaves the phone unresponsive for like a minute. This is super annoying to be honest and hope this gets fixed soon.

To further remove Google from my life, I plan to buy a VPS and setup NextCloud on it. This
would allow me to sync Contacts, Calendar, Notes etc without any proprietary software like Google Drive.
NextCloud also has apps for Office, so it can replace GDocs as well.

I am also thinking of hosting my own email server. This may take some time, as I've read a lot online
about how difficult it can be to manage a self hosted email server. But once setup, I will become 100% Google free
and it would be nice to self host most of the things I use because there will be no third party involved. 

---

Sources:

- `microG`: <https://microg.org/>
- `FDroid`: <https://f-droid.org/en/>
- `nextcloud`: <https://nextcloud.com/>
