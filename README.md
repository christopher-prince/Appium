# Appium

These are just my observations about [Appium](http://appium.io). So, if I need to come back to this, I can reload my brain :). And maybe they can prove useful to someone else. These note are primarily from the perspective of iOS development, since that what I focus on.

## General characteristics

1. You can test on a release build. i.e., on an .ipa that, if tests are successful, can actually be submitted to the app store. To my understanding, you *cannot* do this with the UI Testing framework provided by Apple (see, [ref1](https://forums.developer.apple.com/thread/29609) and [ref2](http://stackoverflow.com/questions/34623029/is-there-a-way-to-run-xctestui-against-an-archived-build-ipa) for example). 
1. Uses a standard automation protocol (Web Driver) and various languages have libraries for that protocol (e.g., JavaScript, Python) so you can write your tests in various languages. It sounds like you can do this in [Objective-C](https://github.com/appium/selenium-objective-c) too, but I haven't tried this yet.
1. Capable of cross-platform (e.g., iOS and Android) testing. So, if you have two versions of an app, one for iOS and one for Android doing the same job, that are quite similar with respect to their UI (and I'm not sure exactly how similar they need to be), you may be able to use the same tests. Personally I suspect there may have to be some conditional characteristics to the tests, but this might amount to considerable avoidance of duplication of tests and effort.

## Attempts to use Appium
