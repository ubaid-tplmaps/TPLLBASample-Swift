
## Getting Started
Before you can begin working with TPLLBA on iOS, you need to download the TPLLBA SDK for iOS.

### Step 1: Get the latest version of Xcode
To build a project using the TPLLBA SDK for iOS, you need **version 9.0** or later of [Xcode](https://developer.apple.com/xcode/). 

### Step 2: Install the SDK


TPLLBA SDK for iOS is available as a CocoaPods pod. CocoaPods is an open source dependency manager for Swift and Objective-C Cocoa projects.

If you don't already have the CocoaPods tool, install it on macOS by running the following command from the terminal. For details, see the [CocoaPods Getting Started guide](https://guides.cocoapods.org/using/getting-started.html).

> sudo gem install cocoapods

Create a `Podfile` for the TPLLBA SDK for iOS and use it to install the API and its dependencies:

1. If you don't have an Xcode project yet, create one now and save it to your local machine. (If you're new to iOS development, create a Single View Application.)

2. Create a file named `Podfile` in your project directory. This file defines your project's dependencies. 

3. Edit the `Podfile` and add your dependencies. Here is an example which includes the dependencies you need for the TPLLBA SDK for iOS:

```ruby
source 'https://github.com/CocoaPods/Specs.git'
platform :ios, '9.0'

target 'YOUR_APPLICATION_TARGET_NAME_HERE' do
pod 'TPLLBA'
end
```

4. Save the `Podfile`

5. Open a terminal and go to the directory containing the `Podfile`:
```ruby
cd <path-to-project>
```

6. Run the `pod install` command. This will install the APIs specified in the `Podfile`, along with any dependencies they may have.

7. Close Xcode, and then open (double-click) your project's `.xcworkspace` file to launch Xcode. From this time onwards, you must use the `.xcworkspace` file to open the project.

### Step 3: Implementation

The code below demonstrates how to start engine of TPLLBA in application.

Now, Update a few methods inside your app's `AppDelegate` class.

```Swift

    func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool {

        // Override point for customization after application launch.

        LBAds.shared().initializeAdsWithAppId("APP_ID")

        return true
    }

```

#### Set APNS Token to send the push notifications

```Swift

    func application(_ application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: Data) {

        // Convert token to string
        let deviceTokenString = deviceToken.reduce("", {$0 + String(format: "%02X", $1)})
        LBAds.shared().setAPNSToken(deviceTokenString)

    }

```

#### Stop background service
```Swift

    func applicationDidEnterBackground(_ application: UIApplication) {
        LBAds.shared().applicationDidEnterBackground()
    }

```
#### Start service on application becomes active
```Swift
    
    func applicationDidBecomeActive(_ application: UIApplication) {
        LBAds.shared().applicationWillEnterForeground()
    }
    
```

#### Below iOS 10 support

Add following code to show the ads notifications

```Swift

    func application(_ application: UIApplication, didReceive notification: UILocalNotification) {
        LBAds.shared().notificationTapped(notification)
    }

```

### Important notes

Following settings are required for propely working sdk

1. App Transport Security Settings : Allow Arbitrary Loads : YES
2. Privacy - Location Always Usage Description : [Message to Display User]
3. Privacy - Location Always and When In Use Usage Description : [Message to Display User]
4. Privacy - Location When In Use Usage Description : [Message to Display User]

In Capabilities:
1. Enable Background Modes for Location Updates and Background Fetch
2. Turn On Remote Notifications

##### For Objective-C : Goto Build Settings -> Always Embed Swift Standard Libraries = YES


