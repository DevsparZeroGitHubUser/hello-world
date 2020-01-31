# <a name="XenchainSDK"></a> Xenchain - Cordova
Docs version: 1.0.0<br>
Last updated: Nov 13, 2019

Xenchain SDK for Cordova is SDK that allows the use of ID Scanning Features and Face Match capabilities into Cordova Applications. This version is a ported/conversion version of existing [Xenchain SDK for Android Platform](https://github.com/XenchainIO/xenchain_android_sdk_v1.1) and [Xenchain SDK for iOS Platform](https://github.com/XenchainIO/xenchain_ios_framework_v1.1), featuring the usage of Native SDK functions and ease of integration for Cordova Developments. This version is intended and used to fulfill SME Sector requirements.

## <a name="Authors"></a> Authors
Jovial Tan (jovial@xendity.com)<br>

## <a name="Revision"></a> Revision History

<table style="width:100%;">
    <tr>
        <th>Version</th>
        <th width=140>Author</th>
        <th width=120>Date</th>
        <th>Description</th>
    </tr>
    <tr>
        <td valign="top">1.0.0</td>
        <td valign="top" style="white-space: nowrap;">Jovial</td>
        <td valign="top" style="white-space: nowrap;">2019-11-13</td>
        <td valign="top">
            <ul>
                <li> Ported/Converted existing Xenchain SDK to allow Cordova Integration. </li>
            </ul>
        </td>
    </tr>
<table>

## <a name="FeatureList"></a> Feature List
| Feature List                                          |
|-------------------------------------------------------|
| • ID Card Reader                                      |
| • ID Card Verification                                |
| • Face Verification                                   |
| • KBA Verification                                    |

### <a name="AddSDK"></a> Adding SDK into project
<i>Step 1:</i> Download Xenchain SDK folder into local folder. The files are located in together with this document. Otherwise, please contact Xendity Admin for SDK request.
Please note that before any integration to the existing project, the developer may opt to modify the codes in the plugin to suit their requirements e.g. Camera UI. <br>

<i>Step 2:</i> Integrate the SDK into existing project:
1. Go to Command Prompt and navigate to the designated project folder that requires the SDK Integration.
2. Execute `cordova plugin add (path to the local folder of the downloaded Xenchain SDK Plugin)`.
3. Execute `cordova build` and ensure both platforms are build successfully.

## <a name="InitialSetup"></a> Initial Setup
### <a name="DeclarationManifest"></a> Declaration AndroidManifest.xml
<i>Step 1</i>: The SDK uses permissions as listed below for **Android Platform**. Kindly note that the app are required to implements it's own Permission Request as the SDK does not provide Permission Request.
```xml
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
<uses-permission android:name="android.permission.CAMERA" />
<uses-permission android:name="android.permission.FLASHLIGHT" /> // Optional
<uses-permission android:name="android.permission.VIBRATE"/> // Optional
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" /> // Optional
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" /> // Optional
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.READ_PHONE_STATE" />
<uses-permission android:name="android.permission.RECORD_AUDIO" />
```
<i>Step 2</i>: For Android Platform depending on the API URL provided, additional resources file with the following path and name (res/xml/network_security_config.xml) is required:
```xml
<network-security-config>
    <domain-config cleartextTrafficPermitted="true">
        <domain includeSubdomains="true">{Put The API URL Here}</domain>
    </domain-config>
</network-security-config>
```

### <a name="InitXenchainSDK"></a> Initialize Xenchain SDK
Please ensure that you execute the below code first with it's callback called before proceeding to other features of the SDK.
```javascript
cordova.plugins.XenchainSDK.initSDK(String apiKey, String apiURL, boolean onPremSaveData, successCallback, errorCallback);
```
| Parameter       | Description |
|-----------------|-------------|
| apiKey          | API Key for activating SDK Features. Please note that both Android & iOS will have different API Key, the app must use different API Key for different platform. |
| apiURL          | URL Server Address which can be configured to point another server should client request private server. The value of this parameter will need to be requested from Xendity Admin. |
| onPremSaveData  | Determines whether the data returned from SDK will be saved into on-premise server. Only applicable if the client decided to host the backend server into client's own server. |
| successCallback | Callback function for returning the success results of `initSDK` function. If called means that the App has access to other features enabled by Xendity. |
| errorCallback   | Callback function for returning the error results of `initSDK` function. |

## <a name="SDKConfiguration"></a> Additional SDK configuration
Please note that the below configuration can only be configured through the respective Native Interface. Refer to the **CordovaXenchainSDK.java** or **CordovaXenchainSDK.m** file for Android or iOS platform respectively for the settings below.
```java
/** Will use for the Scanning Sound e.g. beep sound when scan successfully **/
XenchainSDK.ScanningSound = inputActivity.getResources().getIdentifier("modern_data_beep", "raw", inputActivity.getPackageName());
/** Refers to the Loading Image of the SDKs **/
XenchainSDK.LoadingImage = inputActivity.getResources().getIdentifier("@drawable/loading_logo", null, inputActivity.getPackageName());
```
```objectivec
/** Will use for the Scanning Sound e.g. beep sound when scan successfully **/
[XenchainSDK setScanningSound:[NSBundle.mainBundle.bundlePath stringByAppendingString:@"/modern_data_beep.mp3"]];
/** Refers to the Loading Image of the SDKs **/
[XenchainSDK setLoadingLogo:[UIImage imageNamed:@"loading_logo.png"]];
```
Additionally the above resources (modern_data_beep.mp3 and/or loading_logo.png) may simply be replaced with other resources provided it's filename is the same.

## <a name="ImplementationIDCardReader"></a> Implementation of ID Card Reader
### <a name="XScannerActivity"></a> Implementation of Custom Scanner Activity
Before proceed calling the `deployScanner` function, the app must have an Extended `XScannerActivity` or `XScannerViewController` class, in which the extended class will be used to Scan ID Card. For Cordova implementation, these classes have been implemented in the plugin. Refer to **CameraOCRActivity.java (activity_camera_ocr.xml for UI)** for Java or **CameraOCRViewController.h and CameraOCRViewController.m (Xenchain.storyboard for UI)** for iOS. The default UI has been implemented for both platform. Any changes on the UI can be done through these files.

### <a name="StartScanID"></a> Start Scan ID CARD
```javascript
cordova.plugins.XenchainSDK.deployScanner(int scanType, successCallback, errorCallback);
```
| Parameter       | Description |
|-----------------|-------------|
| scanType        | Determines which ID Card that will be scanned by the SDKs. Further information can be check in **CordovaXenchainSDK.java** for Java or **CordovaXenchainSDK.m** for iOS. |
| successCallback | Callback function for returning the success results of `deployScanner` function. It will be represented as JSON format. |
| errorCallback   | Callback function for returning the error results of `deployScanner` function. It will be represented as String format. |

Kindly note that the below code is required to be executed after `successCallback` function being called. Otherwise, for each scanning, the SDK will charged the scan and in on-premise server case, no data will be passed to server.
```javascript
cordova.plugins.XenchainSDK.completeScanDeployment(String onBoardingID, String cardFrontReferenceID, String faceReferenceID, String cardBackReferenceID, JSONObject cardResult, successCallback, errorCallback);
```
| Parameter            | Description                                                                                                                      |
|----------------------|----------------------------------------------------------------------------------------------------------------------------------|
| onBoardingID         | The Overall Transaction ID for the whole Onboarding Process.                                                                     |
| cardFrontReferenceID | The reference ID of the `refFrontID` from `successCallback` function passed from `deployScanner` function.                       |
| faceReferenceID      | The reference ID of the `refFace` from `successCallback` function passed from `deployScanner` function.                          |
| cardBackReferenceID  | The reference ID of the `refBackID` from `successCallback` function passed from `deployScanner` function.                        |
| cardResult           | The scan results of the `ScannerResults` from `successCallback` function passed from `deployScanner` function.                   |
| successCallback      | Callback function for returning the success results of `completeScanDeployment` function. It will be represented as JSON format. |
| errorCallback        | Callback function for returning the error results of `completeScanDeployment` function. It will be represented as String format. |

### <a name="ScanningConfiguration"></a> Scanning Configuration
The behavior of scanning must be configured through the implementation of the class below. Each of the class represents each IDs that are supported by the SDK.
Please note, further configurations must be set in Native Code instead, refer to the **CordovaXenchainSDK.java** or **CordovaXenchainSDK.m** file for Android or iOS platform respectively.

| Scan Config Class | Description                                    |
|-------------------|------------------------------------------------|
| MyKadConfig       | MyKad Scanning Configuration (ScanType = 0)    |
| MyDLConfig        | MyDL Scanning Configuration (ScanType = 1)     |
| PassportConfig    | Passport Scanning Configuration (ScanType = 2) |

## <a name="ImplementationFaceRecord"></a> Implementation Face Record feature
### <a name="XFaceMatchActivity"></a> Implementation of Custom Face Record Activity
Before proceed calling the `deployFaceRecord` function, the app must have an Extended `XFaceRecordActivity` or `XFaceRecordViewController` class, in which the extended class will be used to process Face Recording. For Cordova implementation, these classes have been implemented in the plugin. Refer to **FaceRecordActivity.java (activity_face_record.xml for UI)** for Java or **FaceRecordViewController.h and FaceRecordViewController.m (Xenchain.storyboard for UI)** for iOS. The default UI has been implemented for both platform. Any changes on the UI can be done through these files.

### <a name="StartFaceLiveness"></a> Start Face Liveness feature
Kindly note that ID Scan Feature must be implemented first and executed before proceed to Face Record Feature.
```javascript
cordova.plugins.XenchainSDK.deployFaceRecord(String onBoardingID, successCallback, errorCallback);
```
| Parameter         | Description                                                                                                                |
|-------------------|----------------------------------------------------------------------------------------------------------------------------|
| onBoardingID      | Refers to the particular OnBoarding Transaction ID.                                                                        |
| successCallback   | Callback function for returning the success results of `deployFaceMotion` function. It will be represented as JSON format. |
| errorCallback     | Callback function for returning the error results of `deployFaceMotion` function. It will be represented as String format. |

## <a name="ImplementationKBAVerification"></a> Implementation KBA Verification related feature.
### <a name="IDVerification"></a> Implementation of ID Verification for KBA Verification
Kindly note that ID Scan Feature must be implemented first and executed before proceed for ID Verification feature.
```javascript
cordova.plugins.XenchainSDK.IDVerificationForOnBoarding(String onBoardingID, successCallback, errorCallback);
```
| Parameter         | Description                                                                                                                           |
|-------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| onBoardingID      | Refers to the particular OnBoarding Transaction ID.                                                                                   |
| successCallback   | Callback function for returning the success results of `IDVerificationForOnBoarding` function. It will be represented as JSON format. |
| errorCallback     | Callback function for returning the error results of `IDVerificationForOnBoarding` function. It will be represented as String format. |

The sample value returned from `successCallback` for the above function is shown as below.
```json
{
    "ref_no": "123456789012",
    "ref_id": "asdfhahlfgaljf",
    "external_source": "",
    "status": "Identity Not Found From any of the Sources"
}
```

### <a name="KBARequest"></a> Implementation of KBA Request for Onboarding.
Kindly note that ID Scan Feature & ID Verification Feature must be implemented first and executed before proceed for KBA Request. This feature will be used to provide questions for the users to answers.
```javascript
cordova.plugins.XenchainSDK.RequestKBAForOnBoarding(String onBoardingID, String referenceNo, successCallback, errorCallback);
```
| Parameter         | Description                                                                                                                       |
|-------------------|-----------------------------------------------------------------------------------------------------------------------------------|
| onBoardingID      | Refers to the particular OnBoarding Transaction ID.                                                                               |
| referenceNo       | Refers to the particular `ref_no` taken from the `successCallback` function passed from `IDVerificationForOnBoarding` function.   |
| successCallback   | Callback function for returning the success results of `RequestKBAForOnBoarding` function. It will be represented as JSON format. |
| errorCallback     | Callback function for returning the error results of `RequestKBAForOnBoarding` function. It will be represented as String format. |

The sample value returned from `successCallback` for the above function is shown as below.
```json
[
  {
    "id": "1001",
    "question": "Do you have a House Loan with AIM Bank?"
  },
  {
    "id": "1002",
    "question": "Do you have a House Loan with Bank ABC?"
  },
  {
    "id": "1003",
    "question": "Do you have a House Loan with XYZ Bank?"
  },
  {
    "id": "1004",
    "question": "Do you have a Credit Card with POI Bank?"
  },
  {
    "id": "1005",
    "question": "Do you have a House Loan with Bank DEF?"
  }
]
```

### <a name="KBAVerification"></a> Implementation of KBA Verification for Onboarding.
Kindly note that ID Scan Feature, ID Verification Feature, & KBA Request Feature must be implemented first and executed before proceed for KBA Verification.
```javascript
cordova.plugins.XenchainSDK.VerifyKBAForOnBoarding(String onBoardingID, String referenceNo, String answers, Activity inputActivity, final XenchainKBACallback callback);
```
| Parameter         | Description |
|-------------------|-------------|
| onBoardingID      | Refers to the particular OnBoarding Transaction ID. |
| referenceNo       | Refers to the particular `ref_no` taken from the `successCallback` function passed from `IDVerificationForOnBoarding` function. |
| answers           | Refers to the JSON-String format of Array of `AnswerKBA` class. This variable will be used to verify the KBA questions provided to the users. |
| successCallback   | Callback function for returning the success results of `VerifyKBAForOnBoarding` function. It will be represented as Integer format which represents the total correct answers submitted by the user. |
| errorCallback     | Callback function for returning the error results of `VerifyKBAForOnBoarding` function. It will be represented as String format. |

The sample format of the `answers` param is shown as below. Kindly note that `id` refers to the `id` of the value returned from `successCallback` of the `RequestKBAForOnBoarding` function.
```json
[
  {
    "id": "1001",
    "answer": "YES"
  },
  {
    "id": "1002",
    "answer": "NO"
  },
  {
    "id": "1003",
    "answer": "YES"
  },
  {
    "id": "1004",
    "answer": "NO"
  },
  {
    "id": "1005",
    "answer": "YES"
  }
]
```
