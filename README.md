# Customize-Android-Apps
This contains my notes on how to customize existing Android apps such as changing app name, app icon, hiding app from the app drawer, and others. These steps were done on a Windows PC. 

# Preparation
The first step to customize an Android app is of course to download the `.apk` file:
1. Search your desired app to customize in [Google Play](https://play.google.com/store/apps).
2. Copy the link of the app from Google Play to this [apk downloader site](https://apps.evozi.com/apk-downloader/). For the purpose of this demonstration, I will customize [AnyDesk Remote Desktop](https://play.google.com/store/apps/details?id=com.anydesk.anydeskandroid). Below shows the downloaded `.apk` file.  
![image](https://user-images.githubusercontent.com/87559347/197316309-4b9e9b1a-6dae-426d-9858-1847347e69a2.png)
3. Next, we will need to decompile this `.apk` file (then recompile later after customizing it) to extract the codes. We will use [apktool](https://www.droidviews.com/compile-and-decompile-apk-files-with-apktool/) for that, follow the instructions on that site on how to setup the apktool. Make sure the location of the `apktool.jar` and the wrapper files `apktool.bat` exist on the PATH.  
4. Run `apktool.bat d <filename.apk>` to decompile your app.  
![image](https://user-images.githubusercontent.com/87559347/197317726-cca66f19-43a1-4623-af0b-647cd2781212.png)

