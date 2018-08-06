# Troubleshooting

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
