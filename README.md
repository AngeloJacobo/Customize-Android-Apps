# Customize-Android-Apps
This contains my notes on how to customize existing Android apps such as changing app name, app icon, hiding app from the app drawer, and others. These steps were done on a Windows PC. 

# Preparation
The first step to customize an Android app is of course to download the `.apk` file:
1. Search your desired app to customize in [Google Play](https://play.google.com/store/apps).
2. Copy the link of the app from Google Play to this [apk downloader site](https://apps.evozi.com/apk-downloader/). For the purpose of this demonstration, I will customize [AnyDesk Remote Desktop](https://play.google.com/store/apps/details?id=com.anydesk.anydeskandroid). Below shows the downloaded `.apk` file.  
![image](https://user-images.githubusercontent.com/87559347/197316309-4b9e9b1a-6dae-426d-9858-1847347e69a2.png)
3. Next, we will need to decompile this `.apk` file (then recompile later after customizing it) to extract the codes. We will use [apktool](https://www.droidviews.com/compile-and-decompile-apk-files-with-apktool/) for that, follow the instructions on that site on how to setup the apktool. Make sure the location of the `apktool.jar` and the wrapper files `apktool.bat` exist on the PATH.  
4. Run `apktool.bat d <filename.apk>` to decompile your app.  
![image](https://user-images.githubusercontent.com/87559347/197320237-e0bfc80c-8622-4f7b-bf04-94ac24458b43.png)


# Customize App Name
First thing you might want to do is to change the name that appears on the app drawer and the name on the Settings>Apps>App_Name:
1. Go inside the decompiled folder and open the manifest file `AndroidManifest.xml`. Search the keyword `android:label`. 
![image](https://user-images.githubusercontent.com/87559347/197320497-d1426ee5-0ae9-4094-8ab5-046f6025dbb2.png)
2. The value of the `android:label` pertains to the app name. As seen below, the value is `"@string/app_name"`. This means the value is inside the `string.xml` file and is stored specifically on the `app_name` variable.  
![image](https://user-images.githubusercontent.com/87559347/197321872-b199b6ee-14a6-41f5-9680-40b90dd78ec1.png)
3. The `string.xml` can be located under `res/values/`. Search for the keyword `app_name` then take note of the string value. On this demonstration, the app name is `AnyDesk`
![image](https://user-images.githubusercontent.com/87559347/197323456-7a579e1f-c627-4873-8ce3-768de70116e5.png)
4. We will now change this string value **for all instances**. First, search for all instance of the name by running `grep -rnw <app_name>`. The result will include the filename and linenumber within that file where the app name is 




