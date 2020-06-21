# How to Consoom on the Internet

<picture>
  <img src="/images/consoomer.png" alt="consoomer">
</picture>

The internet has become rather inconvinient these days filled with ads, tracking, paywalls and what not.
So I thought I'd make some sort of a guide about how to *consoom* effectively on the modern web.

Luke Smith also did a video on RSS recently which I'll link in the sources. You should watch that as well.
Think of this post as more of a companion piece for that video.

## Part 1 - The Basics

In this part I would just be going over some of the basic things you should be doing while browsing the web.

Firstly, install `uBlock Origin` in your browser if you don't have it installed already. This is the least you can do.
All other Ad Blockers are crap and have relationships with some 3rd party advertisers and hence allow some ads to pass through.

If you are willing to put in some extra effort, set up dynamic filtering in uBlock as well. I'll link the wiki in the sources.
Using dynamic filtering, you can block 3rd party scripts and 3rd party frames but I also block first party scripts as well.
This will break a lot of websites but there are some workarounds you can try.
For example, I just use firefox's reader mode to get a readable and nicely formatted page whenever some website breaks on me.

You might also want to use a search engine that's not owned by your email provider. I use a searx instance (which I'll not disclose) which works perfectly.
Also consider using the Tor Browser for websites that don't require login if you want to improve your privacy.

## Part 2 - Dealing with Soical Media Crap

In this part I'll be going over some popular social media sites that just won't work without JavaScript and how you can get around that.

### Invidious

<picture>
  <img src="/images/invidious.png" alt="invidious">
</picture>

`Invidious` is a FOSS web application that acts as a proxy to YouTube and provides an alternative front-end that works without JavaScript.
You can even subscribe to channels without signing in to Google - how cool is that?

On top of that, you get extra features like Reddit Comments, Audio Only Mode and Video/Audio Downloads.

### Nitter

<picture>
  <img src="/images/nitter.png" alt="nitter">
</picture>

`Nitter` is a FOSS web application that provides a clean front-end for Twitter that works without JavaScript.
It even provides and option to get RSS Feeds for a user. Plus you don't have to deal with videos automatically playing as you scroll down the page.

### Bibliogram

<picture>
  <img src="/images/bibliogram.png" alt="bibliogram">
</picture>

Like `Invidious` is for Youtube and `Nitter` is for Twitter, `Bibliogram` is for Instagram and it's awesome!
You can just right click on any image and save it in it's original resolution without any hassle.
Most of the Bibliogram instances have been blocked by Instagram, so you'll have to use a userscript that unblocks it.
I personally use the `https://bibliogram.pussthecat.org` instance becuase it has dark mode on by default.

As anyone can selfhost an instance of these webapps, hidden services are also available which enables Tor Browser users to safely use these sites as well.

### Bringing it all together

Having to manually change the URLs each time is not practical. So you can install the `Privacy Redirect` extension available for Firefox and Chromium. This extensions will automatically redirect
these social media links to the alternative frontends mentioned above. It can also replace youtube embeds with invidious embeds and it also redirects google maps links to openstreetmaps links.
Plus, it can even be customized to redirect to particular instances of these webapps and in case of invidious, it also has an option to enable dark mode automatically.

While you're at it, also install the `Old Reddit Redirect` extension to save yourself from the cancer that is Reddit Redesign.

<blockquote>
    What If I mostly consoom content on my smartphone?
</blockquote>

If you are using Android, just install firefox (or a firefox fork like Icecat or Fennec) and install the `Privacy Redirect` extension on it.
As these are Progressive Webapps, you can save them in your app drawer as regular apps as well.

You don't need to worry about `Invidious` because you can install a FOSS app called `NewPipe` which provides a mobile friendly interface to `Invidious`.
On top of that, it adds things that are a part of Youtube Premium and it does all of that for free. It also has support for SoundCloud as well if you use that.
Even though `NewPipe` is available on F-Droid, I would recommend you download the APK from their Github Releases page (linked at the bottom) because that will receive instant updates.

If you don't want to install Firefox, you can install `UntrackMe` app from F-Droid. This will provide the same functionality and work irrespective of what browser you use.

## Part 3 - Spotify, Netflix and Other Similar Trash

I don't like any of these sites. I would actually use them had they not implemented DRM and other crap in their service.
Even though you are paying for it, you can't *consoom* it how you like. You are tied to their platform where they track you, profile you and sell that to advertisers.
Further, the quality they provides is meh (Except Amazon Prime I guess, Amazon WebDLs look pretty good).

I don't like BluRays either. They have amazing quality but they have other problems. Firstly, these discs are region locked. There are 3 Regions - A, B and C.
So, a BluRay player for Region A discs won't be able to play Region B discs or Region C discs. On top of that, some movies are only available in one region. So, yeah.
To make matters worse, these BluRay discs have a 10-15minute long **unskippable** section about Piracy and what not. So you need see that first each time you try to watch a movie.

Just to mention, there is a good bluray company called Criterion that sells region free BluRays and remasters some old films but ofcourse they don't have everything.

So lets talk about some alternatives -

### 1337x and The Holy Church of QxR

<picture>
  <img src="/images/1337x.png" alt="1337x">
</picture>

`1337x` is a torrent aggregator (just like the `The Pirate Bay`) which is officially used by an encoding group called `QxR`.

What's so great about `QxR` you ask? -

- Glorious HEVC Encodes
- They include Bluray Featurretes with their releases
- Encodes are not bloated and still look great

If `QxR` has a release for something you are looking just go with them. There's also another encoder called `Prof` (who also uploads on `1337x`) and his encodes are great as well.
(Although some of his encodes border on being bloated).

If you are looking for Anime, `Prof` does that as well but you might wanna head to `nyaa.si` and look for `CTR` or `VCB-Studio` releases.

### Rutracker - Cheeki Breeki Music Awesomeness

<picture>
  <img src="/images/rutracker.png" alt="rutracker">
</picture>

`Rutracker` is a russian torrent tracker that has **LOTS** of Music of all sorts. Most of it is high bitrate as well.
The site is mostly in russian so it can be a little hard to navigate if you are looking for something specific.

If you don't care about bitrate you can use Youtube as well I guess.

---

Sources:

- `Luke's Video`: <https://invidio.us/watch?v=hMH9w6pyzvU>
- `Invidious Instances`: <https://github.com/omarroth/invidious/wiki/Invidious-Instances>
- `Nitter Instances`: <https://github.com/zedeus/nitter/wiki/Instances>
- `Bibliogram Instances`: <https://github.com/cloudrac3r/bibliogram/wiki/Instances>
- `uBlock Origin Wiki`: <https://github.com/gorhill/uBlock/wiki/Dynamic-filtering:-quick-guide>
- `UntrackMe`: <https://f-droid.org/en/packages/app.fedilab.nitterizeme/>
- `NewPipe`: <https://github.com/TeamNewPipe/NewPipe/releases>
- `QxR`: <https://1337x.to/user/QxR/>
- `Prof`: <https://1337x.to/user/Prof/>
- `Rutracker`: <https://rutracker.org/forum/index.php>
