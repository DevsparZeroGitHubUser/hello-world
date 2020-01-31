# <a name="XenditySDK"></a> Xendity - Cordova
Docs version: 1.0.1<br>
Last updated: Dec 13, 2019

**Xendity SDK for Cordova** is a SDK that allows the use of ID Scanning Features and Face Match capabilities in Cordova Applications. This version is a ported/converted version of existing [Xendity SDK for Android Platform](https://github.com/XenchainIO/xendity_android_sdk) and [Xendity SDK for iOS Platform](https://github.com/XenchainIO/xendity_ios_framework), featuring the usage of Native SDK functions and ease of integration for Cordova Developments. This version is intended and used to fulfill SME (Small and Medium Entreprise) Sector requirements.

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
                <li> Ported/Converted existing Xendity SDK to allow Cordova Integration. </li>
            </ul>
        </td>
    </tr>
    <tr>
        <td valign="top">1.0.1</td>
        <td valign="top" style="white-space: nowrap;">Jovial</td>
        <td valign="top" style="white-space: nowrap;">2019-12-13</td>
        <td valign="top">
            <ul>
                <li> Added Pre-Deployment function. </li>
                <li> Added Landmark Checking function. </li>
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
<i>Step 1:</i> Download Xendity SDK folder into local folder. The files are located together in the same directory with this document. Otherwise, please contact Xendity Admin for SDK request.
Please note that before any integration is done to the existing project, you may modify the codes in the plugin to suit your requirements e.g. Camera UI. <br>

<i>Step 2:</i> Integrate the SDK into existing project:
1. Go to Command Prompt and navigate to the designated project folder that requires the SDK Integration.
2. Execute `cordova plugin add (path to the local folder of the downloaded Xendity SDK Plugin)`.
3. Execute `cordova build` and ensure both platforms are build successfully.

## <a name="InitialSetup"></a> Initial Setup
### <a name="DeclarationManifest"></a> Declaration AndroidManifest.xml
<i>Step 1</i>: The SDK uses permissions as listed below for **Android Platform**. Kindly note that the app requires to implement it's own Permission Requests as the SDK does not provide Permission Requests.
```xml
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
<uses-permission android:name="android.permission.CAMERA" />
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" /> // Optional
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" /> // Optional
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.READ_PHONE_STATE" />
<uses-permission android:name="android.permission.RECORD_AUDIO" />
```
<i>Step 2</i>: For Android Platform depending on the API URL provided, additional resources file with the following code, path and name (res/xml/network_security_config.xml) is required:
```xml
<network-security-config>
    <domain-config cleartextTrafficPermitted="true">
        <domain includeSubdomains="true">{Put The API URL Here}</domain>
    </domain-config>
</network-security-config>
```

### <a name="InitXenditySDK"></a> Initialize Xendity SDK
Please ensure that you execute the code below first with the callback called before proceeding to other features of the SDK. If not, other features will not run or will produce errors.
```javascript
cordova.plugins.XenditySDK.initSDK(String apiKey, String apiURL, successCallback, errorCallback);
```
| Parameter       | Description |
|-----------------|-------------|
| apiKey          | API Key for activating SDK Features. Please note that both Android & iOS will have different API Key, the app must use different API Key for different platform. |
| apiURL          | URL Server Address which can be configured to point to another server should client request private server. The value of this parameter will need to be requested from Xendity Admin. |
| successCallback | Callback function for returning the success results of `initSDK` function. If called means that the App has access to other features enabled by Xendity. |
| errorCallback   | Callback function for returning the error results of `initSDK` function. |

## <a name="SDKConfiguration"></a> Additional SDK configuration
Please note that the configuration below can only be configured through their respective Native Interface. Please refer to the **CordovaXenditySDK.java** or **CordovaXenditySDK.m** file for Android or iOS platform respectively for the settings below.
```java
/** Will use for the Scanning Sound e.g. beep sound when scan successfully **/
XenditySDK.ScanningSound = inputActivity.getResources().getIdentifier("modern_data_beep", "raw", inputActivity.getPackageName());
/** Refers to the Loading Image of the SDKs **/
XenditySDK.LoadingImage = inputActivity.getResources().getIdentifier("@drawable/loading_logo", null, inputActivity.getPackageName());
```
```objectivec
/** Will use for the Scanning Sound e.g. beep sound when scan successfully **/
[XenditySDK setScanningSound:[NSBundle.mainBundle.bundlePath stringByAppendingString:@"/modern_data_beep.mp3"]];
/** Refers to the Loading Image of the SDKs **/
[XenditySDK setLoadingLogo:[UIImage imageNamed:@"loading_logo.png"]];
```
Additionally the above resource files (modern_data_beep.mp3 and/or loading_logo.png) may be replaced with other resource file provided the filename and type is the same.

## <a name="ImplementationIDCardReader"></a> Implementation of ID Card Reader
### <a name="XScannerActivity"></a> Implementation of Custom Scanner Activity
Before proceed calling the `deployScanner` function, the app must have an Extended `XScannerActivity` or `XScannerViewController` class, in which the extended class will be used to Scan ID Card. For Cordova implementation, these classes have been implemented in the plugin. Refer to **CameraOCRActivity.java (activity_camera_ocr.xml for UI)** for Java or **CameraOCRViewController.h and CameraOCRViewController.m (Xendity.storyboard for UI)** for iOS. The default UI has been implemented for both platform. Any changes on the UI can be done through these files.

### <a name="PreDeployment"></a> Pre-Deployment Details for Text Similarity Results
Before proceeding to `deployScanner`, the app may opt to execute the function below. In this case, this function is used as a check value, which will be compared against OCR Results obtained from `deployScanner` function.
```javascript
cordova.plugins.XenditySDK.setPreDeployment(String userID, JSONObject inputDetails, successCallback, errorCallback);
```
| Parameter       | Description |
|-----------------|-------------|
| userID          | Applicable only if the particular onboarding needs to be tied to certain user, otherwise the value is empty string. |
| inputDetails    | A JSON Object that contains the full name and IC Number of the user. Param key for full name is `fullName`. Param key for IC Number is `documentNumber`. |
| successCallback | Callback function for returning the success results of `PreDeployment` function. It contains `onBoardingID` value, which refers to the Overall Transaction ID for the whole Onboarding Process. The value contained in this variable will be used to track User's onboarding journeys. |
| errorCallback   | Callback function for returning the error results of `PreDeployment` function. It will be represented as String format. |

The sample value of `inputDetails` is shown as below.
```json
{
  "fullName": "Test Name",
  "documentNumber": "123456789012"
}
```

### <a name="StartScanID"></a> Start Scan ID CARD
```javascript
cordova.plugins.XenditySDK.deployScanner(int scanType, successCallback, errorCallback);
```
| Parameter       | Description |
|-----------------|-------------|
| scanType        | Determines which ID Card that will be scanned by the SDKs. Further information can be check in ID Scanning Type for the available types of ID Scanning. |
| successCallback | Callback function for returning the success results of `deployScanner` function. It will be represented as JSON format. |
| errorCallback   | Callback function for returning the error results of `deployScanner` function. It will be represented as String format. |

After `successCallback` is called, the app must call the function below to confirm the results of the `successCallback`. This means that the SDK will confirm that the `deployScanner` function is considered as completed and will be charged (billed) as per overall onboarding transaction. Failure to do so would mean that for each `deployScanner` call, the SDK will charged (billed) each of the call.
```javascript
cordova.plugins.XenditySDK.completeScanDeployment(String onBoardingID, JSONObject metaCardResult, JSONObject cardResult, int scanType, successCallback, errorCallback);
```
| Parameter       | Description |
|-----------------|-------------|
| onBoardingID    | Refers to the Overall Transaction ID for the whole Onboarding Process. The value contained in this variable will be used to track User's onboarding journeys. |
| metaCardResult  | Refers to the `MetaResults` passed from the `deployScanner` function. |
| cardResult      | Refers to the `ScannerResults` passed from the `deployScanner` function. |
| scanType        | The value of this param must follow back the inputted value of `scanType` in the `deployScanner` function. |
| successCallback | Callback function for returning the success results of `deployScanner` function. It will be represented as JSON format. |
| errorCallback   | Callback function for returning the error results of `deployScanner` function. It will be represented as String format. |

### <a name="ScanningType"></a> ID Scanning Type
Below show the supported scanning type.

| Scan Type | Description                                              |
|-----------|----------------------------------------------------------|
| 0         | Passport / MRZ Scanning Type                             |
| 1         | MyKad Front Scanning Type                                |
| 2         | MyKad Back Scanning Type                                 |
| 12        | MyKad Front & Back Scanning Type                         |
| 123       | MyKad Front & Back Scanning Type with Landmark checking. |
| 3         | Thailand National ID Card Scanning Type                  |
| 5         | Thailand Driving License ID Card Scanning Type           |

## <a name="ImplementationFaceMatch"></a> Implementation Face Match feature
### <a name="XFaceMatchActivity"></a> Implementation of Custom Face Record Activity
Before proceed calling the `deployFaceRecord` function, the app must have an Extended `XFaceRecordActivity` or `XFaceRecordViewController` class, in which the extended class will be used to process Face Recording. For Cordova implementation, these classes have been implemented in the plugin. Refer to **FaceRecordActivity.java (activity_face_record.xml for UI)** for Java or **FaceRecordViewController.h and FaceRecordViewController.m (Xendity.storyboard for UI)** for iOS. The default UI has been implemented for both platform. Any changes on the UI can be done through these files.

### <a name="StartFaceLiveness"></a> Start Face Liveness feature
Kindly note that ID Scan Feature must be implemented and executed first before proceeding to Face Record Feature.
```javascript
cordova.plugins.XenditySDK.deployFaceRecord(String onBoardingID, successCallback, errorCallback);
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
cordova.plugins.XenditySDK.IDVerificationForOnBoarding(String onBoardingID, successCallback, errorCallback);
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
cordova.plugins.XenditySDK.RequestKBAForOnBoarding(String onBoardingID, String referenceNo, successCallback, errorCallback);
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
cordova.plugins.XenditySDK.VerifyKBAForOnBoarding(String onBoardingID, String referenceNo, String answers, Activity inputActivity, final XendityKBACallback callback);
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
