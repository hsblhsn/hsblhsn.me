---
title: "Fix crackling sound after opening Xcode Simulator."
datePublished: Sat Jun 26 2021 13:31:57 GMT+0000 (Coordinated Universal Time)
cuid: ckqdsyes20d6vd6s1dvgfdog8
slug: fix-crackling-sound-after-opening-xcode-simulator
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1624714227619/8KGcj2gAv.png
tags: xcode, ios, bugs-and-errors, macos

---

While developing apps for iOS, you may face an issue with your main speakers. It makes weird crackling noises. Well, most probably the simulator is also using your main speaker as the output. This issue can be fixed by using another speaker device and using that device as the output device of your simulator. So your mac's output stays intact and the simulator's output too.


![change output device - https://discussions.apple.com/thread/251814420](https://cdn.hashnode.com/res/hashnode/image/upload/v1624713132075/aWA0x5DQ6.png)

But, if you do not have a secondary speaker, you can use a virtual audio driver to fix the noise issue.


Welcome to  [BlackHole](https://github.com/ExistentialAudio/BlackHole).

> BlackHole is a modern MacOS virtual audio driver that allows applications to pass audio to other applications with zero additional latency.

#### Install BlackHole

You can follow the [manual way](https://github.com/ExistentialAudio/BlackHole#option-1-download-installer)  of installing the package.
Or, if you have Homebrew installed, just run: 

```sh
brew install blackhole-2ch
```

After completing the installation, Open your Xcode simulator. On the menu bar, go to **I/O** > **Audio Output** > **BlackHole 2ch**

![visual instruction of selecting BlackHole 2ch as audio driver.](https://cdn.hashnode.com/res/hashnode/image/upload/v1624713593881/lbgPPzSl9.png)

**NOTE:** If you use `BlackHole` as your audio driver, you won't be able to hear any audio from your simulator. In most of the case you might not need the audio from the simulator. If you need the audio, I highly recommend you to use external speaker devices to use as the audio output of your simulator.


Thank you for reading, here is a potato.

![lukasz-rawa-QHWxPcrpBB0-unsplash-2.jpg](https://cdn.hashnode.com/res/hashnode/image/upload/v1624714099010/XLwDAcKYJ.jpeg)
