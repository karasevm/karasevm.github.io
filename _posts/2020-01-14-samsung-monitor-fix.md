---
layout: post
title: How to fix washed out colors on Samsung UHD monitors
lang: en
pageid: samsung-monitor
---
Ever since I purchased my U28D590 monitor I had the same issue: washed out colors while using 1080p. As this is a somewhat common problem for NVIDIA, I found the usual solution which was changing the `Output dynamic range` option in NVIDIA Control Panel. But when I opened the resolution setting, the option was not there, probably because the monitor was connected via DisplayPort. This particular model does not support 4k@60hz via HDMI as it does not support HDMI 2.0 so connecting via HDMI was not an option. 

At the time I gave up, at 1440p the colors were displaying correctly and, most of the time, 1440p satisfied me when I requiered a lower resolution for any reason.

### The solution

Around a month ago I had to use Custom Resolution Utility for some unrelated stuff, thats when I noticed that the Samsung monitor was not listing the 1080p resolution as a monitor but rather as a TV. After digging around in NVIDIA Control Panel once again I finally found the solution:

1. Open the resolution settings in NVIDIA Control Panel
2. Change the monitor resolution to 1080p
3. Click `Apply`
4. (Skip if `Output dynamic range` option is active) Reboot your computer with the monitor resolution set to 1080p and open the control panel again
5. Change the `Output dynamic range` to full
6. Change the resolution back to the native 2160p

For me the important thing was the reboot after changing the resolution as that was the only thing that activated the `Output dynamic range` option on my machine.