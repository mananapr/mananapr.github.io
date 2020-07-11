# Downloading from Curefit - An Update

<center>
*I strongly recommend going through the [earlier guide](/curefit.html) before proceeding further*
</center>

Curefit has updated their backend which alters the way they are serving their live streams.
<br>
Their older videos are still being served the old way, but in order to download their newer videos we're going to have to put in some extra effort.

The major change they've made is that you need to be authenticated to access the stream url. So, a simple `wget <url>` won't work this time.
<br>
As you can see in the image below, the base stream URL has also changed -

<picture>
  <img src="/images/curefit_update.png" alt="curefit - updated stream URL">
</picture>

### Understanding the Template URL

Like last time, we need to open the developer console during the stream to get the template URL.
<br>
In their newer videos, you're going to notice that this time they have two streams - `index1280x720_00XXX.ts` and the other would be for lower res.
<br>
Also the host URL is no more *cloudfront* - they have shifted to *live-vod.cure.fit*.

So, the template URL is going to be something like this - `https://live-vod.cure.fit/blahblahblah/hls/index1280x720_00XXX.ts`, where `XXX` would be the packet number.

### Downloading all the Packets using the Template URL

Firstly, lets start with some good news - we don't have to guess the packet number range like last time. In their newer streams, the session starts at packet number `001`.
For the last packet, use a large number like 700. We will start getting *403 Forbidden* errors after we cross the last packet number.

Another good news - we can download packet numbers even if they haven't been streamed yet. So no need to wait!

Now the bad news is - Unlike last time, We can't just loop over `XXX` and get all the packets. So we're going to need cookies for our curefit session.
<br>
For this, I'm gonna be using the *Export Cookies* extension for Firefox which I'll link at the bottom. It's open source, So I would recommend you use that as well.

So open the stream you want to download, then click on the *Export Cookies* extension and download cookies for all the domains. The extension will save them in `cookies.txt` in your Downloads folder.

Now, we just have to tell wget to use those cookies -
```
for i in {001..755}; do wget -U 'Mozilla/5.0 (X11; Linux x86_64; rv:30.0) Gecko/20100101 Firefox/30.0' --load-cookies=/home/username/Downloads/cookies.txt -nc "https://live-vod.cure.fit/2d2c96bc-e7a9-405b-9d22-e7f9cf13bd2c/hls/index1280x720_00$i.ts"; done
```

### Concatinating the files

This is same as last time -
```
cat * > session.ts
ffmpeg -i session.ts -acodec copy -vcodec copy session.mp4
```

All Done :)

---

Sources:

- `export cookies`: <https://addons.mozilla.org/en-US/firefox/addon/export-cookies-txt/>

<br>
<center><i>
comments and questions can be left [here](https://github.com/mananapr/blog/issues)
</i></center>
