
# Build an UWP app with runtime access to network shares

With the Windows 10 Creators Update, we are enabling developers to create UWP apps that can access network shares during the apps runtime when the device is in developer mode. This feature is built in an effort to make it easier for our developers to collaborate with other developers. 

Follow the instructions below to see how you can build an UWP app that can access network shares. In this process, the app code is decoupled from the assets. The assets sit on a network share and the app code is packaged with the app. While you deploy the app code once, you are free to modify the assets as you wish. When the app is launched, the app will pull the latest assets from the network folder. 

## What you need
1. UWP app - You can fork or download this GitHub sample 
2. Network share folder - Any shared folder that your target device has access to. We will go through how to create a network share folder below. 

## UWP App manifest declaration 

The UWP app that is part of this GitHub sample is a basic 3D game using DirectX. The functionality to access network share during the app's runtime makes a lot of sense to use while building UWP games. Games are usually asset heavy and they go through a lot of churn during game development. Because the app code and assets are decoupled while using this functionality, game developers can independently iterate on the app code and assets. 

For that same reason, we are going to modify the UWP app to use assets from a network share instead of the local app package. During the app's runtime, the app will access the assets from the network share instead of looking for them in the app package like they normally do. 

To get started:
1. Either download or clone the GitHub sample
2. Launch Visual Studio Solution - MarbleMaze_VS2015.sln
3. Open Package.appxmanifest to open
4. Add the required namespace and the restricted capability to the manifest as shown below - 
```xml
<Package xmlns="http://schemas.microsoft.com/appx/manifest/foundation/windows10" 
         xmlns:mp="http://schemas.microsoft.com/appx/2014/phone/manifest" 
         xmlns:uap="http://schemas.microsoft.com/appx/manifest/uap/windows10" 
         xmlns:rescap="http://schemas.microsoft.com/appx/manifest/foundation/windows10/restrictedcapabilities" 
         IgnorableNamespaces="uap mp rescap">
 ...
 ...
 ...
<Capabilities>
  <rescap:Capability Name="developmentModeNetwork" />
</Capabilities>
```

Now we will go ahead and create a network share where we will store the assets that the app will load. 

### Create a network share 

If you already have a network share and your target machine can access that share, then you can skip this section. 

1. Create a new folder on your desktop 
2. Right-click on the folder and go to Properties and shift to the Sharing tab. 
3. Click on "Share..." button
4. Here you can either choose "Everyone" or specify the folks that you want to have access to this folder.
5. Click "Share" on the bottom of the dialogue prompt
6. Copy the network share path that starts '\\\'

You are done! Now, all we need to do is copy the assets from the app package to the network share and modify the path in the app code to the new network path. 

### UWP App Code changes

#### Copy the assets to the network share folder

If you downloaded/cloned the MarbleMaze sample from GitHub, go to C++/MarbleMaze_VS2015/Media/Textures/ to find some of the assets used in the game. For simplicity, lets only copy the loadscreen.png file to the network share. 

#### Make code change to access the new path 

Open LoadScreen.cpp file on your code editor and modify the path specified in CreateDecoderFromFilename function to use the new network share path: 
``` cpp
    ComPtr<IWICBitmapDecoder> wicBitmapDecoder;
    DX::ThrowIfFailed(
        m_wicFactory->CreateDecoderFromFilename(
            L"Media\\Textures\\loadscreen.png",
            nullptr,
            GENERIC_READ,
            WICDecodeMetadataCacheOnDemand,
            &wicBitmapDecoder
            )
        );
 ```
 ``` cpp
     ComPtr<IWICBitmapDecoder> wicBitmapDecoder;
    DX::ThrowIfFailed(
        m_wicFactory->CreateDecoderFromFilename(
            L"//CDON/desktop/public/loadscreen.png",
            nullptr,
            GENERIC_READ,
            WICDecodeMetadataCacheOnDemand,
            &wicBitmapDecoder
            )
        );
```

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
