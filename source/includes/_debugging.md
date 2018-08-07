# Troubleshooting

In this section, we’ll take a look at a general debugging checklist that can help you identify the actual issue that you’re having.

## Failing build on react-native run-windows
Error
```
Build failed with message Error: Command failed: "C:\Program Files (x86)\MSBuild\14.0\bin\msbuild.exe" 
"C:/<path_to_project>/windows/<project_name>.sln" /clp:NoSummary;NoItemAndProperty;Verbosity=minimal /nologo
/p:Configuration=debug /p:Platform=x86
. Check your build configuration.
```

Solution
This error is likely caused by missing libraries on your machine. To fix this, open the solutions file, C:\<path_to_project>\windows\<project_name>.sln, in Visual Studio. You will be prompted to install the missing libraries. Install the preselected libraries and restart visual studio.

Error
Failed to restore the NuGet packages

Solution
This usually happens when you don't have Visual Studio installed. Install Visual Studio as listed in the Requirements, and try again.

Error
Build failed with message Error: Must have a minimum Windows SDK version 10.0.10586.0

Solution
This is exactly as it says, you need to install the Windows 10 SDK version >= 10.0.10586.x. Note that the latest Windows 10 SDK requires Visual Studio 2017, which React Native Windows doesn't support quite yet. Install Windows 10 SDK version 10.0.14393.x as listed in the Requirements, and try again.

Error
```
ERROR: The system was unable to find the specified registry key or value.

Build failed with message Error: Command failed: "C:\Program Files\MSBuild\14.0\
bin\msbuild.exe" "C:/Users/IEUser/v41/windows/v41.sln" /clp:NoSummary;NoItemAndP
ropertyList;Verbosity=minimal /nologo /p:Configuration=Debug /p:Platform=x86 /p:
AppxBundle=Never
. Check your build configuration.
```
or
```
error APPX0002: Task 'GenerateAppxPackageRecipe' failed. 0x7F - Failed to load MRM support library.
```
Solution
Re-run the standalone installer for Windows 10 SDK version 10.0.14393.x as listed in the Requirements. It appears that sometimes a partial install occurs when the SDK is installed via the Visual Studio installer.

Error
(After trying to run the project)
```The project '___' cannot be started directly. In order to debug this project, you must consume it from an application project that creates a package and is marked as the startup project ```

Solution
Right click your react-native-windows project name (i.e. AwesomeProject) and select "Set as StartUp Project"

Error
(After trying to 'install missing features' on ReactNativeWebViewBridge when it is unavailable)
```Object reference not set to an instance of an object```
Solution
Install the 10.0.14393.0 Windows 10 SDK in the Visual Studio Installer

## Error initializing project
Error "react-native is not recognized as an internal or external command" while initializing a project
Solution Check environment variables. add npm path to global path config. 


## Port already in use
The React Native packager runs on port 8081. If another process is already using that port, you can either terminate that process, or change the port that the packager uses.

Terminating a process on port 8081
Run the following command to find the id for the process that is listening on port 8081:
```
$ sudo lsof -i :8081
```
Then run the following to terminate the process:
```
$ kill -9 <PID>
```
On Windows you can find the process using port 8081 using Resource Monitor and stop it using Task Manager.
  
Using a port other than 8081
You can configure the packager to use a port other than 8081 by using the port parameter:
```
$ react-native start --port=8088
```

You will also need to update your applications to load the JavaScript bundle from the new port. If running on device from Xcode, you can do this by updating occurrences of 8081 to your chosen port in the node_modules/react-native/React/React.xcodeproj/project.pbxproj file.

## NPM locking error
If you encounter an error such as npm WARN locking Error: EACCES while using the React Native CLI, try running the following:
```
sudo chown -R $USER ~/.npm
sudo chown -R $USER /usr/local/lib/node_modules
```

## Missing libraries for React

If you added React Native manually to your project, make sure you have included all the relevant dependencies that you are using, like RCTText.xcodeproj, RCTImage.xcodeproj. Next, the binaries built by these dependencies have to be linked to your app binary. Use the Linked Frameworks and Binaries section in the Xcode project settings. More detailed steps are here: Linking Libraries.

If you are using CocoaPods, verify that you have added React along with the subspecs to the Podfile. For example, if you were using the <Text />, <Image /> and fetch() APIs, you would need to add these in your Podfile:

```
pod 'React', :path => '../node_modules/react-native', :subspecs => [
  'RCTText',
  'RCTImage',
  'RCTNetwork',
  'RCTWebSocket',
]
```

Next, make sure you have run pod install and that a Pods/ directory has been created in your project with React installed. CocoaPods will instruct you to use the generated .xcworkspace file henceforth to be able to use these installed dependencies.

React Native does not compile when being used as a CocoaPod
There is a CocoaPods plugin called cocoapods-fix-react-native which handles any potential post-fixing of the source code due to differences when using a dependency manager.

Argument list too long: recursive header expansion failed
In the project's build settings, User Search Header Paths and Header Search Paths are two configs that specify where Xcode should look for #import header files specified in the code. For Pods, CocoaPods uses a default array of specific folders to look in. Verify that this particular config is not overwritten, and that none of the folders configured are too large. If one of the folders is a large folder, Xcode will attempt to recursively search the entire directory and throw above error at some point.

To revert the User Search Header Paths and Header Search Paths build settings to their defaults set by CocoaPods - select the entry in the Build Settings panel, and hit delete. It will remove the custom override and return to the CocoaPod defaults.

## No transports available

React Native implements a polyfill for WebSockets. These polyfills are initialized as part of the react-native module that you include in your application through import React from 'react'. If you load another module that requires WebSockets, such as Firebase, be sure to load/require it after react-native:
``` 
import React from 'react';
import Firebase from 'firebase';
```

## Shell Command Unresponsive Exception

If you encounter a ShellCommandUnresponsiveException exception such as:

``` 
Execution failed for task ':app:installDebug'.
  com.android.builder.testing.api.DeviceException: com.android.ddmlib.ShellCommandUnresponsiveException
  
  ```
  
Try downgrading your Gradle version to 1.2.3 in android/build.gradle.

## react-native init hangs

If you run into issues where running react-native init hangs in your system, try running it again in verbose mode and refering to #2797 for common causes:
```
react-native init --verbose
```
## Unable to start react-native package manager (on Linux
Case 1: Error "code":"ENOSPC","errno":"ENOSPC"
Issue caused by the number of directories inotify (used by watchman on Linux) can monitor. To solve it, just run this command in your terminal window

```
echo fs.inotify.max_user_watches=582222 | sudo tee -a /etc/sysctl.conf && sudo sysctl -p
```

## react-native known issues

https://www.decoide.org/react-native/docs/known-issues.html

## Could not connect to MongoDB on the provided host and port

Execute mongod command and start mongodb.

C:\Program Files\MongoDB\Server\3.6\bin>mongod --dbpath "C:\Program Files\MongoDB\data\db" 
(or)
C:\Program Files\MongoDB\Server\3.6\bin>mongod --dbpath "C:\Program Files\MongoDB\data\db" --logpath "C:\Program Files\MongoDB\log\mongo.log" --logappend --rest --install

C:\Program Files\MongoDB\Server\3.6\bin>net start MongoDB

C:\Program Files\MongoDB\Server\3.6\bin>Mongo

## native module error

If you’re trying to get a native module to work, and you’ve followed the install instructions to the letter. But still it wouldn’t work, the solution may be to clear out your node_modules and re-install all the packages:

``
 rm -r node_modules
 npm install
 ``
 After that, execute the following:
 ``
 cd android
 ./gradlew clean
``
This will delete the build directory and make sure that no previous code or resources are still being cached.

You may even go one step further by clearing out the Gradle’s dependency cache:
``
./gradlew build --refresh-dependencies
``
Once that’s done, go back to your project’s root directory and execute react-native run-android like usual.

## Android path not added to the environment

The first time you build your Android app after setting up your computer for React Native development, you might encounter an issue similar to the following:

``
FAILURE: Build failed with an exception.

    * What went wrong:
    A problem occurred configuring project ':app'.
    > SDK location not found. Define location with sdk.dir in the local.properties file or with an ANDROID_HOME environment variable.
``
This happens when you haven’t properly configured your environment variables to use the path where Android is installed. React Native requires this if you’re running the app on Android.

To solve the issue, you need to add the Android path to your environment variables.

In Ubuntu, this can be done by editing the .bash_profile file located in your home directory:

``nano ~/.bash_profile``

Add the following to the file then save it:

`` export ANDROID_HOME=$HOME/Android/Sdk
    export PATH=$PATH:$ANDROID_HOME/tools
    export PATH=$PATH:$ANDROID_HOME/tools/bin
    export PATH=$PATH:$ANDROID_HOME/platform-tools
    ``
Then you can execute the following command to propagate the change to your system:

`` source ~/.bash_profile``

For Windows, here’s a detailed tutorial on how you can add the Android path: <a href="http://www.automationtestinghub.com/setup-android-environment-variables/" target="_blank">Setup Android Environment Variables.</a>

## Required Android packages not installed

Another issue which you might encounter when first starting out is that the Android packages required by React Native are not installed.

You can solve this by opening Android studio, then click on the configure button and select SDK Manager.

Check the below packages

* Android 6.0 (Marshmallow)
  * Google APIs
  * Android SDK Platform 23
  * Intel x86 Atom_64 System Image
  * Google APIs Intel x86 Atom_64 System Image
  
  Next, under the SDK Tools tab, the requirement is Android SDK Build-Tools version 23.0.1.
  
  Go through the installation process and that should solve the issue. Note that the items I’ve checked are the ones that are required by React Native.

If you’re using Google Play services in your project, you should install the following packages from the SDK Tools as well:

Google Play services
Support Repository
Android Support Repository
Google Repository

## Build tool problems

Sometimes, you’ll also encounter problems with the build tools that React Native uses for building the app or running the development server.
* Watchman

React Native uses Watchman to watch the project files for changes. This allows you to automatically rebuild the app so the changes will be reflected on the emulator or device as you’re developing.

Here’s the error that you’ll usually get if there is a problem with Watchman. This problem usually occurs in Ubuntu, but it can occur in other operating systems as well:
The build log says the error is:
``    Could not run adb reverse: Command failed: /home/wern/Android/Sdk/platform-tools/adb -s 192.168.56.101:5555 reverse tcp:8081 tcp:8081
``
Unfortunately, Googling the error “could not run adb reverse react native” doesn’t really return results which point out to the actual cause of the problem. It only gives us the idea that something is wrong with the development server.

To solve this issue, you need to run the development server separately. You can do that by executing react-native start.

This returns the actual error which prevents the development server from running automatically:

`` inotify-add-watch(/home/wern/dev/mobile/TestProject/android/app/build/intermediates/incremental/mergeDebugResources/merged.dir) -> The user limit on the total number of inotify watches was reached; increase the fs.inotify.max_user_watches sysctl

    All requests will continue to fail with this message until you resolve 
    the underlying problem.  You will find more information on fixing this at
    https://facebook.github.io/watchman/docs/troubleshooting.html#poison-inotify-add-watch
 
 ``
   
This points you out to the following page: <a href="https://facebook.github.io/watchman/docs/troubleshooting.html#poison-inotify-add-watch">Troubleshooting Watchman</a>. Which then points out to this page: <a href="https://facebook.github.io/watchman/docs/install.html#system-specific-preparation">Installation</a> for the actual solution.

Unfortunately, the solution presented isn’t really very helpful. Especially if you don’t have much experience with Linux commands.

Here’s are the commands which you need to execute:

``    sudo sysctl fs.inotify.max_user_instances=99999
    sudo sysctl fs.inotify.max_user_watches=99999
    sudo sysctl fs.inotify.max_queued_events=9999
    ``
This raises the limits of the inotify-watches to a really high value. Setting it to a value of 99999 is like saying to Watchman to use however much resource it needs to watch the directories. Because the underlying issue here is that Watchman wasn’t able to allocate the resources it needs because the default values were too low.

After that, shut down the Watchman server so the changes will be reflected in the system:

``watchman shutdown-server``

Once that’s done, executing react-native start should work smoothly. You can even skip it and just run react-native run-android because that will also run the development server in the background. Be sure to terminate the currently running process before you proceed (press Ctrl + C or Cmd + C on your keyboard).

## Gradle

Gradle is the build tool used for Android app development. React Native also taps into it in order to build and compile the app to an executable .apk file.

The most common problem that you might encounter, especially when your project is using a lot of third-party native modules, is the collision of Gradle dependencies. Collisions occur when two or more native modules are using different versions of native dependencies.

The most common among the native dependencies which cause a collision is the Google Play service. Any native module which uses Google’s services (for example, Firebase, Google Maps, AdMob) imports Google Play services as one of its native dependency.

The good news is someone has already written about this subject in really nice detail, so I’ll just point you out to the article: <a href="https://medium.com/@suchydan/how-to-solve-google-play-services-version-collision-in-gradle-dependencies-ef086ae5c75f">How to solve Google Play Services version collision in Gradle dependencies.</a>

In the future, it’s always a good idea to check whether you’ll have a potential collision before installing a specific module. You can do that by opening the android/app/build.gradle file on the modules Github repo.

For example, here’s the build.gradle file of the <a href="https://github.com/sbugert/react-native-admob">React Native AdMob</a> module. Check the packages under the dependencies to find out whether you will have a collision. And then use the article I’ve pointed out above as a guide for dealing with the collision:

## Third-party package issues

<a href="https://blog.pusher.com/debugging-react-native-android/"> Issues commonly encountered when using third-party packages</a>
