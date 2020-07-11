<center>
*Read the updated version [here](/curefit_update.html)*
</center>

```
Before I start with the main content, I would like to clear up a few things -

If you are a Curefit Employee,
- This article doesn't promotes piracy or distribution of your content. Anyone who has that kind of intent can just simply record their screens.
- I myself have never uploaded any of your videos nor do I plan to do so.
- I'm gonna mention some issues I have with your service, It would be great if you could try to work on them.

If you are a freeloader or a pirate -
- Don't bother mailing me to upload the videos somewhere, I'm not gonna reply.
- Curefit is not really an expensive service so consider paying for it.
```

# How I Use Curefit

Curefit is a subscription based service that provides follow along fitness and workout videos. The videos are really well made and of all the follow along videos I've tried,
I've liked them the best.

That being said, there are 2 major issues I have with the service -

- Even though you are paying for the service, you can't watch the videos at your convinience.
The sessions are streamed at fixed times and if you get a few minutes late, you can't seek back because it is being live streamed.

- The video streams are overlayed with distracting bars and numbers I don't care about. And there is no option to disable any of that.
On top of that if you forget to turn off your front camera you're gonna have to deal with annoying pop ups that cover the video each time you go out of frame.

So to deal with all of this I decided to find a way to store the live sessions locally so that I can watch them at any time.
Also, this would be saving the video in raw format without any of the UI overlays as you can see below -

<picture>
  <img src="/images/curefit2.png" alt="curefit - no overlays">
</picture>

I will be using Linux and Bash for this but I guess you can also use the Linux Subsystem in Windows.
Also keep in mind that this process should work on other live stream platforms as well (unless they are using some sort of DRM).

### Getting the Template Stream URL

So firstly, go to the website and start playing the session you would like to download.

Once it starts playing, open the developer console in your browser (<kbd>Ctrl</kbd> <kbd>Shift</kbd> <kbd>c</kbd> in Firefox).
<br>
Click on the `Network` tab and look for URLs that have a format like `index_1_XXX.ts?m=XXXXXXXXXX`, where *X* would be any number.
Click on that and find the `Request URL` like shown below -

<picture>
  <img src="/images/curefit.png" alt="curefit - stream request url">
</picture>

It is going to be different for each stream and will have a format like `https://blahblah.cloudfront.net/out/v1/blahblahblah/index_1_packetNumber.ts?m=XXXXXXXXXXX`.
This is going to act as the Template URL for the stream.

### Downloading all the Packets using the Template URL

As you can guess, incrementing the `packetNumber` in `index_1_packetNumber` will give us next part of the stream.
So we can just use a simple `for` loop in `bash` and download all the packets.

A few things I have noticed -

- Actual video starts between `packetNumber` 250 and 275

- The last packet number will depend on the length of the session. It can range between 600 and 850

- You will not be able to download a `packetNumber` if that part hasn't been streamed yet.
So, if you try to download packet number 600 at the begininng of the stream, you are going to get a 404 error

Keeping the above points in mind, use the following command to download the packets recursively -
```
for i in {270..710}; do wget -nc "https://d1rtdzwv5q8fnq.cloudfront.net/out/v1/36bf9406a019476bbd82e03366686125/index_1_$i.ts?m=1593102717"; done
```

Change the limits (270 and 710) and the template url accordingly.
<br>
You can open the inidividual packet files in your video player of choice and see if all the parts have been downloaded or not.
For example,

- If you open the file for packet `270` and you see that the session has already begun - decrease the lower limit accordingly. (Sometimes it can go as low as 230).

- Similarly, If you open the last packet and you see that the workout is still going on - increase the upper limit.

Once you have all the packets in one folder (make sure you have no other files in that folder) the output should look something like this -
```
-> ls
'index_1_270.ts?m=1593102717'  'index_1_287.ts?m=1593102717'  'index_1_304.ts?m=1593102717'  'index_1_321.ts?m=1593102717'  'index_1_338.ts?m=1593102717'  'index_1_355.ts?m=1593102717'
'index_1_271.ts?m=1593102717'  'index_1_288.ts?m=1593102717'  'index_1_305.ts?m=1593102717'  'index_1_322.ts?m=1593102717'  'index_1_339.ts?m=1593102717'  'index_1_356.ts?m=1593102717'
'index_1_272.ts?m=1593102717'  'index_1_289.ts?m=1593102717'  'index_1_306.ts?m=1593102717'  'index_1_323.ts?m=1593102717'  'index_1_340.ts?m=1593102717'  'index_1_357.ts?m=1593102717'
'index_1_273.ts?m=1593102717'  'index_1_290.ts?m=1593102717'  'index_1_307.ts?m=1593102717'  'index_1_324.ts?m=1593102717'  'index_1_341.ts?m=1593102717'  'index_1_358.ts?m=1593102717'
'index_1_274.ts?m=1593102717'  'index_1_291.ts?m=1593102717'  'index_1_308.ts?m=1593102717'  'index_1_325.ts?m=1593102717'  'index_1_342.ts?m=1593102717'  'index_1_359.ts?m=1593102717'
'index_1_275.ts?m=1593102717'  'index_1_292.ts?m=1593102717'  'index_1_309.ts?m=1593102717'  'index_1_326.ts?m=1593102717'  'index_1_343.ts?m=1593102717'  'index_1_360.ts?m=1593102717'
'index_1_276.ts?m=1593102717'  'index_1_293.ts?m=1593102717'  'index_1_310.ts?m=1593102717'  'index_1_327.ts?m=1593102717'  'index_1_344.ts?m=1593102717'  'index_1_361.ts?m=1593102717'
'index_1_277.ts?m=1593102717'  'index_1_294.ts?m=1593102717'  'index_1_311.ts?m=1593102717'  'index_1_328.ts?m=1593102717'  'index_1_345.ts?m=1593102717'  'index_1_362.ts?m=1593102717'
'index_1_278.ts?m=1593102717'  'index_1_295.ts?m=1593102717'  'index_1_312.ts?m=1593102717'  'index_1_329.ts?m=1593102717'  'index_1_346.ts?m=1593102717'  'index_1_363.ts?m=1593102717'
'index_1_279.ts?m=1593102717'  'index_1_296.ts?m=1593102717'  'index_1_313.ts?m=1593102717'  'index_1_330.ts?m=1593102717'  'index_1_347.ts?m=1593102717'  'index_1_364.ts?m=1593102717'
'index_1_280.ts?m=1593102717'  'index_1_297.ts?m=1593102717'  'index_1_314.ts?m=1593102717'  'index_1_331.ts?m=1593102717'  'index_1_348.ts?m=1593102717'  'index_1_365.ts?m=1593102717'
'index_1_281.ts?m=1593102717'  'index_1_298.ts?m=1593102717'  'index_1_315.ts?m=1593102717'  'index_1_332.ts?m=1593102717'  'index_1_349.ts?m=1593102717'  'index_1_366.ts?m=1593102717'
'index_1_282.ts?m=1593102717'  'index_1_299.ts?m=1593102717'  'index_1_316.ts?m=1593102717'  'index_1_333.ts?m=1593102717'  'index_1_350.ts?m=1593102717'  'index_1_367.ts?m=1593102717'
'index_1_283.ts?m=1593102717'  'index_1_300.ts?m=1593102717'  'index_1_317.ts?m=1593102717'  'index_1_334.ts?m=1593102717'  'index_1_351.ts?m=1593102717'  'index_1_368.ts?m=1593102717'
'index_1_284.ts?m=1593102717'  'index_1_301.ts?m=1593102717'  'index_1_318.ts?m=1593102717'  'index_1_335.ts?m=1593102717'  'index_1_352.ts?m=1593102717'
'index_1_285.ts?m=1593102717'  'index_1_302.ts?m=1593102717'  'index_1_319.ts?m=1593102717'  'index_1_336.ts?m=1593102717'  'index_1_353.ts?m=1593102717'
'index_1_286.ts?m=1593102717'  'index_1_303.ts?m=1593102717'  'index_1_320.ts?m=1593102717'  'index_1_337.ts?m=1593102717'  'index_1_354.ts?m=1593102717'
```

Ofcourse the number of files will be different in your case.

### Concatinating the files

You can use the `cat` command to join all the files together. As these files are `.ts` files we will have to use that extension.
```
cat * > session.ts
```

Now that we have the `ts` file, we can use `ffmpeg` to change the container to `mp4`.
<br>
If you are on windows, I will be linking windows binaries for `ffmpeg` at the bottom.
```
ffmpeg -i session.ts -acodec copy -vcodec copy session.mp4
```

All Done :)

<blockquote>
How many videos do you have downloaded?
</blockquote>

```
-> du -sh cure.fit/
38G     cure.fit/
-> find . -type f | wc -l
191
```
and counting...

---

Sources:

- `curefit`: <https://www.cure.fit>
- `ffmpeg`: <https://ffmpeg.zeranoe.com/builds/>
- `WSL`: <https://docs.microsoft.com/en-us/windows/wsl/install-win10>

<br>
<center><i>
comments and questions can be left [here](https://github.com/mananapr/blog/issues)
</i></center>
