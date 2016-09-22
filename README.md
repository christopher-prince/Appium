# Appium

These are just my observations about [Appium](http://appium.io). So, if I need to come back to this, I can reload my brain :). And maybe they can prove useful to someone else. These note are primarily from the perspective of iOS development, since that's what I focus on. Also, I'm doing my testing on a Mac.

## General characteristics

1. You can test on a release build. i.e., on an .ipa that, if tests are successful, can actually be submitted to the app store. To my understanding, you *cannot* do this with the UI Testing framework provided by Apple (see, [ref1](https://forums.developer.apple.com/thread/29609) and [ref2](http://stackoverflow.com/questions/34623029/is-there-a-way-to-run-xctestui-against-an-archived-build-ipa) for example). 
1. Uses a standard automation protocol (Web Driver) and various languages have libraries for that protocol (e.g., JavaScript, Python) so you can write your tests in various languages. It sounds like you can do this in [Objective-C](https://github.com/appium/selenium-objective-c) too, but I haven't tried this yet.
1. Capable of cross-platform (e.g., iOS and Android) testing. So, if you have two versions of an app, one for iOS and one for Android doing the same job, that are quite similar with respect to their UI (and I'm not sure exactly how similar they need to be), you may be able to use the same tests. Personally I suspect there may have to be some conditional characteristics to the tests (ie., some parts that differ across iOS and Android), but this still might amount to considerable avoidance of duplication of tests and effort.

## Efforts with Appium

1. GUI Appium. A GUI-based app for Appium is available (via the download link on [http://appium.io](http://appium.io) and [you can select a version here](https://bitbucket.org/appium/appium.app/downloads/)). I downloaded version 1.5.3 and 1.5.2 and had zero luck with this. I get the problem described [here](https://discuss.appium.io/t/cannot-start-appium-server-and-launch-inspector-after-upgrading-to-1-5-2/10098/18).

1. I looked at the [documentation here](http://appium.io/slate/en/master/?ruby#about-appium) and I suspect it would be useful as a reference but didn't help me much initially.

1. Running apps on Apple mobile devices. What I did was this:
	
	`appium -U <snip--Put the UDID of your device here> --app <Put the .ipa path of your app here>`
	
	e.g., I used "/Users/chris.prince/Desktop/Greenpoint 2016-09-21 17-27-24/Apps/Greenpoint-iPhone 6.ipa" for my .ipa
	
	This starts the server, apparently connected to the device. At this point I didn't know what to do further. I then went ahead with the step below. I think what's needed is to actually run a client that performs the tests on that specific app. Like what takes place in the following. 

1. Running apps on the iOS simulator. My next main effort worked, but I had to figure out many of the steps. I wanted to get [these examples](https://github.com/appium/sample-code) running. 

  1. The following assumes you have Xcode installed. I'm using Xcode 7.3.1.
  1. You need to have [brew](http://brew.sh) installed. 
  1. You need to do the first two installs mentioned at the bottom of the [http://appium.io](http://appium.io) page. At a Mac terminal window, type:
  
  	`brew install node`  
  	`npm install -g appium`  
  	
  1. I'm not 100% sure this is necessary, but perhaps it is. At the terminal window:
  
  	`sudo authorize-ios`
  	
  1. Start the Appium server. This will remain running in the terminal window you use:
  
  	`appium`
  	
  1. Download [the examples from](https://github.com/appium/sample-code)
  	
  1. I ran the Node.js examples. So the rest of these directions assume that. The following directions are taken partly from `sample-code/sample-code/examples/node/README.md`.
  
  1. Open a terminal window at `sample-code/sample-code/examples/node`
  	
  1. Install the npm packages in `package.json`:
  
  	`npm install`
  	
  1. You now will likely need to edit some files to get the Node.js tests to run. The file `sample-code/examples/node/helpers/caps.js` has some definitions about specific iOS Simulator devices. For example, when I downloaded the examples, the `caps.js` file included this definition:  
```javascript
		exports.ios92 = {
		  browserName: '',
		  'appium-version': '1.3',
		  platformName: 'iOS',
		  platformVersion: '9.2',
		  deviceName: 'iPhone 5s',
		  app: undefined // will be set later
		};
```


However, I wanted to use iOS9.3 simulators, so I added the following definition to that file:


```javascript	
		exports.ios93 = {
		  browserName: '',
		  'appium-version': '1.3',
		  platformName: 'iOS',
		  platformVersion: '9.3',
		  deviceName: 'iPhone 5s',
		  app: undefined // will be set later
		};
```
  	
  1. If you added definitions to caps.js, you'll want use these definitions in the test(s) you want to run. For example, in `ios-simple.js`, the relevant line originally looked like:
  
  	 `var desired = _.clone(require("./helpers/caps").ios92);`
  	 
  	 and I changed that to:
  	 
  	 `var desired = _.clone(require("./helpers/caps").ios93);`
  	 
  1. Now we can actually run the tests:
  
  	`npm run ios-simple.js`
  	
  1. Note that the file `sample-code/sample-code/examples/node/README.md` indicates which tests you can run. (I'm getting errors when I run `ios-complex.js`-- I assume those just haven't been updated in a while).