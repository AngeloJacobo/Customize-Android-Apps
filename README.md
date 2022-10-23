# Customize-Android-Apps
This contains my notes on how to customize existing Android apps such as changing app name, app icon, hiding app from the app drawer, and others. These steps were done on a Windows PC. 

## Preparation
The first step to customize an Android app is of course to download the `.apk` file:
1. Search your desired app to customize in [Google Play](https://play.google.com/store/apps).
2. Copy the link of the app from Google Play to this [apk downloader site](https://apps.evozi.com/apk-downloader/). For the purpose of this demonstration, I will customize [AnyDesk Remote Desktop](https://play.google.com/store/apps/details?id=com.anydesk.anydeskandroid). Below shows the downloaded `.apk` file.  
![image](https://user-images.githubusercontent.com/87559347/197316309-4b9e9b1a-6dae-426d-9858-1847347e69a2.png)
3. Next, we will need to decompile this `.apk` file (then recompile later after customizing it) to extract the codes. We will use [Easy Apk Tool](https://apk-easy-tool.en.lo4d.com/windows) for that. Download the tool, extract, then run `apkeasytool.exe`.

4. Browse the apk file then click on Decompile button. A new folder will be created under `/1-Decompiled APKs/`.  
![image](https://user-images.githubusercontent.com/87559347/197329777-62e3beb3-badd-445b-969b-895223ae72d8.png)


## Customize App Name
First thing you might want to do is to change the name that appears on the app drawer and the name on the Settings>Apps>App_Name:
1. Go inside the decompiled folder and open the manifest file `AndroidManifest.xml`. Search the keyword `android:label`. 
![image](https://user-images.githubusercontent.com/87559347/197320497-d1426ee5-0ae9-4094-8ab5-046f6025dbb2.png)
2. The value of the `android:label` pertains to the app name. As seen below, the value is `"@string/app_name"`. This means the value is inside the `string.xml` file and is stored specifically on the `app_name` variable.  
![image](https://user-images.githubusercontent.com/87559347/197321872-b199b6ee-14a6-41f5-9680-40b90dd78ec1.png)
3. The `string.xml` can be located under `res/values/`. Search for the keyword `app_name` then take note of the string value. On this demonstration, the app name is `AnyDesk`.
![image](https://user-images.githubusercontent.com/87559347/197323456-7a579e1f-c627-4873-8ce3-768de70116e5.png)  
4. We will now change this string value **for all instances**. First, search for all instance of the name by running `grep -rnw <app_name>` on the top directory of the decompiled folder. The result will include the filename and the linenumber where the app name is hardcoded. On this demonstration, I run `grep -rnw AnyDesk`.  
![image](https://user-images.githubusercontent.com/87559347/197323696-bb39102c-951c-44fb-aed3-4ca047482280.png)   
5. We can manually change the name for each files listed above which is very tedious. Instead, we can just use the bash terminal and some commands:  
```
find . -type f -name "*.xml" -exec sed -i'' -e 's/<previous_name>/<customized_name>/g' {} +
```
This will search for all `.xml` files recursively then substitute all instances of `<previous_name>` to `<customized_name>`. On this demonstration, I run: 
```
find . -type f -name "*.xml" -exec sed -i'' -e 's/AnyDesk/My App/g' {} +
```
This will change the name from `AnyDesk` to `My App`. For sanity check if the app name is changed, look for the `app_name` under `strings.xml` again. The string value must now match your desired new app name.   
https://user-images.githubusercontent.com/87559347/197324278-b9da1784-56dc-4a11-aa57-fa69b65d25d9.png  

6. We can now convert the decompiled codes back to `.apk` file. Go back to Easy APK tool, change the compile name, then cick on Compile to compile it back to apk file. The generated `.apk` file will be created under `/2-Recompiled APKs/`.    
![image](https://user-images.githubusercontent.com/87559347/197329747-74eacbf7-affe-4353-b419-df8397264f2e.png) 

7. Install the `.apk` to your phone. Done! As shown below, the app name is changed from `AnyDesk` to `My App`.  
![image](https://user-images.githubusercontent.com/87559347/197369454-04232906-e660-4763-95ad-47d34400379b.png)


## Customize App Icon
After changing the app name, you might also want to customize the app icon:
1. Go inside the decompiled folder and open the manifest file `AndroidManifest.xml`. Search the keyword `android:icon`. 
![image](https://user-images.githubusercontent.com/87559347/197368442-93dcc4c5-025c-4e4e-83e8-3fe73ba5b421.png)  
2. The value of the `android:icon` pertains to the file location of the app icon. As seen above, the value is `"@mipmap/ic_launcher`. Go to `/res/` directory then notice folders starting with `mipmap`. Each folder contains various icons used by the app. 
![image](https://user-images.githubusercontent.com/87559347/197368558-f21a66a0-2646-4325-9b5f-406b6df8fd67.png)  
3. We will now change every icons for all `mipmap` folders. Make sure all icon names will remain, just replace the image. To make it less tedious, you can just replace all icons with the same images.
![image](https://user-images.githubusercontent.com/87559347/197369204-6b9d6dc8-3d77-41e9-8bf2-40f5c4b75c99.png)
5. We can now convert the decompiled codes back to `.apk` file. Go back to Easy APK tool, change the compile name, then cick on Compile to compile it back to apk file. The generated `.apk` file will be created under `/2-Recompiled APKs/`.  
![image](https://user-images.githubusercontent.com/87559347/197329747-74eacbf7-affe-4353-b419-df8397264f2e.png)
6. Install the apk to your phone. Done! As shown below, the app icon of `MyDesk` is now different.
![image](https://user-images.githubusercontent.com/87559347/197369607-504958d3-8714-4cd8-b086-822e50893121.png)

## Hide App from App Drawer
There might be situations where you might want your app to not appear on the app drawer. You can use app launcher to hide apps (like this [HideU: Calculator Lock](https://play.google.com/store/apps/details?id=com.calculator.hideu&gl=US)) but this will implicitly give someone an idea that you have an app that you don't want others to see. If you want to hide your app without app launchers, follow the steps below:
1. Go inside the decompiled folder and open the manifest file `AndroidManifest.xml`. Search for the keyword `android.intent.category.LAUNCHER`.   
2. This category means that the app should appear in the launcher (your app drawer) as a top-level application. To hide your app, just comment the line containing the keyword `android.intent.category.LAUNCHER`. A comment starts with **<!--** and ends with **-->**

`![image](https://user-images.githubusercontent.com/87559347/197370076-3136c021-cf4d-47a8-a2c0-06a50b828a0c.png)`











