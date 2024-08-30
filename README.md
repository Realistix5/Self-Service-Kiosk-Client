# Self-Service-Kiosk Client by Christopher Trautmann

## Introduction

This project was designed and developed as part of my bachelor thesis, aiming to provide a self-service kiosk for a local tennis club.

This repository contains the client application for the project using an Android app to implement the SumUp card reader SDK. It is intended to be used together with [Self-Service-Kiosk Server](https://github.com/Realistix5/Self-Service-Kiosk-Server) which contains a webserver that this app can connect to. Together they provide a self-service-kiosk for a tennis club, allowing members to order food and drinks, pay directly or later and view their account details.

## Features
- **Restrict user access to your webserver only** by using an Android WebView and utilizing Androids [Lock Task Mode](https://developer.android.com/work/dpc/dedicated-devices/lock-task-mode)
- **Start Payments** by clicking a button containing a custom URL scheme
- **Secure Payment Processing** by integrating the [SumUp mPOS SDK](https://github.com/sumup/sumup-android-sdk)
- **Return Payment Result** back to the webserver
- **Customizable Interface to your webserver** through a settings menu. The settings also allow you to customize the WebView and the SumUp SDK.

## Limitations
Because the project was custom developed for a german tennis club, there are a few limitations that you should consider before thinking about adapting it in another context:
### Language
The whole front end of the app is in German language. Changing it to another language does require some work, but should be possible in a reasonable amount of time.
### Payment Service Provider (SumUp)
This project uses the SumUp mPOS SDK to process card payments and is limited to that provider. If you want to use another payment service provider, you would have to replace the SumUp SDK with the SDK of your provider.

## Installation
To install the app, you can either download the APK from the [app/release](/app/release) folder or clone the repository and build the app yourself. To build the app, you need to have Android Studio installed on your computer. After cloning the repository, open the project in Android Studio and build the app. You can then install the app on your Android device or an emulator.

Because the app utilizes Androids `Lock Task Mode`, you will need to set `de.chrtra.sumup_self_service_kiosk/.MyDeviceAdminReceiver` as device owner before you can use the app.
You can do this by enabling Android Developer options and especially [USB debugging](https://developer.android.com/studio/debug/dev-options#Enable-debugging) of your device, connecting it and running the following command through the [Android Debug Bridge (ADB)](https://developer.android.com/tools/adb) after you installed the app:
```shell
adb shell dpm set-device-owner de.chrtra.sumup_self_service_kiosk/.MyDeviceAdminReceiver
```
Now you should be able to start the app and use it.

## Usage
Before you can use the main function, the self-service application, accessible via the button `Starte Kundenanwendung` , you need to configure the app.
You can do this by clicking the clicking the button `Einstellungen` after starting the app. Here you can configure the following settings:
- **Custom URL Scheme**: The custom URL scheme that the app should use to start payments.
- **Webserver URLs**: The URLs of the webserver that the app should start the WebView with and that the app should return the payment results to individually.
- **WebView Settings**: Settings for the WebView that displays the webserver.
- **SumUp Settings**: Settings for the SumUp SDK that processes the payments.

After you have saved the required settings, you need to login a SumUp merchant account login. 
To do so, you need to click the button `Händler Login` in the main menu. This will open a SumUp login page.
After you have logged in, you will get sent back to the main menu.
Now you can start using the app to its full extent.

## License
This project is licensed under the MIT License - see the [LICENSE.txt](LICENSE.txt) file for details.

## Acknowledgments
This project is based on the [SumUp mPOS SDK](https://github.com/sumup/sumup-android-sdk).

The project was developed as part of my bachelor thesis at the [Hochschule Darmstadt - University of Applied Sciences](https://h-da.de/).

I would like to thank my supervisor [Prof. Dr. Daniel Burda](https://fbi.h-da.de/personen/daniel-burda) for his support and guidance throughout the project.

I would also like to thank the [tennis department of GSV Gundernhausen e.V.](https://tennis.gsv-gundernhausen.de/) for providing the opportunity to develop this project for them.
