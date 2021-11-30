# HTML-Elements moving with position=fixed when scrolling

## Summary
An footer element with the CSS properties `position=fixed` and `bottom=0` will get scrolled up and hides the content behind it. This happens if you used the keyboard and rotate your device from landscape to portrait. That's a problem because it's hard to reach the content hidden by the footer. It seems to be an bug in webkit with installed App's on mobile devices.

## Steps to reproduce
1. Install a PWA with a position-fixed footer to your home screen (example: https://dstester.github.io/ElementsMovingWithFixedPosition)
2. Rotate the device to landscape
3. Open the app
4. Open the keyboard by focusing an input
5. Close the keyboard
6. Rotate the device to portrait
7. Scroll up
8. The footer gets scrolled with the content and hides it

## Description
May be connected to this webkit bugs:
* https://bugs.webkit.org/show_bug.cgi?id=218465
* https://bugs.webkit.org/show_bug.cgi?id=218983

It seems to be connected to the value of visualViewport.height. After the keyboard usage and rotation the value is to low.
On my iPad the value should change from 717 to 1282 on rotation, but it changes to 980.
Also the value of visualViewport.pageTop only changes after the touchend event. Usualy the value gets updated immediately on scrolling.
Once you opened the keyboard in portrait the problem disappears. The height gets the right value and the pageTop gets updated immediately again.
This does not happen in Safari.
At first it seemed to no big deal. Who rotates the ipad in that specific order after keyboard usage, right? But after we got in production with our new App, the first 5 User we started with, reported all this bug in the first two week. So i guess it is a only an annoying problem, but a real problem.
You can see the demo in the attached short video (Also on Github: https://github.com/DSTester/ElementsMovingWithFixedPosition/raw/main/ExampleVideo.mp4).

Simple sourcecode to reproduce this problem can be found on github: https://github.com/DSTester/ElementsMovingWithFixedPosition

I don't know how to test this with the latest webkit build and the iOS-Simulator. So for now i report this as described and will add information as i got familiar with build webkit, Xcode and the iOS-Simulator.

## Tested with
* iPad 8.Gen, MYMH2FD/A, iPadOS 15.1 => happens
* iPad Air, MD791FD/A, iOS 12.5.5 => happens
* iPhone SE, MP822DN/A, iOS 15.1 => happens
* iPad Air 4, iOS 15.2 Beta 3 (19C5044b) => happens
* iOS-Simulator, iPad 9. Gen., iOS 15.0
* some other devices i have no detailed data at this moment => happens
