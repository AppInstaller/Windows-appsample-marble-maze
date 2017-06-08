
# Build an UWP app with runtime access to network shares

With the Windows 10 Creators Update, we are enabling developers to create UWP apps that can access network shares during the apps runtime when the device is in developer mode. This feature is built in an effort to make it easier for our developers to collaborate with other developers. 

Follow the instructions below to see how you can build an UWP app that can access network shares. In this process, the app code is decoupled from the assets. The assets sit on a network share and the app code is packaged with the app. While you deploy the app code once, you are free to modify the assets as you wish. When the app is launched, the app will pull the latest assets from the network folder. 

## What you need
1. UWP app - You can fork or download this GitHub sample 
2. Network share folder - Any shared folder that your target device has access to. We will go through how to create a network share folder below. 

## 1. UWP App 

The UWP app that is part of this GitHub sample is a basic 3D game using DirectX. The functionality to access network share during the app's runtime makes a lot of sense to use while building UWP games. Games are usually asset heavy and they go through a lot of churn during game development. Because the app code and assets are decoupled while using this functionality, game developers can independently iterate on the app code and assets. 

For that same reason, we are going to modify the UWP app to use assets from a network share instead of the local app package. During the app's runtime, the app will access the assets from the network share instead of looking for them in the app package like they normally do. 

To get started:
1. Either download or clone the GitHub sample
2. Launch Visual Studio Solution - MarbleMaze_VS2015.sln
3. Open Package.appxmanifest to open
4. Add the restricted capability to the manifest as shown below - 
```xml
  <Capabilities>
    <rescap:Capability Name="developmentModeNetwork" />
  </Capabilities>
```
5. Add the 
```xml
<Package xmlns="http://schemas.microsoft.com/appx/manifest/foundation/windows10" 
         xmlns:mp="http://schemas.microsoft.com/appx/2014/phone/manifest" 
         xmlns:uap="http://schemas.microsoft.com/appx/manifest/uap/windows10" 
         xmlns:rescap="http://schemas.microsoft.com/appx/manifest/foundation/windows10/restrictedcapabilities" 
         IgnorableNamespaces="uap mp rescap">
```


## Setup required to try packaged apps with network access
![MarbleMaze app in action](MarbleMaze.png)

This sample is written in C++ and requires some experience with graphics programming and DirectX. 
Complete content that examines this code can be found at 
[Developing Marble Maze, a UWP game in C++ and DirectX](https://msdn.microsoft.com/windows/uwp/gaming/developing-marble-maze-a-windows-store-game-in-cpp-and-directx).

## Features

- Incorporating the Windows Runtime into your DirectX game 
- Using DirectX to render 3D graphics for display in a game 
- Implementing simple vertex and pixel shaders with HLSL 
- Developing simple physics and collision behaviors in a DirectX game 
- Handling input from accelerometer, touch, and mouse, and game controller with the Windows Runtime and XInput 
- Playing and mixing sound effects and background music with XAudio2 

## Related topics

[Marble Maze]( http://go.microsoft.com/fwlink/?LinkId=624010)  
[Direct3D 11 game development](https://msdn.microsoft.com/library/windows/apps/mt228367.aspx)  
[Create a simple UWP game with DirectX](https://msdn.microsoft.com/library/windows/apps/mt210793.aspx)  
[Direct3D 11 graphics](https://msdn.microsoft.com/library/windows/apps/ff476080.aspx)  
[HLSL](https://msdn.microsoft.com/library/windows/desktop/bb509561.aspx)  
[Direct2D graphics ](https://msdn.microsoft.com/library/windows/apps/dd370990.aspx)  
[XAudio2](https://msdn.microsoft.com/library/windows/apps/hh405049.aspx)  
[XInput](https://msdn.microsoft.com/library/windows/apps/hh405053.aspx)  
[Developing games](https://msdn.microsoft.com/library/windows/apps/mt228375.aspx)  

## Universal Windows Platform development

This sample requires Visual Studio 2015 and the Windows Software Development Kit (SDK) for Windows 10. 

[Get a free copy of Visual Studio 2015 Community Edition with support for building Universal Windows apps](http://go.microsoft.com/fwlink/?LinkID=280676)

Additionally, to be informed of the latest updates to Windows and the development tools, join the [Windows Insider Program](https://insider.windows.com/ "Become a Windows Insider").

## Build the sample

1. Uunzip the archive.
2. Start Microsoft Visual Studio 2015 and select **File** \> **Open** \> **Project/Solution**.
3. Starting in the folder where you unzipped the sample, go to the C++ subfolder. Double-click the Visual Studio 2015 Solution (.sln) file.
4. Press Ctrl+Shift+B, or select **Build** \> **Build Solution**.

## Run the sample

The next steps depend on whether you just want to deploy the sample or you want to both deploy and run it.

### Deploying the sample

- Select Build > Deploy Solution. 

### Deploying and running the sample

- To debug the sample and then run it, press F5 or select Debug >  Start Debugging. To run the sample without debugging, press Ctrl+F5 or selectDebug 
