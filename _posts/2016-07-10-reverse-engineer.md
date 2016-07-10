---
layout: post
comments: true
permalink: /blog/:title
title: Reverse Engineering an APK
---

Earlier this year, I was tasked with reverse engineering an APK. For reasons I won't explain, I needed to extract the code from this APK because the APK contained the latest version of code for the project. So, I set out on researching how I can unzip the APK into its individual parts: the resources for the application and the decompiled java code.

There's a few things I learned from doing this and I'll explain them throughout this post, but it's good to note upfront that APKs don't necessarily contain _all_ of the parts of the Android project. You won't be able to extract the Gradle scripts from the APK, because the Gradle script files are not compiled into the APK (obviously). Also, if you're expecting the java source code to be exactly as it is in the Android project, think again. Java code that is compiled and decompiled will be in short form (i.e., how it's interpreted by the Java Virtual Machine). It won't necessarily be "readable" anymore and it won't contain any comments. But, if you're a Java developer, you probably already know this. Also, it's helpful to know that an APK is nothing more than a .zip file containing compiled Java code and Android resources. Technically, you can just unzip the APK, but you'll find that the files are going to be unreadable.

Now, it's good to note that there are websites out there that will decompile the APK for you in one easy upload of the file. And there are apps out there that you can download onto your Android phone that will decompile the APK to retrieve metadata from the APKs already installed on your phone. But, if you're like me, you probably don't trust those services with APKs that you built yourself and there's honestly no telling what they'll do with your decompiled code. 
Also, it's worth mentioning that Google has built a single tool called [Classy Shark](https://github.com/google/android-classyshark) which will handle the decompilation (both Java and Android resources) for you.

But, without further ado, here are the steps _I followed_ to decompile an APK on my own.

Make sure to download these files and install them before following the steps below.

1. [Apktool](http://ibotpeaches.github.io/Apktool)
2. [dex2jar](https://github.com/pxb1988/dex2jar)
3. [JD-GUI](http://jd.benow.ca/)

For the purposes of demoing how to decompile an APK, I've built a dummy APK out of an Android Studio project template that contains a single Activity and a single Fragment (along with layout resources for each). My project, like any other Android project contains the Android Manifest file and Gradle scripts. I'm also going to assume you're using a Mac, but note that the three aforementioned tools have installation instructions for other platforms on their respective websites.

## Step 1: Extract the Android Resources using Apktool
Latest Apktool installation instructions can be found [here](http://ibotpeaches.github.io/Apktool/install/)

1. Download the Apktool mac [wrapper script](https://raw.githubusercontent.com/iBotPeaches/Apktool/master/scripts/osx/apktool) (Right click, Save Link As apktool) Or rename after downloading file via cli: `mv apktool.txt apktool`
2. Download [apktool-2](https://bitbucket.org/iBotPeaches/apktool/downloads)
3. Rename downloaded jar to apktool.jar
4. Move both files (apktool.jar & apktool) to /usr/local/bin (root needed)
5. Make sure both files are executable via cli: `chmod +x apktool` and `chmod +x apktool.jar`
6. Via cli, run: 
```
apktool d ~/Desktop/dummy_app.apk -o ~/Desktop/dummy_app
```

You'll notice that you now have a folder containing the Android resources. But, at least the Android resources are readable!
Take a look at the before and after Android Manifest files in my gist [here](https://gist.github.com/TylerMcCraw/fc62a13a6ec4a9877858db853d274f6d)

## Step 2: Extract the compiled Java code using dex2jar

1. Unzip the APK file via cli: 
```
unzip ~/Desktop/dummy_app.apk -d ~/Desktop/dummy_app
```
2. Download the dex2jar tool and unzip it.
3. Recursively set executable permissions to files within the new dex2jar folder via cli: `chmod -R +x ~/Desktop/dex2jar-2.0/`
4. Change your current directory to the same directory that was created via the Apktool so that the dex2jar script outputs the decompiled .jar file in a place that you can easily find later: `cd ~/Desktop/dummy_app`
5. Execute the d2j-jar2dex shell script against your APK via cli:
```
~/Desktop/dex2jar-2.0/d2j-dex2jar.sh ~/Desktop/dummy_app.apk
```

You'll notice that you now have a file titled something like "dummy_app-dex2jar.jar" in your current directory. This file was converted from the APK's classes.dex (Dalvik Executable) file. This jar contains the APK's java code! All we need now is a tool to decompile the jar.

## Step 3: Decompile the Jar using JD-GUI
Latest installation instructions on this tool can be found [here](http://jd.benow.ca/).
Alternatively, you can use any java decompiler tool that you prefer. This step isn't necessarily specific to Android decompilation.

1. Extract the JD-GUI tool from the download
2. Double click on the tool (.jar file for Mac) to open it.
3. Using the tool, click on "Open a file" and select the jar file that was extracted using dex2jar in Step 2 above.

JD-GUI should now show folders containing the Java class files. These aren't going to be exactly as they are in the developer's Android project because they are the decompiled short-form classes, as I mentioned earlier.
If you'd like to save the decompiled class files, just click on File -> Save All Sources.
Take a look at the before and after Java class files in my gist [here](https://gist.github.com/TylerMcCraw/fc62a13a6ec4a9877858db853d274f6d)

That's it! Now that you have the source code and the Android resource files, you can use it to help you get a glimpse of how the application is architected and to decipher how the application works.