# Appium

These are just my observations about [Appium](http://appium.io). So, if I need to come back to this, I can reload my brain :). And maybe they can prove useful to someone else. These note are primarily from the perspective of iOS development, since that's what I focus on. Also, I'm doing my testing on a Mac.

## General characteristics

1. You can test on a release build. i.e., on an .ipa that, if tests are successful, can actually be submitted to the app store. To my understanding, you *cannot* do this with the UI Testing framework provided by Apple (see, [ref1](https://forums.developer.apple.com/thread/29609) and [ref2](http://stackoverflow.com/questions/34623029/is-there-a-way-to-run-xctestui-against-an-archived-build-ipa) for example). 
1. Uses a standard automation protocol (Web Driver) and various languages have libraries for that protocol (e.g., JavaScript, Python) so you can write your tests in various languages. It sounds like you can do this in [Objective-C](https://github.com/appium/selenium-objective-c) too, but I haven't tried this yet.
1. Capable of cross-platform (e.g., iOS and Android) testing. So, if you have two versions of an app, one for iOS and one for Android doing the same job, that are quite similar with respect to their UI (and I'm not sure exactly how similar they need to be), you may be able to use the same tests. Personally I suspect there may have to be some conditional characteristics to the tests (ie., some parts that differ across iOS and Android), but this still might amount to considerable avoidance of duplication of tests and effort.

## Attempts to use Appium

1. GUI Appium. A GUI-based app for Appium is available (via the download link on [http://appium.io](http://appium.io) and [you can select a version here](https://bitbucket.org/appium/appium.app/downloads/)). I downloaded version 1.5.3 and 1.5.2 and had zero luck with this. I get the problem described [here](https://discuss.appium.io/t/cannot-start-appium-server-and-launch-inspector-after-upgrading-to-1-5-2/10098/18).

1. Examples. My next main effort worked, but I had to figure out many of the steps. I wanted to get [these examples](https://github.com/appium/sample-code) running. 

  1. You need to the basic installs mentioned at the bottom of the [http://appium.io](http://appium.io) page. At a Mac terminal window, type:
  
  	`brew install node`
  	`npm install -g appium`
  	
  	
  	
