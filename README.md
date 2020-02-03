# <a name="XenditySDK"></a> Xendity - Android
SDK version: 1.0.8<br>
Last updated: Jan 30, 2020

**Xendity SDK for Android** is an SDK that allows the use of ID Document Scanning Features and Face Match capabilities on your Android Applications. This version is an *In-House Version* of the existing [Xenchain SDK for Android Platform](https://github.com/XenchainIO/xenchain_android_sdk), featuring more improvement in performance and ease of integration in comparison to older version.

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
        <td valign="top" style="white-space: nowrap;">2019-07-19</td>
        <td valign="top">
            <ul>
                <li> Overhaul Xendity SDK for In-House OCR Scanner. </li>
            </ul>
        </td>
    </tr>
    <tr>
        <td valign="top">1.0.1</td>
        <td valign="top" style="white-space: nowrap;">Jovial</td>
        <td valign="top" style="white-space: nowrap;">2019-08-01</td>
        <td valign="top">
            <ul>
                <li> Added new `OCRType` for passport scanning. </li>
                <li> Added UI customisation feature for `XCameraActivity`. </li>
            </ul>
        </td>
    </tr>
    <tr>
        <td valign="top">1.0.2</td>
        <td valign="top" style="white-space: nowrap;">Jovial</td>
        <td valign="top" style="white-space: nowrap;">2019-09-05</td>
        <td valign="top">
            <ul>
                <li> Added `deployFaceRecord` feature for Liveness Detection. </li>
                <li> Added UI customisation feature for `XFaceRecordActivity`. </li>
            </ul>
        </td>
    </tr>
    <tr>
        <td valign="top">1.0.3</td>
        <td valign="top" style="white-space: nowrap;">Jovial</td>
        <td valign="top" style="white-space: nowrap;">2019-12-20</td>
        <td valign="top">
            <ul>
                <li> Added `deployFaceMatch` feature for Liveness Detection. </li>
                <li> Added UI customisation feature for `XFaceMatchActivity`. </li>
                <li> Added `setPreDeployment` feature for Text Similarity function. </li>
                <li> Added ID and KBA Verification feature. </li>
                <li> Added `completeScanDeployment` function. </li>
            </ul>
        </td>
    </tr>
    <tr>
        <td valign="top">1.0.4</td>
        <td valign="top" style="white-space: nowrap;">Jovial</td>
        <td valign="top" style="white-space: nowrap;">2019-12-26</td>
        <td valign="top">
            <ul>
                <li> Added fallback method for Old MyKad. </li>
                <li> Fixed crash issue on `XFaceMatchActivity` due to fast `finish()` function. </li>
            </ul>
        </td>
    </tr>
    <tr>
        <td valign="top">1.0.5</td>
        <td valign="top" style="white-space: nowrap;">Jovial</td>
        <td valign="top" style="white-space: nowrap;">2020-01-16</td>
        <td valign="top">
            <ul>
                <li> Added `setPreviewOCR` function for ID Capture Preview. </li>
                <li> Fixed the sensitivity issue on the `deployFaceMatch` function. </li>
                <li> Added list of `ErrorCode` for SDK fallback function. </li>
            </ul>
        </td>
    </tr>
    <tr>
        <td valign="top">1.0.6</td>
        <td valign="top" style="white-space: nowrap;">Jovial</td>
        <td valign="top" style="white-space: nowrap;">2020-01-21</td>
        <td valign="top">
            <ul>
                <li> Added Face Comparable feature. </li>
                <li> Pass `ErrorCode` from scanner if it did not pass Face Comparable. </li>
            </ul>
        </td>
    </tr>
    <tr>
        <td valign="top">1.0.7</td>
        <td valign="top" style="white-space: nowrap;">Jovial</td>
        <td valign="top" style="white-space: nowrap;">2020-01-22</td>
        <td valign="top">
            <ul>
                <li> Update the motion of `XFaceMatchViewController` from Blink then Smile to become Smile then Blink. </li>
            </ul>
        </td>
    </tr>
    <tr>
        <td valign="top">1.0.8</td>
        <td valign="top" style="white-space: nowrap;">Jovial</td>
        <td valign="top" style="white-space: nowrap;">2020-01-30</td>
        <td valign="top">
            <ul>
                <li> Fixed duplicate records on backend and text similarity issue. </li>
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

## <a name="SDKSteps"></a> Summary of SDK Functions in 4 Steps
| Steps Activation | Actions | Function Name |
| :--------------: | ------- | ------------- |
| Step 0           | Initialize Xendity SDK | [`initSDK`](#-initialize-xendity-sdk) |
| Step 1           | Implementation of ID Card Reader | [`deployScanner`](#-implementation-of-id-card-reader) |
| Step 2           | Implementation of Face Match Feature | [`deployFaceMatch`](#-implementation-face-match-feature) |
| Step 2           | Implementation of Liveness Feature | [`deployFaceRecord`](#-implementation-liveness-feature) |
| Step 3           | Implementation of KBA Verification Related Feature | [`IDVerificationForOnBoarding`](#-implementation-kba-verification-related-feature) |
| Step 4           | Implementation of KBA Request for Onboarding.<br />Implementation of KBA Verification for Onboarding. | [`RequestKBAForOnBoarding`](#-implementation-of-kba-request-for-onboarding)<br />[`VerifyKBAForOnBoarding`](#-implementation-of-kba-verification-for-onboarding) |

### <a name="AddSDK"></a> Adding SDK into project
<i>Step 1:</i> Download the Xendity SDK .aar file. Please note that you are required to use Git LFS (Git Large File Storage) to download the Frameworks folder. Otherwise, manually download the [Xendity SDK](Frameworks/XenditySDK.aar) file and replace it into the Frameworks folder. <br>

<i>Step 2:</i> (option 1): Adding the .aar into your project:
1. Select File > New > New Module
2. Choose "Import .jar/.aar Package"
3. Select where the .aar location.
4. Open 'build.gradle' file(the one under 'app') and add dependency:
   * implementation project(':XenditySDK')

<i>Step 2: (option 2)</i>: Adding .aar file to the libs folder:
1. Create 'libs' folder under src/main
2. Copy your .aar file to src/main/libs
3. Open 'build.gradle' file(the one under 'app') and add dependency:
   * implementation(name: 'XenditySDK', ext: 'aar')
4. An error message, "Failed to resolve :my library" will be displayed, this is normal. To fix this error open the top level 'build.gradle' file and add the following code:
```javascript
defaultConfig {
    // The rest of the Config....
    multiDexEnabled true
}

dexOptions {
    javaMaxHeapSize "4g" // Depending on project requirement. Default value is set as shown.
}

allprojects {
    repositories {
        jcenter()
        flatDir {
            dirs 'src/main/libs'
        }
    }
}

useLibrary 'org.apache.http.legacy'

```
<i>Step 3</i>: Add the following required libraries to build.gradle:
```javascript
implementation 'com.google.code.gson:gson:2.8.2'
implementation 'com.mcxiaoke.volley:library:1.0.19'
implementation 'com.android.support:design:28.0.0'
implementation "com.android.support:appcompat-v7:28.0.0"
implementation 'com.android.support.constraint:constraint-layout:1.1.3'
implementation 'com.android.support:support-annotations:28.0.0'
implementation 'com.android.support:support-v13:28.0.0'

implementation 'com.google.android.gms:play-services-vision:17.0.2'
```

## <a name="InitialSetup"></a> Initial Setup
### <a name="DeclarationManifest"></a> Declaration AndroidManifest.xml
<i>Step 1</i>: The SDK use permissions as listed below. Kindly note that the app requires to implement it's own Permission Requests as the SDK does not provide Permission Requests. 
```xml
<uses-permission android:name="android.permission.READ_PHONE_STATE" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.CAMERA" />
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.RECORD_AUDIO"/>

<uses-feature android:name="android.hardware.camera" />
<uses-feature android:name="android.hardware.camera.autofocus"/>
```
*Note : Permission Request is a window that shows up asking for permission to access the required hardware/software component on the smartphone such as camera/contacts/wifi/etc when you install and run any android app for the first time.*

<i>Step 2</i>: FileProvider definition is required for Android Lolipop(5.0), Android Marshmallow (6.0) Android Nougat (7.0) and Above. Please add the following code to your Manifest:
```xml
<provider
    android:name="android.support.v4.content.FileProvider"
    android:authorities="{Replace this with Project Package Name}.fileprovider"
    android:exported="false"
    android:grantUriPermissions="true">
    <meta-data
        android:name="android.support.FILE_PROVIDER_PATHS"
        android:resource="@xml/provider_path"/>
</provider>
```
Also add the following code to a new resources file with the following path and name (res/xml/provider_path.xml):
```xml
<?xml version="1.0" encoding="utf-8"?>
<paths>
    <external-path name="." path="."/>
</paths>
```
<i>Step 3</i>: Depending on the API URL provided, additional resources file with the following code, path and name (res/xml/network_security_config.xml) is required:
```xml
<network-security-config>
    <domain-config cleartextTrafficPermitted="true">
        <domain includeSubdomains="true">{Put The API URL Here}</domain>
    </domain-config>
</network-security-config>
```

### <a name="ImportSDK"></a> Code to import SDK classes
```java
import com.xendity.reader.XenditySDK;
import com.xendity.reader.Callback.XenditySDKCallback;
import com.xendity.reader.Callback.XendityScannerCallback;
import com.xendity.reader.Model.Enum.OCRType;
```

### <a name="InitXenditySDK"></a> Code to initialize Xendity SDK
Please ensure that you execute the code below first before proceeding to other features of the SDK. If not, other features will not run or will produce errors.
```java
XenditySDK.initSDK(String apiKey, String apiURL, Activity inputActivity, XenditySDKCallback callback);
```
| Parameter      | Description |
|----------------|-------------|
| apiKey         | API Key for activating SDK Features. |
| apiURL         | URL Server Address which can be configured to point another server should client request private server. The value of this parameter will need to be requested from Xendity Admin. |
| inputActivity  | Activity class that is used for the scanner. |
| callback       | Callback function for returning the results of `initSDK` function. |

### <a name="XenditySDKCallback"></a> XenditySDKCallback callback functions
```java
public void InitSDKStatus(boolean status, String message);
```
<b>Description:</b>
Callback function that returns two value(status and message) to determine the status of the initialization process of XenditySDK.<br>
<b>Parameters:</b>
* status : Determines whether the SDK can be used or not.
* message : Contains the error message if the SDK cannot be initialized.

## <a name="SDKConfiguration"></a> Additional SDK configuration
#### <a name="ScanningSound"></a> Custom Scanning Sound
```java
XenditySDK.ScanningSound = R.raw.modern_data_beep;
```
Kindly note that the input must be in int based raw format.

#### <a name="LoadingDialogImage"></a> Loading Dialog Image
```java
XenditySDK.LoadingImage = R.drawable.please_wait;
```
Kindly note the input must be in int based drawable format.

#### <a name="CustomLoadingDialog"></a> Custom Loading Dialog
```java
XenditySDK.SDKLoadingDialog = new Dialog();
```
Kindly note the input must be in `Dialog` Data Type format.

## <a name="ImplementationIDCardReader"></a> Implementation of ID Card Reader
### <a name="PreDeployDetails"></a> Pre-Deploy Scanner Details.
This function is optional and is used to provide the App with Text Similarity features. In this case, the function below takes a JSON Input which contains the preliminary user details.
```java
XenditySDK.setPreDeployment(String userID, JSONObject inputDetails, Activity inputActivity, XendityPreDeployCallback callback)
```
| Parameter     | Description |
|---------------|-------------|
| userID        | Applicable only if the particular onboarding needs to be tied to certain user, otherwise the value is empty string. |
| inputDetails  | A JSON Object that contains the full name and IC Number of the user. Param key for full name is `fullName`. Param key for IC Number is `documentNumber`. |
| inputActivity | Activity class that is used for the `setPreDeployment`. |
| callback      | Callback function for PreDeployment Scanning. |

The sample value of `inputDetails` is shown as below.
```json
{
  "fullName": "Test Name",
  "documentNumber": "123456789012"
}
```

### <a name="XCameraActivity"></a> Implementation of the Custom Scanner Activity
Before proceeding to call the `deployScanner` function, the app must have an Extended `XCameraActivity` class, in which the extended class will be used to scan the ID Card. The minimum implementation of the Extended `XCameraActivity` class is shown below.
```java
/** Sample Class of Extended XCameraActivity */
public class CameraActivity extends XCameraActivity implements View.OnClickListener {
    private final String TAG = "CameraActivity";

    @Override
    protected void onCreate(@Nullable Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);

        LayoutInflater vi = (LayoutInflater) getSystemService(Context.LAYOUT_INFLATER_SERVICE);
        /** Adding Custom View is possible with the condition that the Root Layout's background must be Transparent */
        View v = vi.inflate(R.layout.activity_camera, null);
        /** Call the setupCustomScanner to add the custom view into XCameraActivity */
        setupCustomScanner(v);
        /** For this example, assume that the layout has R.id.camera_start_capture */
        v.findViewById(R.id.camera_start_capture).setOnClickListener(this);
    }

    @Override
    protected void prepareForFrontCapture() {
        Log.d(TAG, "This function is called when the Scanner is ready for Front ID Capture");
    }

    @Override
    protected void completeFrontCapture(Bitmap frontBitmap) {
        Log.d(TAG, "This function is called when the scanner has capture the Front ID. Image will be passed back to App for confirmation purpose");
    }

    @Override
    protected void prepareForBackCapture() {
        Log.d(TAG, "This function is called when the Scanner is ready for Back ID Capture");
    }

    @Override
    protected void completeBackCapture(Bitmap backBitmap) {
        Log.d(TAG, "This function is called when the scanner has capture the Back ID. Image will be passed back to App for confirmation purpose");
    }

    @Override
    protected void processImageFailure(String errorMessage) {
        Log.d(TAG, "processImageFailure: " + errorMessage);
    }

    /** Function below is optional and only will be called if the `setPreviewOCR` is set to `true` */
    @Override
    protected void showPreview(Bitmap previewBitmap) {
        // Do the Preview of the Image captured here.
    }

    /** Function below is optional and only will be called if the `setPreviewOCR` is set to `true` */
    @Override
    protected void dismissPreview() {
        // Dismiss the Preview here.
    }

    @Override
    public void onClick(View v) {
        if (v.getId() == R.id.camera_start_capture) {
            /** The protected function below is used to capture & process image. */
            capturePicture();
        // Below code will assume that the Preview will call the onClick function based on whether to Retry or Continue.
        } else if (v.getId() == R.id.ocr_preview_retry_button) {
            // Call this function if the User wants to retry for ID Capture.
            mPreviewListener.retryCapture();
        } else if (v.getId() == R.id.ocr_preview_continue_button) {
            // Call this function for ID Capture confirmation.
            mPreviewListener.submitCapture();
        }
    }
}
```

### <a name="StartScanID"></a> Start Scan ID CARD
Before calling the `deployScanner` function, the App may enable the `setPreviewOCR` function from XenditySDK class by setting the attribute to true which will allows the Scanner to call `showPreview` function for the App to preview the image before being submitted for the OCR Process.
```java
XenditySDK.setPreviewOCR(true);
```
*Note : This will enable preview function so that user will be able to see preview image on the app.*

Below shows the `deployScanner` that will be used to initiate the Scanner for ID Card Scanning.
```java
XenditySDK.deployScanner(int inputOCRType, Activity inputActivity, Class inputClass, XendityScannerCallback callback)
```
| Parameter     | Description |
|---------------|-------------|
| inputOCRType  | The value that determines the document types to be expected by the Scanner. Refer to [OCR Type](#OCRType) for list of available scan types. |
| inputActivity | Activity class that is used for the scanner. |
| inputClass    | The extended `XCameraActivity` class that is used as overlay for the Camera Activity. |
| callback      | Callback function for ID Scanning. |

Kindly note that the below code is required to be executed after `successCallback` function being called. Otherwise, for each scanning, the SDK will charged the scan (means you will be billed) and in on-premise server case, no data will be passed to server.
```java
XenditySDK.completeScanDeployment(String onBoardingID, JSONObject metaCardResult, JSONObject cardResult, int inputOCRType, Activity inputActivity, XendityScannerCallback callback)
```
| Parameter            | Description                                                                       |
|----------------------|-----------------------------------------------------------------------------------|
| onBoardingID         | The Overall Transaction ID for the whole Onboarding Process.                      |
| metaCardResult       | Refers to all the meta results passed from the `XendityScannerCallback` callback. |
| cardResult           | Refers to the `rawOCRResults` passed from the `XendityScannerCallback` callback.  |
| inputOCRType         | Refers to the existing `inputOCRType` used in the `deployScanner` function.       |
| completionHandler    | Callback function for ID Scanning.                                                |

The value of `metaCardResult` is shown as below.
```json
{
  "idFrontImage": "Taken From frontDocBitmap",
  "refFrontID": "Taken From refFrontDocBitmap",
  "idBackImage": "Taken From backDocBitmap",
  "refBackID": "Taken From refBackDocBitmap",
  "idFaceImage": "Taken From faceBitmap",
  "refFace": "Taken From refFaceBitmap",
}
```

### <a name="XendityScannerCallback"></a> XendityScannerCallback callback functions
---
```java
public void scanResults(JSONObject rawOCRResults, String onBoardingID, String errorMessage);
```
<b>Description:</b>
Callback function that provides Scanning Results (rawOCRResults, onBoardingID, errorMessage) from ID Scanning Process<br>
<b>Parameters:</b>
* rawOCRResults : Result card info from the reader.
* onBoardingID : The Overal Transaction ID for the whole Onboarding Process.
* errorMessage : Error passed from processing ID Card result.
---
```java
public void scanMetaDocFrontResults(Bitmap frontDocBitmap, String refFrontDocBitmap, String errorMessage);
```
<b>Description:</b>
Callback function that provides Meta Document Front Results (frontDocBitmap, refFrontDocBitmap, errorMessage) from ID Scanning Process<br>
<b>Parameters:</b>
* frontDocBitmap : The Front ID Card Image from ID Scanner.
* refFrontDocBitmap : The reference Front ID of the ID Card Image.
* errorMessage : Error passed from processing Front ID Card result.
---
```java
public void scanMetaDocBackResults(Bitmap backDocBitmap, String refBackDocBitmap, String errorMessage);
```
<b>Description:</b>
Callback function that provides Meta Document Back Results (frontDocBitmap, refFrontDocBitmap, errorMessage) from ID Scanning Process<br>
<b>Parameters:</b>
* frontDocBitmap : The Back ID Card Image from ID Scanner.
* refFrontDocBitmap : The reference Back ID of the ID Card Image.
* errorMessage : Error passed from processing Back ID Card result.
---
```java
public scanMetaDocFaceResults(Bitmap faceBitmap, String refFaceBitmap, String errorMessage);
```
<b>Description:</b>
Callback function that provides Meta Document Face Results (faceBitmap, refFaceBitmap, errorMessage) from ID Scanning Process. Only applicable if the Scan Document contains Face of the Owner's Document. (for example: Passport, ID Card, Driving License, etc)<br>
<b>Parameters:</b>
* faceBitmap : Refers to Cropped Face Image from ID Card Image.
* refFaceBitmap : The reference ID of the Cropped Face Image.
* errorMessage : Error passed from processing ID Card result.
---
```java
public void scanSimilarityResults(boolean nameIsSimilar, boolean documentNoIsSimilar, boolean frontBackIsSimilar);
```
<b>Description:</b>
Callback function that provides Text Similarity features. Only applicable if the app has execute `setPreDeployment` function. Used to determine the legitimacy of the ID Card.<br>
<b>Parameters:</b>
* nameIsSimilar : Show whether the name obtained from Scanner is similar to the value submitted in `setPreDeployment` function.
* documentNoIsSimilar : Show whether the document number obtained from Scanner is similar to the value submitted in `setPreDeployment` function.
* frontBackIsSimilar : Show whether the front ID and back ID is similar. Only applicable for MyKad Scanning.
---
```java
public void scanLandmarkInformation(JSONObject landmarkScores);
```
<b>Description:</b>
Callback function that provides the Landmark Scores (in form of JSON data object) of the ID Cards. Used to determine the legitimacy of the ID Card.<br>
<b>Parameters:</b>
* landmarkScores : The landmark scores for each field that is captured by the ID Scanner.
For full sample of `LandmarkResults` refer to below (Please note only applicable for MyKad Scanning).
```json
{
    "landmark_total_checksum": 24, "The total number of Landmark Checks detected in the ID card."
    "total_check_value": 20, "The number of Landmark Checks that are passed."
    "is_original": true "The value that determine whether this particular ID Card is Original or not."
}
```
---
```java
public void scanCompleteDeployment(boolean status, String errorMessage);
```
<b>Description:</b>
Callback function that is called when the Scanning has been charged completely (Means the billing process is successful). Not yet applicable for this version.<br>
<b>Parameters:</b>
* status : Represents whether the `completeScanDeployment` is successfully called or not.
* errorMessage : Error passed from processing `completeScanDeployment`.

### <a name="OCRType"></a> Scanning Types
This Scanning Types determines the OCR Results being produced from the Scanner. (Different types has different scanning functions) 

| Scan Config Class                | Description                                      |
|----------------------------------|--------------------------------------------------|
| ID_PSP_MRTD                      | Passport Scanning                                |
| ID_MYS_MYKAD_FRONT               | MyKad Front Scanning                             |
| ID_MYS_MYKAD_BACK                | MyKad Back Scanning                              |
| ID_MYS_MYKAD_FRONT_BACK          | MyKad Front & Back Scanning                      |
| ID_MYS_MYKAD_FRONT_BACK_LANDMARK | MyKad Front & Back Scanning with Landmark Checks |
| ID_THA_NIDC                      | Thai ID Front Scanning                           |
| ID_THA_DLC                       | Thai Driving License Scanning                    |

### <a name="IDCardReaderResult"></a> ID Card Reader Sample Results & Description
For full details of the `rawOCRResults` refer to the list below.

---
```java
public String mDocumentType = "";
```
<b>Description:</b><br>
Get document type from ID Card.

---
```java
public String mDocumentNumber = "";
```
<b>Description:</b>
Get document ID Number from ID Card.

---
```java
public String mCardNumber = "";
```
<b>Description:</b>
Get ID card Number for the Passport.

---
```java
public String mArmyNumber = "";
```
<b>Description:</b>
Get Army Number from ID Card.

---
```java
public String mBackDocumentNumber = "";
```
<b>Description:</b>
Get document ID Number from Back side of ID Card.

---
```java
public String mFrontName = "";
```
<b>Description:</b>
Get Name from Front side of ID Card.

---
```java
public String mBackName = "";
```
<b>Description:</b>
Get Name from Back side of ID Card.

---
```java
public String mBloodType = "";
```
<b>Description:</b>
Get blood type from ID Card.

---
```java
public String mAddress = "";
```
<b>Description:</b>
Get address from ID Card.

---
```java
public String mVillage = "";
```
<b>Description:</b>
Get village from ID Card (Only in Indonesia eKTP).

---
```java
public String mRTRW = "";
```
<b>Description:</b>
Get RT/RW from ID Card (Only in Indonesia eKTP).

---
```java
public String mDistrict = "";
```
<b>Description:</b>
Get district from ID Card (Only in Indonesia eKTP).

---
```java
public String mCity = "";
```
<b>Description:</b>
Get city from ID Card.

---
```java
public String mProvince = "";
```
<b>Description:</b>
Get province from ID Card (Only in Indonesia eKTP).

---
```java
public String mReligion = "";
```
<b>Description:</b>
Get religion status from ID Card.

---
```java
public String mStatus = "";
```
<b>Description:</b>
Get marital status from ID Card.

---
```java
public String mJob = "";
```
<b>Description:</b>
Get job data from ID Card.

---
```java
public String mGender = "";
```
<b>Description:</b>
Get gender data from ID Card.

---
```java
public String mCitizenship = "";
```
<b>Description:</b>
Get citizenship data from ID Card.

---
```java
public String mNationality = "";
```
<b>Description:</b>
Get nationality data from ID Card.

---
```java
public String mRace = "";
```
<b>Description:</b>
Get race data from ID Card.

---
```java
public String mPlaceOfBirth = "";
```
<b>Description:</b>
Get place of birth data from ID Card.

---
```java
public String mDateOfBirth = "";
```
<b>Description:</b>
Get date of birth from ID Card.

---
```java
public String mCountryOfBirth = "";
```
<b>Description:</b>
Get country of birth from ID Card.

---
```java
public String mFrontDateIssued = "";
```
<b>Description:</b>
Get date of issued from Front ID Card.

---
```java
public String mBackDateIssued = "";
```
<b>Description:</b>
Get date of issued from Back ID Card.

---
```java
public String mDateUpdated = "";
```
<b>Description:</b>
Get date of updated from ID Card.

---
```java
public String mFrontExpiry = "";
```
<b>Description:</b>
Get date of expiry from Front ID Card.

---
```java
public String mBackExpiry = "";
```
<b>Description:</b>
Get date of expiry from Back ID Card.

---
```java
public String mChipNumber = "";
```
<b>Description:</b>
Get chip number from ID card.

---
```java
public String mSerialNumber = "";
```
<b>Description:</b>
Get Serial Number from ID Card

---
```java
public String mEmployerInfo = "";
```
<b>Description:</b>
Get Employer Info from ID Card (Only in Singapore PASS or Work Permit).

---
```java
public String mSector = "";
```
<b>Description:</b>
Get Employer Sector from ID Card (Only in Singapore PASS or Work Permit).

---
```java
public String mEmploymentOccupation = "";
```
<b>Description:</b>
Get Employment Occupation from ID Card (Only in Singapore PASS or Work Permit).

---
```java
public String mDateOfApplication = "";
```
<b>Description:</b>
Get Date of Application from ID Card (Only in Singapore PASS or Work Permit).

---
```java
public String mForeignIdentificationNo = "";
```
<b>Description:</b>
Get Foreign Identification No from ID Card (Only in Singapore PASS or Work Permit).

---
```java
public String mFacultyInfo = "";
```
<b>Description:</b>
Get Faculty Information from ID Card (Only in Singapore PASS or Work Permit).

---
```java
public String mFacultyCityZipcodeState = "";
```
<b>Description:</b>
Get Faculty City Zip Code State from ID Card (Only in Singapore PASS or Work Permit).

---
```java
public String mFacultyAddress = "";
```
<b>Description:</b>
Get Faculty Address from ID Card (Only in Singapore PASS or Work Permit).

---

## <a name="ImplementationFaceMatch"></a> Implementation Face Match feature
### <a name="XFaceMatchActivity"></a> Implementation of Custom Face Match Activity
Before proceeding to call the `deployFaceMatch` function, the app must have an Extended `XFaceMatchActivity` class, in which the extended class will be used to process the face match motion. The minimum implementation of the Extended `XFaceMatchActivity` class is shown below.
```java
/** Sample Class of Extended XFaceMatchActivity */
public class FaceMatchActivity extends XFaceMatchActivity implements View.OnClickListener {
    private final String TAG = "FaceMatchActivity";

    @Override
    protected void onCreate(@Nullable Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);

        LayoutInflater vi = (LayoutInflater) getSystemService(Context.LAYOUT_INFLATER_SERVICE);
        /** Adding Custom View is a must with the condition that the Root Layout's background must be Transparent */
        View v = vi.inflate(R.layout.activity_face_record, null);
        /** Call the setupCustomScanner to add the custom view into XFaceMatchActivity */
        setupCustomScanner(v);

        /** For this example, assume that the layout has R.id.face_match_dismiss */
        v.findViewById(R.id.face_match_dismiss).setOnClickListener(this);
    }

    @Override
    protected void onStart() {
        super.onStart();

        // Call this function to start the Face Match
        startFaceMatch();
    }

    @Override
    public void onClick(View v) {
        if (v.getId() == R.id.face_match_dismiss) {
            /**
             * The protected function below is used to dismiss FaceMatchActivity.
             * Failure to do so might result in the blocked access to camera.
             */
            dismissFaceMatch();
        }
    }

    @Override
    protected void preSmileDetection() {
        Log.d(TAG, "This function is called to tell the App that the Scanner is ready to detect Smile.");
    }

    @Override
    protected void smileDetected() {
        Log.d(TAG, "This function is called when the Scanner has detected Smile.");
    }

    @Override
    protected void processingSmile() {
        Log.d(TAG, "This function is called to tell the App that the Scanner is processing Smile picture.");
    }

    @Override
    protected void preBlinkDetection() {
        Log.d(TAG, "This function is called to tell the App that the Scanner is ready to detect Blink Eye.");
    }

    @Override
    protected void blinkDetected() {
        Log.d(TAG, "This function is called when the Scanner has detected Eye Blink.");
    }

    @Override
    protected void processingBlink() {
        Log.d(TAG, "This function is called to tell the App that the Scanner is processing Eye Blink picture.");
    }

    @Override
    protected void completingFaceMatchProcess() {
        Log.d(TAG, "This function is called when the Scanner is about to complete the Face Match Process.");
    }
}
```

### <a name="StartFaceMatch"></a> Start Face Match Function
Kindly note that ID Scan Feature must be implemented and executed first before proceeding to the Face Match Feature.
```java
XenditySDK.deployFaceMatch(String onBoardingID, String inputImageRef, Activity inputActivity, Class inputClass, XendityFaceCallback callback);
```
| Parameter    | Description                                                                              |
|--------------|------------------------------------------------------------------------------------------|
| activity     | Activity class that is used for the scanner.                                             |
| onBoardingID | Refers to the particular OnBoarding Transaction ID.                                      |
| imageRef     | The reference ID of the `refFace` from `scanMetaDocFaceResults` function.                |
| inputClass   | The extended `XFaceMatchActivity` class that is used as overlay for the Camera Activity. |
| callback     | Callback function for Face Match Scanning.                                               |

## <a name="ImplementationLiveness"></a> Implementation Liveness feature
### <a name="XFaceRecordActivity"></a> Implementation of Custom Face Record Activity
Before proceeding to call the `deployFaceRecord` function, the app must have an Extended `XFaceRecordActivity` class, in which the extended class will be used to process the Liveness video. The minimum implementation of the Extended `XFaceRecordActivity` class is shown below.
```java
/** Sample Class of Extended XFaceRecordActivity */
public class FaceRecordActivity extends XFaceRecordActivity implements View.OnClickListener {
    private final String TAG = "FaceRecordActivity";

    @Override
    protected void onCreate(@Nullable Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);

        LayoutInflater vi = (LayoutInflater) getSystemService(Context.LAYOUT_INFLATER_SERVICE);
        /** Adding Custom View is possible with the condition that the Root Layout's background must be Transparent */
        View v = vi.inflate(R.layout.activity_face_record, null);
        /** Call the setupCustomScanner to add the custom view into XFaceRecordActivity */
        setupCustomScanner(v);

        /** For this example, assume that the layout has R.id.face_record_start_capture */
        v.findViewById(R.id.face_record_start_capture).setOnClickListener(this);
    }

    @Override
    public void onClick(View v) {
        if (v.getId() == R.id.face_record_start_capture) {
            /**
             * The protected function below is used to start the Video Recording.
             * If need of manual 'finish()', do call 'dismissVideoRecord()' function.
             */
            startVideoRecord();
        }
    }

    @Override
    protected void preBlinkDetection() {
        Log.d(TAG, "This function is called to tell the App that the Scanner is ready to detect Blink Eye.");
    }

    @Override
    protected void blinkDetected() {
        Log.d(TAG, "This function is called when the Scanner has detected Eye Blink.");
    }

    @Override
    protected void smileDetected() {
        Log.d(TAG, "This function is called when the Scanner has detected Smile.");
    }

    @Override
    protected void startRecording() {
        Log.d(TAG, "This function is called to tell the App that the Scanner is starting to record the video.");
    }

    protected void processingRecording() {
        Log.d(TAG, "This function is called to tell the App that the Scanner is processing recorded video.");
    }

    @Override
    protected void completingProcess() {
        Log.d(TAG, "This function is called when the Scanner is about to complete the Face Record Process.");
    }
}
```

### <a name="StartFaceRecord"></a> Start Face Record Function
Kindly note that ID Scan Feature must be implemented and executed first before proceeding to the Face Record / Liveness Feature.
```java
XenditySDK.deployFaceRecord(String onBoardingID, Activity inputActivity, Class inputClass, XendityFaceCallback callback);
```
| Parameter     | Description                                                                               |
|---------------|-------------------------------------------------------------------------------------------|
| onBoardingID  | Refers to the particular OnBoarding Transaction ID.                                       |
| inputActivity | Activity class that is used for the scanner.                                              |
| inputClass    | The extended `XFaceRecordActivity` class that is used as overlay for the Camera Activity. |
| callback      | Callback function for Face Match Scanning.                                                |

### <a name="XendityFaceCallback"></a> XendityFaceCallback callback functions
---
```java
public void faceMatchResult(boolean isMatched, double percentMatched, String error);
```
<b>Description:</b>
Callback function that provides Face Match Results (isMatched, percentMatched, error) from the Face Match Process<br>
<b>Parameters:</b>
* isMatched : True for Matched Face. Otherwise, False.
* percentMatched : Percentage of Face Matching.
* error : Error passed from processing Face Match result.
---
```java
public void faceMatchMetaResult(Bitmap outputBitmap, String outputRef);
```
<b>Description:</b>
Callback function that provides meta Face Match Results (outputBitmap, outputRef) from the Face Match Process<br>
<b>Parameters:</b>
* outputBitmap : The Face Image captured during Face Match Process.
* outputRef : The reference ID of the image captured.

## <a name="ImplementationKBAVerification"></a> Implementation of KBA Verification related feature.
### <a name="IDVerification"></a> Implementation of ID Verification for KBA Verification
Kindly note that ID Scan Feature must be implemented and executed first before proceeding to ID Verification feature.
```java
XenditySDK.IDVerificationForOnBoarding(String onBoardingID, Activity inputActivity, XendityKBACallback callback);
```
| Parameter         | Description                                                                                  |
|-------------------|----------------------------------------------------------------------------------------------|
| onBoardingID      | Refers to the particular OnBoarding Transaction ID.                                          |
| inputActivity     | Activity class that is used for the scanner.                                                 |
| callback          | Callback function for KBA Verification.                                                      |

### <a name="KBARequest"></a> Implementation of KBA Request for Onboarding.
Kindly note that ID Scan Feature & ID Verification Feature must be implemented and executed first before proceeding to KBA Request. This feature will be used to provide questions for the user to answer.
```java
XenditySDK.RequestKBAForOnBoarding(String onBoardingID, String referenceNo, Activity inputActivity, XendityKBACallback callback);
```
| Parameter         | Description                                                                                  |
|-------------------|----------------------------------------------------------------------------------------------|
| onBoardingID      | Refers to the particular OnBoarding Transaction ID.                                          |
| referenceNo       | Refers to the particular `ref_no` taken from the `IDVerificationStatus` callback function.   |
| inputActivity     | Activity class that is used for the scanner.                                                 |
| callback          | Callback function for KBA Verification.                                                      |

### <a name="KBAVerification"></a> Implementation of KBA Verification for Onboarding.
Kindly note that ID Scan Feature, ID Verification Feature, & KBA Request Feature must be implemented and executed first before proceeding to KBA Verification.
```java
XenditySDK.VerifyKBAForOnBoarding(String onBoardingID, String referenceNo, AnswerKBA[] answers, Activity inputActivity, XendityKBACallback callback);
```
| Parameter         | Description |
|-------------------|-------------|
| onBoardingID      | Refers to the particular OnBoarding Transaction ID. |
| referenceNo       | Refers to the particular `ref_no` taken from the `IDVerificationStatus` callback function. |
| answers           | Refers to the `AnswerKBA` class. This variable will be used to verify the KBA questions provided to the users. |
| inputActivity     | Activity class that is used for the scanner. |
| callback          | Callback function for KBA Verification. |

### <a name="AnswerKBA"></a> AnswerKBA Class Details
This class will be used to verify the answer provided by the user to the KBA questions.
```java
/** The Question ID will be provided from `questionObject` passed from the `KBARequestStatus` callback function. */
public void setQuestionID(String questionID);
public String getQuestionID();
/** Answer of the Question is in Boolean format. */
public void setAnswer(boolean answer);
public String getAnswer();
```

### <a name="XendityKBACallback"></a> XendityKBACallback callback functions
---
```java
public void IDVerificationStatus(int status, JSONObject profileObject, String errorMessage);
```
<b>Description:</b>
Callback function that provides ID Verification status<br>
<b>Parameters:</b>
* status : Status Code passed from ID Verification Status.
Below shows the details of the param `Status` value.

| Parameter | Description |
|-----------|-------------|
| 300       | Record Found and Match. The particular OnBoarding ID is found in the CTOS Cloud Database Record with matched result. |
| 400       | Record Found and Not Match. The particular OnBoarding ID is found but is not macthed with the results. Possible fraud case. |
| 500       | Record Not found. The particular OnBoarding ID is not found on any of the Server Records. Possibility of Foreign User or Fresh User who has clean slate of financial record. |
| 109       | Service not available. CCRIS Server or CTOS Server might be unavailable at the moment. |

* profileObject : Contains the details of the ID Verification Status. Refer to the sample JSON below for details.
```json
{
    "name_check": "Found and Match",
    "ref_no": "1578887797492140706",
    "ref_id": "NjEwMzJlYTYzNWU2NzkzY2ZmODMyOTg2NzdlMTE2YWE=",
    "external_source": [
      {
        "source": "CCRIS",
        "nic_br": "1234567890",
        "name": "Test Account",
        "name_match": "100.0",
        "address": "W.P. KUALA LUMPUR",
        "address_match": "-",
        "source_date": "2020-01-13"
      },
      {
        "source": "CTOS",
        "nic_br": "1234567890",
        "name": "Test Account",
        "name_match": "100.0",
        "address": ",,,,,",
        "address_match": "-",
        "source_date": []
      }
    ],
    "status": "Successfully fetched the result"
}
```
* errorMessage : Error passed from processing ID.
---
```java
public void KBARequestStatus(JSONArray questionObject, String errorMessage);
```
<b>Description:</b>
Callback function that provides meta Face Match Results (questionObject, errorMessage) from the Face Match Process<br>
<b>Parameters:</b>
* questionObject : Contains the details of the questions that provide verification purpose for users. Refer to the sample JSON below for details.
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
* errorMessage : Error passed from requesting KBA.
---
```java
public void KBAVerificationStatus(int totalCorrect, String errorMessage);
```
<b>Description:</b>
Callback function that provide results of the KBA Verification<br>
<b>Parameters:</b>
* totalCorrect : The number of correct answers submitted by the users.
* errorMessage : Error passed from verifying answers.

### <a name="ErrorCode"></a> Possible Error Codes generated by SDKs
Below show the list of Error Codes that will pass back to the App based on the number of fallback testing.
Please note that the Error Code structure starts with the Error Code followed by description of the error code with single dash as it's separator.
The vertical bar in the error code description represents alternative description of the error.
```java
SDK_RESPONSE_TOKEN_ERROR = "300-Unable to Require Access Token. Please try again later.";
SDK_RESPONSE_LICENSE_ERROR = "301-Unable to initialise SDK License based on the inputted License.";
SDK_RESPONSE_NO_AUTO_FOCUS = "302-Camera Hardware has not Auto Focus Supported.";
SDK_RESPONSE_NO_CAMERA_SUPPORT = "303-No Access to Camera is detected.";
SDK_RESPONSE_UNKNOWN_ERROR = "304-Unknown Error in initialising SDK.";

SDK_RESPONSE_PRE_DEPLOY_ERROR = "305-Unable to submit initial data for text similarity.";
SDK_RESPONSE_IMAGE_CREATION = "306-Unable to upload %s Image to server for processing.";
SDK_RESPONSE_IMAGE_MISSING = "307-%s Image was not captured correctly. Please try again.";

SDK_RESPONSE_LANDMARK_ERROR = "308-Unable to process Landmark Details from ID Card.";
SDK_RESPONSE_IC_NUMBER_MISSING = "309-Unable to capture IC Number. Please scan again.";
SDK_RESPONSE_SCANNER_RESULTS_ERROR = "310-Unable to process Scanning Results from SDKs.";
SDK_RESPONSE_SAVE_DATA_ERROR = "311-Unable to commit Scanner Result to Server.";

SDK_RESPONSE_FACE_REFERENCE_MISSING = "312-Missing Reference Image to be compared against Selfie.";
SDK_RESPONSE_FACE_MATCH_ERROR = "313-Unable to process Selfie Image for Face Match.";
SDK_RESPONSE_FACE_LIVENESS_ERROR = "314-Unable to process Face Liveness.";
SDK_RESPONSE_SAVE_FACE_ERROR = "315-Unable to commit Face Match Result to Server.";

SDK_RESPONSE_BARCODE_ERROR = "316-Unable to process Barcode Image.";
SDK_RESPONSE_SIGNATURE_ERROR = "317-Unable to process Signature Image.";

SDK_RESPONSE_VERIFY_ID_ERROR = "318-Unable to Verify ID in the Server. Please try again later.";
SDK_RESPONSE_KBA_REQUEST_ERROR = "319-Unable to Request KBA from the Server. Please try again later.";
SDK_RESPONSE_KBA_VERIFY_ERROR = "320-Unable to Verify KBA in the Server. Please try again later.";

SDK_RESPONSE_CLASS_ERROR = "400-Inputted Class is not Instance of %s.";
SDK_RESPONSE_NO_ACCESS = "401-No Access Granted to %s. Please contact Xendity Admin.";
SDK_RESPONSE_LICENSE_EXPIRY = "402-API Key License Expired. Please contact Xendity Admin.";
SDK_RESPONSE_RETRY_REACHED = "404-Maximum Number of Retry for this feature has been reached.";
SERVER_RESPONSE_HOLOGRAM_MISMATCHED = "406-Hologram Server have detected possible different MyKad submitted for this Session.";
SDK_RESPONSE_BILLING_ERROR = "407-Unable to record %s Transaction. Please try again later.";
SERVER_RESPONSE_HOLOGRAM_EXPIRED = "408-Hologram Server Session Expired.";
SERVER_RESPONSE_HOLOGRAM_UNKNOWN_ERROR = "409-Hologram Server Produce Unknown Error. ";

SDK_RESPONSE_HOLOGRAM_ERROR = "4101-Error Processing Hologram Image.";
SDK_RESPONSE_POSSIBLE_OLD = "4102-Hologram checks show high probability of Old MyKad being detected.";
SDK_RESPONSE_FACE_NOT_COMPARABLE = "4103-MyKad's Cropped Face is not comparable against itself.";

SERVER_RESPONSE_NETWORK_FAIL = "500-Server Response is Fatal.|Internal Server Error.";
SERVER_RESPONSE_FAIL_MESSAGE = "501-Fail Response by Server.|Refer to Debug Logs.";
SERVER_RESPONSE_FAIL_JSON = "502-Decrypted Response from Server is not JSON format.";
SERVER_REQUEST_FAIL_JSON = "503-Unable to create JSON Request.|Unable to encrypt request body.";
SDK_RESPONSE_POSSIBLE_ROOT = "525-Possible Root Device.";
```

## <a name="MobileApplication"></a> Mobile Application Framework Support for Other Frameworks
Please note that [Xendity](https://xendity.com) does not support nor encourage the use of other Mobile Application Framework, such as React Native, Angular JS (and its mobile support framework), Appcelerator, and so on, to implement this SDK. Should the Project Requirements requires the use of Mobile Application Framework to build the App, the developers are **required** to build their own wrapper or middleware (A type of interface to interact with this SDK) at their own risk. The support of this SDK will be limited to only for **Native Android (Java/Kotlin) or iOS (Objective-C/Swift)** language support only.
