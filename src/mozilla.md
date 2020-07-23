# Mozilla, Get your act together

I have a love-hate relationship with Mozilla. I've been using Firefox since the Pre-Quantum days and even though it has never been perfect, Mozilla has always made effort to improve their product.
<br>
I believe it's an important war Mozilla is fighting against Chromium's browser monopoly but sadly, it seems to me that Mozilla has changed it's priorities - They no longer care about user experience,
code quality and personalization. Instead, they have prioritised fighting for social justice.
<br>
And it's not just Mozilla, a lot of open source projects (including Linux itself) have been forced to incorporate various "Code of Conducts". It's just that Mozilla is the only one I feel
that has been negatively affected.

<picture>
  <img src="/images/code_of_conduct.png" alt="code of conduct meme">
</picture>

### Firefox is not a Privacy Browser

At least out of the box it isn't. Users need to mess around in `about:config` to enable various privacy and security tweaks. Not to mention it comes pre-installed with a bunch of proprietary bloat like
Pocket. Yes, you can save these settings in the `user.js` file but even that is not foolproof - Firefox keeps changing or sometimes completely removes options from `about:config`. This can break your
Firefox installation, something that has happened with me once.

Mozilla has also made privacy related blunders in the past - like when they used Google Analytics on Firefox's homepage, or when they automatically installed an add-on without the user's permission
to promote the TV show *Mr Robot*. Oh and how can we forget that one time when they forgot to renew their SSL Certificates - something that broke add-ons and extensions even on the Tor Browser.

At this point, I would recommend something like *Ungoogled Chromium*<sup>[1]</sup> or *Brave*<sup>[2]</sup> to normies because they would have a much more pleasant time using those. These browsers also
provide better privacy than Firefox out of the box. Although a hardened Firefox is much better than these browsers, at that point you might as well just use *Tor Browser*<sup>[3]</sup>.

If you are still interested in hardening your Firefox installation, I would recommend starting with the *ghacks-user.js*<sup>[4]</sup> as a template.

### Decline in Code Quality

Although Quantum is a much better engine than the earlier Gecko engine it's still not perfect. There's no doubt in my mind that Chromium provides a much more smoother web experience.
Also media playback on websites like *invidio.us* has always worked for me on chromium based browsers. On Firefox, a lot of videos either stop playing midway or just refuse to load at all.

Mozilla has stopped improving the main backend. They just keep on adding stupid "features" that no one wants and making visual changes that break the user's workflow.

I have tried switching to various other Firefox forks like *IceCat* whenever Firefox broke on me but I've also come back to Firefox because the forks are not properly maintained and don't receive updates
regularly. Most of them are based on the ESR version, which means that they would getting the same changes the latest version has - just after 6 months. So It's not a long term solution.

On my phone, I've already switched to *Bromite*<sup>[5]</sup> - which is like Ungoogled Chromium for Android and who knows, I might switch to a Chromium based browser on my desktop as well.

---

Sources:

- `[1]`: <https://ungoogled-software.github.io/>
- `[2]`: <https://brave.com/>
- `[3]`: <https://www.torproject.org/>
- `[4]`: <https://github.com/ghacksuserjs/ghacks-user.js/>
- `[5]`: <https://www.bromite.org/>

<br>
<center><i>
comments and questions can be left [here](https://github.com/mananapr/blog/issues)
</i></center>
