# Sample app for flutter-web with enablex video sdk

This is a Sample Flutter web App demonstrates the use of [EnableX platform Server APIs](https://developer.enablex.io/docs/guides/video-guide/sample-codes/video-calling-app/#demo-application-server) and Flutter Toolkit to build 1-to-1 RTC (Real-Time Communication) Application. It allows developers to ramp up on app development by hosting on their own devices.

This App creates a virtual Room on the fly hosted on the Enablex platform using REST calls and uses the Room credentials (i.e. Room Id) to connect to the virtual Room as a mobile client. The same Room credentials can be shared with others to join the same virtual Room to carry out an RTC session.

NOTE: Supported languages: Web and mobile

> EnableX Developer Center: https://developer.enablex.io/

## 1. Getting Started

### 1.1 Prerequisites


#### 1.1.1 App Id and App Key

- Register with EnableX [https://www.enablex.io/free-trial/]
- Create your Application
- Get your App ID and App Key delivered to your email

#### 1.1.2 Sample Flutter Client

* Clone or download this Repository : https://github.com/EnableX/Sample-Flutter-Web-app-using-enablex-flutter-video-sdk-.git


#### 1.1.3 Test Application Server

You need to set up an Application Server to provision Web Service API for your Flutter Application to enable Video Session.

To help you to try our Flutter Application quickly, without having to set up Application Server, this Application is shipped pre-configured to work in a "try" mode with EnableX hosted Application Server i.e. https://demo.enablex.io.

Our Application Server restricts a single Session Duations to 10 minutes, and allows 1 moderator and not more than 3 participants in a Session.

Once you tried EnableX Flutter Sample Application, you may need to set up your own Application Server and verify your Application to work with your Application Server. Refer to point 2 for more details on this.

#### 1.1.4 Configure Flutter Client

- Open the App
- Go to Main.dart and change the following:

```
 /* To try the App with Enablex Hosted Service you need to set the kTry = true When you setup your own Application Service, set kTry = false */

     public  static  final  boolean kTry = true;

 /* Your Web Service Host URL. Keet the defined host when kTry = true */

     String kBaseURL = "https://demo.enablex.io/"

 /* Your Application Credential required to try with EnableX Hosted Service
     When you setup your own Application Service, remove these */

     String kAppId = "App_Id"
     String kAppkey = "App_Key"

```

### 1.2 Test

#### 1.2.1 Open the App

- Open the App in your Device. You get a form to enter Credentials i.e. Name & Room Id.
- You need to create a Room by clicking the "Create Room" button.
- Once the Room Id is created, you can use it and share with others to connect to the Virtual Room to carry out an RTC Session.

Note:- In case of emulator/simulator your local stream will not create. It will create only on real device.

## 2. Set up Your Own Application Server

You may need to set up your own Application Server after you tried the Sample Application with EnableX hosted Server. We have differnt variants of Appliciation Server Sample Code. Pick the one in your preferred language and follow instructions given in respective README.md file.

* NodeJS: [https://github.com/EnableX/Video-Conferencing-Open-Source-Web-Application-Sample.git]
* PHP: [https://github.com/EnableX/Group-Video-Call-Conferencing-Sample-Application-in-PHP]

Note the following:

* You need to use App ID and App Key to run this Service.
* Your Flutter Client EndPoint needs to connect to this Service to create Virtual Room and Create Token to join the session.
* Application Server is created using EnableX Server API, a Rest API Service helps in provisioning, session access and post-session reporting.

To know more about Server API, go to:
https://developer.enablex.io/docs/guides/video-guide/sample-codes/video-calling-app/#demo-application-server

## 3. Flutter Toolkit

Flutter Sample App to use Flutter Toolkit to communicate with EnableX Servers to initiate and manage Real-Time Communications.

- Documentation: https://developer.enablex.io/docs/references/sdks/video-sdk/flutter-sdk/index/
- Download: https://developer.enablex.io/docs/references/sdks/video-sdk/flutter-sdk/index/

## 4. Application Walk-through

### 4.1 Create Token

We create a Token for a Room Id to get connected to EnableX Platform to connect to the Virtual Room to carry out a RTC Session.

To create Token, we make use of Server API. Refer following documentation:
https://developer.enablex.io/docs/references/apis/video-api/content/api-routes/#create-a-room

### 4.2 Connect to a Room, Initiate & Publish Stream

We use the Token to get connected to the Virtual Room. Once connected, we intiate local stream and publish into the room. Refer following documentation for this process:
https://developer.enablex.io/docs/references/sdks/video-sdk/flutter-sdk/room-connection/index/

### 4.3 Play Stream

We play the Stream into EnxPlayerWidget Object. You can pass local true for localStream player, and local false for remote stream Players.
Add import for EnxPlayerWideget

```
import 'package:enx_flutter_plugin/enx_player_widget.dart';

EnxPlayerWidget(0, local: true)
```

### 4.4 Handle Server Events

EnableX Platform will emit back many events related to the ongoing RTC Session as and when they occur implicitly or explicitly as a result of user interaction. We use Call Back Methods to handle all such events.

Add import to handle callbacks and methods:

```

import 'package:enx_flutter_plugin/enx_flutter_plugin.dart';

/* Example of Call Back Methods */

/* Call Back Method: onRoomConnected
Handles successful connection to the Virtual Room */

EnxFlutterPlugin.onRoomConnected = (Map<dynamic, dynamic> map) {
       /* You may initiate and publish stream */
        print('onRoomConnectedFlutter' + jsonEncode(map));
    };

/* Call Back Method: onRoomError
 Error handler when room connection fails */
 EnxFlutterPlugin.onRoomError = (Map<dynamic, dynamic> map) {

    };

/* Call Back Method: onStreamAdded
 To handle any new stream added to the Virtual Room */

 EnxFlutterPlugin.onStreamAdded = (Map<dynamic, dynamic> map) {
      print('onStreamAdded' + jsonEncode(map));
       /* Subscribe Remote Stream */
}


/* Call Back Method: onActiveTalkerList
 To handle any time Active Talker list is updated */

 EnxFlutterPlugin.onActiveTalkerList = (Map<dynamic, dynamic> map) {
     /* Handle Stream Players */
}
```
## 5. Demo

EnableX provides hosted Demo Application Server of different use-case for you to try out.

1. Try a quick Video Call: https://try.enablex.io
2. Try Apps on Demo Zone: https://portal.enablex.io/demo-zone/
3. Try Meeting & Webinar:  https://developer.enablex.io/docs/references/apis/ucaas-api/index/
## Flutter Web
Need to run on secure service like local host run on secure host .

To serve your Flutter web app over HTTPS using a custom certificate and key file while running it directly with Flutter's command-line tool, you currently need to use a workaround since Flutter's `flutter run -d chrome` doesn't natively support passing SSL certificate options. Instead, you can use a local HTTPS server to serve the built Flutter web app.

Here's how you can do it:

1. **Generate SSL Certificate and Key with `mkcert`**:
   - Follow the previous steps to install `mkcert` and generate a certificate and key for `localhost`.

    ```sh
    mkcert localhost
    ```

   This generates `localhost.pem` and `localhost-key.pem`.

2. **Build Your Flutter Web App**:
   - Build the Flutter web app to generate the necessary files.

    ```sh
    flutter build web
    ```

3. **Serve the Built Web App with an HTTPS Server**:
   - Use a simple HTTPS server, such as `http-server` with SSL support, to serve the built Flutter web app.

   **Install `http-server`**:
    ```sh
    npm install -g http-server
    ```

   **Run `http-server` with HTTPS**:
    ```sh
    http-server build/web -S -C localhost.pem -K localhost-key.pem -p 8080
    ```

   This serves the `build/web` directory over HTTPS on port 8080.

4. **Open Chrome with Flags**:
   - Open Chrome with the `--ignore-certificate-errors` flag to ignore self-signed certificate warnings.

   **On Linux or macOS**:
    ```sh
    google-chrome --ignore-certificate-errors --user-data-dir=/tmp/foo --allow-insecure-localhost https://localhost:8080
    ```

   **On macOS, if `google-chrome` command doesn't work**:
    ```sh
    /Applications/Google\ Chrome.app/Contents/MacOS/Google\ Chrome --ignore-certificate-errors --user-data-dir=/tmp/foo --allow-insecure-localhost https://localhost:8080
    ```

   **On Windows**:
    ```sh
    "C:\Program Files (x86)\Google\Chrome\Application\chrome.exe" --ignore-certificate-errors --user-data-dir=/tmp/foo --allow-insecure-localhost https://localhost:8080
    ```

### Alternative: Custom Web Server for Local Development

If you want a more integrated solution, you can create a simple custom server script in Dart to serve your Flutter web app with HTTPS. Below is an example using `shelf` and `shelf_static` packages.

**1. Add Dependencies**:
Add `shelf` and `shelf_static` to your `pubspec.yaml`.

```yaml
dependencies:
   shelf: ^1.3.0
   shelf_static: ^1.1.0
```

**2. Create a Custom Server Script (`server.dart`)**:
Create a Dart script to serve your Flutter web app with HTTPS.

```dart
import 'dart:io';
import 'package:shelf/shelf_io.dart' as io;
import 'package:shelf_static/shelf_static.dart';

void main() async {
   var handler = createStaticHandler('build/web', defaultDocument: 'index.html');
   var server = await io.serve(
      handler,
      InternetAddress.loopbackIPv4,
      8080,
      securityContext: SecurityContext()
         ..useCertificateChain('localhost.pem')
         ..usePrivateKey('localhost-key.pem'),
   );

   print('Serving at https://${server.address.host}:${server.port}');
}
```

**3. Run the Custom Server Script**:
Run the script using the Dart VM.

```sh
dart run server.dart
```

This serves your Flutter web app over HTTPS on `https://localhost:8080`.

### Summary

By building your Flutter web app and serving it with an HTTPS server like `http-server` or a custom Dart server using `shelf`, you can achieve running your Flutter web app over HTTPS. This workaround addresses the current limitation of `flutter run -d chrome` not supporting SSL certificate options directly.

