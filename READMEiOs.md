# <a name="XenditySDK"></a> Xendity - iOS
SDK version: 1.0.6<br>
Last updated: Jan 30, 2020

**Xendity SDK for iOS** is SDK that allows the use of ID Scanning Features and Face Match capabilities into Android Applications. This version is an *In-House Version* of the existing [Xenchain SDK for iOS Platform](https://github.com/XenchainIO/xenchain_ios_framework), featuring improvement of Performance and ease of integration in comparison to older version.

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
        <td valign="top" style="white-space: nowrap;">2019-07-25</td>
        <td valign="top">
            <ul>
                <li> Overhaul Xendity SDK for In-House OCR Scanner. </li>
            </ul>
        </td>
    </tr>
    <tr>
        <td valign="top">1.0.1</td>
        <td valign="top" style="white-space: nowrap;">Jovial</td>
        <td valign="top" style="white-space: nowrap;">2019-09-05</td>
        <td valign="top">
            <ul>
                <li> Added `DeployFaceRecord` feature for Liveness Detection. </li>
                <li> Added UI customisation feature for `XFaceRecordViewController`. </li>
            </ul>
        </td>
    </tr>
    <tr>
        <td valign="top">1.0.2</td>
        <td valign="top" style="white-space: nowrap;">Jovial</td>
        <td valign="top" style="white-space: nowrap;">2019-12-20</td>
        <td valign="top">
            <ul>
                <li> Added `DeployFaceMatch` feature for Liveness Detection. </li>
                <li> Added UI customisation feature for `XFaceMatchViewController`. </li>
                <li> Added `setPreDeployment` feature for Text Similarity function. </li>
                <li> Added ID and KBA Verification feature. </li>
                <li> Added `completeScanDeployment` function. </li>
            </ul>
        </td>
    </tr>
    <tr>
        <td valign="top">1.0.3</td>
        <td valign="top" style="white-space: nowrap;">Jovial</td>
        <td valign="top" style="white-space: nowrap;">2020-01-16</td>
        <td valign="top">
            <ul>
                <li> Added `SetPreviewOCR` function for ID Capture Preview. </li>
                <li> Fixed the sensitivity issue on the `DeployFaceMatch` function. </li>
                <li> Added list of `ErrorCode` for SDK fallback function. </li>
            </ul>
        </td>
    </tr>
    <tr>
        <td valign="top">1.0.4</td>
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
        <td valign="top">1.0.5</td>
        <td valign="top" style="white-space: nowrap;">Jovial</td>
        <td valign="top" style="white-space: nowrap;">2020-01-22</td>
        <td valign="top">
            <ul>
                <li> Update the motion of `XFaceMatchViewController` from Blink then Smile to become Smile then Blink. </li>
            </ul>
        </td>
    </tr>
    <tr>
        <td valign="top">1.0.6</td>
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
| Step 0           | Initialize Xendity SDK | [`InitSDK`](#-initialize-xendity-sdk) |
| Step 1           | Implementation of ID Card Reader | [`DeployScanner`](#-implementation-of-id-card-reader) |
| Step 2           | Implementation of Face match feature | [`DeployFaceMatch`](#-implementation-face-match-feature) |
| Step 2           | Implementation of Liveness feature | [`DeployFaceRecord`](#-implementation-liveness-feature) |
| Step 3           | Implementation of KBA Verification related feature | [`IDVerificationForOnBoarding`](#-implementation-kba-verification-related-feature) |
| Step 4           | Implementation of KBA Request for Onboarding.<br />Implementation of KBA Verification for Onboarding. | [`RequestKBAForOnBoarding`](#-implementation-of-kba-request-for-onboarding)<br />[`VerifyKBAForOnBoarding`](#-implementation-of-kba-verification-for-onboarding) |

### <a name="AddSDK"></a> Adding SDK into project
Kindly note that the project requires the use of a real physical iOS Device in order for the SDK to compile and work properly. Otherwise, will result in either compilation error or no access to the camera.<br>
*Step 1*: Download XenditySDK.framework file. Please note that you are required to use **Git LFS** (Git Large File Storage) to download the Frameworks folder. Otherwise, manually download the [XenditySDK](Frameworks/XenditySDK.framework/XenditySDK) file and replace them accordingly as shown below. **Failure to do so will results in App Crash during the `InitSDK` process.** <br>
![Download Xendity](Images/ios_download_xendity.png "Download Xendity")
![Replace Xendity](Images/ios_replace_xendity.png "Replace Xendity")
<br/>

*Step 2*: Import the .framework file into your project
1. Open the project navigator
2. Drag the XenditySDK.framework to your project *Framework physical group folder*
3. In your target settings, add XenditySDK.framework into "Embedded Binaries" section. If any, remove any duplicates of XenditySDK.framework from the "Linked Frameworks and Libraries" section.

## <a name="InitialSetup"></a> Initial Setup
### <a name="ProjectTargetSettings"></a> Project Target Settings Setup
#### <a name="BuildSettingsSetup"></a> Build Settings Setup
Please follow the red oval below to setup for the frameworks which is crucial for scanning ID cards.<br>
![Build Settings](Images/ios_build_search_path.png "Build Settings")

#### <a name="InfoPlistSetup"></a> Info.plist Setup
Kindly add the below configuration setup to allow iOS to bypass the HTTPS checking for Xendity URL. In addition, please setup Privacy – Camera Usage Description and Privacy – Photo Library Usage Description. Please note that the contents of these Privacy Description can be anything. Finally, the key for `apiurl` must be replaced and will be provided by Xendity.
```xml
<key>NSAppTransportSecurity</key>
<dict>
    <key>NSExceptionDomains</key>
    <dict>
        <key>apiurl</key>
        <dict>
            <key>NSExceptionAllowsInsecureHTTPLoads</key>
            <true/>
            <key>NSIncludesSubdomains</key>
            <true/>
        </dict>
    </dict>
</dict>
<key>NSCameraUsageDescription</key>
<string>Capture Face Image of the User for Face Match Feature</string>
<key>NSPhotoLibraryUsageDescription</key>
<string>Upload Image of the User for App Features</string>
```

#### <a name="BuildPhaseSetup"></a> Build Phase Setup
![alt text](Images/ios_build_phase_script.png "Build Phases")<br>
Kindly add the script configuration below to remove all the Device Architecture from the Framework as shown in the image above. Please add the script on the very last of the Build Phase. Failure to do so might result in rejection when uploading to the Apple Store.
```javascript
APP_PATH="${TARGET_BUILD_DIR}/${WRAPPER_NAME}"

# This script loops through the frameworks embedded in the application and

# removes unused architectures.
find "$APP_PATH" -name '*.framework' -type d | while read -r
FRAMEWORK
do
FRAMEWORK_EXECUTABLE_NAME=$(defaults read "$FRAMEWORK/Info.plist" CFBundleExecutable)
FRAMEWORK_EXECUTABLE_PATH="$FRAMEWORK/$FRAMEWORK_EXECUTABLE_NAME"
echo "Executable is $FRAMEWORK_EXECUTABLE_PATH"
EXTRACTED_ARCHS=()
for ARCH in $ARCHS
do
echo "Extracting $ARCH from $FRAMEWORK_EXECUTABLE_NAME"

lipo -extract "$ARCH" "$FRAMEWORK_EXECUTABLE_PATH" -o "$FRAMEWORK_EXECUTABLE_PATH-$ARCH"

EXTRACTED_ARCHS+=("$FRAMEWORK_EXECUTABLE_PATH-$ARCH")
done
echo "Merging extracted architectures: ${ARCHS}"

lipo -o "$FRAMEWORK_EXECUTABLE_PATH-merged" -create "${EXTRACTED_ARCHS[@]}"

rm "${EXTRACTED_ARCHS[@]}"
echo "Replacing original executable with thinned version"
rm "$FRAMEWORK_EXECUTABLE_PATH"
mv "$FRAMEWORK_EXECUTABLE_PATH-merged" "$FRAMEWORK_EXECUTABLE_PATH"
done
```

### <a name="ImportSDK"></a> Import SDK classes
```swift
// For Swift Implementation
import XenditySDK;
```
```objectivec
// For Objective-C Implementation
#import <XenditySDK/XenditySDK.h>;
```

### <a name="InitXenditySDK"></a> Initialize Xendity SDK
Please ensure that you execute the code code first before proceeding to other features of the SDK.
```swift
// For Swift Implementation
XenditySDK.initSDK("SampleAPIKey", apiURL: "SampleAPIURL", completionHandler: XenditySDKCallback)
```
```objectivec
// For Objective-C Implementation
[XenditySDK InitSDK:@"SampleAPIKey" apiURL:@"SampleAPIURL" onPremSaveData:false completionHandler:XenditySDKCallback];
```
| Parameter         | Description |
|-------------------|-------------|
| apiKey            | API Key for activating SDK Features. |
| apiURL            | URL Server Address which can be configured to point to another server should client request private server. The value of this parameter will need to be requested from Xendity Admin.     |
| completionHandler | Callback function for returning the results of `initSDK` function. Refer to  |

### <a name="XenditySDKCallback"></a> XenditySDKCallback callback functions
```swift
// For Swift Implementation
func InitSDKStatus(_ status: Bool, message: String!)
```
```objectivec
// For Objective-C Implementation
- (void)InitSDKStatus:(bool)status message:(NSString *)message;
```
<b>Description:</b>
Callback function that is used to determine the status of the Initialization of XenditySDK<br>
<b>Parameters:</b>
* status : Determines whether the SDK can be used or not.
* message : Contains the error message if the SDK cannot be initialized.

## <a name="SDKConfiguration"></a> Additional SDK configuration
#### <a name="ScanningSound"></a> Custom Scanning Sound
```swift
// For Swift Implementation
XenditySDK.setScanningSound(Bundle(identifier: "com.example.reader")!.bundlePath + "/example_sound.mp3")
```
```objectivec
// For Objective-C Implementation
XenditySDK.scanningSound = [[NSBundle bundleWithIdentifier:@"com.example.reader"].bundlePath stringByAppendingString:@"/example_sound.mp3"]
```
Kindly note that the input must be in String Path format.

#### <a name="LoadingDialogImage"></a> Loading Dialog Image
```swift
// For Swift Implementation
XenditySDK.setLoadingLogo(UIImage())
```
```objectivec
// For Objective-C Implementation
XenditySDK.loadingLogo = [[UIImage alloc] init];
```
Kindly note the input must be in UIImage based format.

#### <a name="CustomLoadingDialog"></a> Custom Loading Dialog
```swift
// For Swift Implementation
XenditySDK.setLoadingView(UIView())
```
```objectivec
// For Objective-C Implementation
XenditySDK.loadingView = [[UIView alloc] init];
```
Kindly note the input must be in `UIView` Data Type format.

## <a name="ImplementationIDCardReader"></a> Implementation of ID Card Reader
### <a name="PreDeployDetails"></a> Pre-Deploy Scanner Details.
This function is optional and is used to provide the App with Text Similarity features. In this case, the function below takes a JSON Input which contains the preliminary user details.
```swift
// For Swift Implementation
XenditySDK.setPreDeployment(userID, inputDetails: NSDictionary, completionHandler: self)
```
```objectivec
// For Objective-C Implementation
[XenditySDK setPreDeployment:(NSString * _Nonnull)userID inputDetails:(NSDictionary * _Nonnull)inputDetails completionHandler:(void (^)(NSString * _Nullable onBoardingID, NSString * _Nullable error))completionHandler;
```
| Parameter     | Description |
|---------------|-------------|
| userID        | Applicable only if the particular onboarding needs to be tied to certain user, otherwise the value is empty string. |
| inputDetails  | A JSON Object that contains the full name and IC Number of the user. Param key for full name is `fullName`. Param key for IC Number is `documentNumber`. |
| callback      | Callback function for PreDeployment Scanning. |

The sample value of `inputDetails` is shown as below.
```json
{
  "fullName": "Test Name",
  "documentNumber": "123456789012"
}
```

### <a name="XCameraViewController"></a> Implementation of Custom Scanner ViewController
Before proceeding to call the `deployScanner` function, the app must have an Extended `XCameraViewController` class, in which the extended class will be used to Scan ID Card. The minimum implementation of the Extended `XCameraViewController` class is shown below.
```swift
/** Sample Swift Class of Extended XCameraViewController */
// Assume that the App has a protocol name PreviewListener (Optional)
class CameraViewController: XCameraViewController, PreviewListener {
    override func viewDidLoad() {
        super.viewDidLoad()
    }

    override func prepareForFrontCapture() {
        print("Xendity Log: Function used to determine that the scanner is ready to capture front ID.")
    }

    override func completeFrontCapture(_ frontImage: UIImage?) {
        print("Xendity Log: Function used to pass captured front ID of the image during Scanner Process.")
    }

    override func prepareForBackCapture() {
        print("Xendity Log: Function used to determine that the scanner is ready to capture back ID.")
    }

    override func completeBackCapture(_ backImage: UIImage?) {
        print("Xendity Log: Function used tor pass captured back ID of the image during Scanner Process.")
    }

    override func processImageFailure(_ errorMessage: String?) {
        print("Xendity Log: %s", errorMessage ?? "")
    }

    /** Function below is optional and only will be called if the `SetPreviewOCR` is set to `true` */
    override func showPreview(_ previewImage: UIImage?) {
        // Do the Preview of the Image captured here.
    }

    /** Function below is optional and only will be called if the `SetPreviewOCR` is set to `true` */
    override func dismissPreview() {
        // Dismiss the Preview here.
    }

    // Assume Protocol `PreviewListener` has this function and the Preview contains the delegate variable of `PreviewListener`
    // Below function will assume that the Preview will call the protocol function.
    func PreviewAction(isRetry: bool) {
        if (isRetry) {
            self.RetryCapture() // Call this function if the User wants to retry for ID Capture.
        } else {
            self.SubmitCapture() // Call this function for ID Capture confirmation.
        }
    }

    @IBAction func startCaptureAction(_ sender: UIButton) {
        // Call 'capturePicture' function to start capture & process image.
        self.capturePicture()
    }
}
```
```objectivec
/** Sample Objective-C Class of Extended XCameraViewController */
// Assume that the App has a protocol name PreviewListener (Optional)
@interface CameraViewController : XCameraViewController <PreviewListener>

@end

@implementation CameraViewController
    - (void)viewDidLoad {
        [super viewDidLoad];
    }

    - (void)prepareForFrontCapture {
        NSLog(@"Xendity Log: Function used to determine that the scanner is ready to capture front ID.");
    }

    - (void)completeFrontCapture:(UIImage *)frontImage {
        NSLog(@"Xendity Log: Function used to pass captured front ID of the image during Scanner Process.");
    }

    - (void)prepareForBackCapture {
        NSLog(@"Xendity Log: Function used to determine that the scanner is ready to capture back ID.");
    }

    - (void)completeBackCapture:(UIImage *)backImage {
        NSLog(@"Xendity Log: Function used tor pass captured back ID of the image during Scanner Process.");
    }

    - (void)processImageFailure:(NSString *)errorMessage {
        NSLog(@"Xendity Log: %@", errorMessage);
    }

    /** Function below is optional and only will be called if the `SetPreviewOCR` is set to `true` */
    - (void)showPreview:(UIImage *)previewImage {
        // Do the Preview of the Image captured here.
    }

    /** Function below is optional and only will be called if the `SetPreviewOCR` is set to `true` */
    - (void)dismissPreview {
        // Dismiss the Preview here.
    }

    // Assume Protocol `PreviewListener` has this function and the Preview contains the delegate variable of `PreviewListener`
    // Below function will assume that the Preview will call the protocol function based on whether to Retry or Continue.
    - (void)PreviewAction:(bool)isRetry {
        if (isRetry) {
            [self RetryCapture]; // Call this function if the User wants to retry for ID Capture.
        } else {
            [self SubmitCapture]; // Call this function for ID Capture confirmation.
        }
    }

    - (IBAction)startCaptureAction:(id)sender {
        // Call 'capturePicture' function to start capture & process image.
        [self capturePicture];
    }
@end
```

### <a name="StartScanID"></a> Start Scan ID CARD
Before calling the `DeployScanner`, the App may enable the `SetPreviewOCR` which will allows the Scanner to call `showPreview` function for the App to preview the image before being submitted for OCR Process.
```swift
// For Swift Implementation
XenditySDK.SetPreviewOCR(true);
```
```objectivec
// For Objective-C Implementation
[XenditySDK SetPreviewOCR:true];
```

Below shows the `DeployScanner` that will be used to initiate the Scanner for ID Card Scanning.
```swift
// For Swift Implementation
XenditySDK.DeployScanner(inputOCRType, inputController: self, extendedController: self.storyboard!.instantiateViewController(withIdentifier: "CameraViewController"), completionHandler: self)
```
```objectivec
// For Objective-C Implementation
[XenditySDK DeployScanner:inputOCRType inputController:self extendedController:[self.storyboard instantiateViewControllerWithIdentifier:@"CameraViewController"] completionHandler:self];
```
| Parameter          | Description |
|--------------------|-------------|
| inputOCRType       | The value that determines the document types to be expected by the Scanner. Refer to [OCR Type](#OCRType) for list of available scan types. |
| inputController    | ViewController class that is used to call the scanner. |
| extendedController | The extended `XCameraViewController` class that is used as overlay for the Camera ViewController. Value can be `nil` for default UI. |
| completionHandler  | Callback function for ID Scanning. |

Kindly note that the code below is required to be executed after the `successCallback` function being called. Otherwise, for each scanning, the SDK will charged (billed) the scan and in on-premise server case, no data will be passed to the server.
```swift
// For Swift Implementation
XenditySDK.completeScanDeployment(onBoardingID, metaCardResult: mMetaCardResults, cardResult: rawOCRResults, inputOCRType: inputOCRType, completionHandler: self)
```
```objectivec
// For Objective-C Implementation
[XenditySDK CompleteScanDeployment:onBoardingID metaCardResult:mMetaCardResults cardResult:rawOCRResults inputOCRType:inputOCRType completionHandler:self];
```
| Parameter            | Description                                                                       |
|----------------------|-----------------------------------------------------------------------------------|
| onBoardingID         | The Overall Transaction ID for the whole Onboarding Process.                      |
| metaCardResult       | Refers to all the meta results passed from the `XendityScannerCallback` protocol. |
| cardResult           | Refers to the `rawOCRResults` passed from the `XendityScannerCallback` protocol.  |
| inputOCRType         | Refers to the existing `inputOCRType` used in the `deployScanner` function.       |
| completionHandler    | Callback function for ID Scanning.                                                |

The value of `metaCardResult` is shown as below.
```json
{
  "idFrontImage": "Taken From frontdocImage",
  "refFrontID": "Taken From refFrontDocImage",
  "idBackImage": "Taken From backDocImage",
  "refBackID": "Taken From refBackDocImage",
  "idFaceImage": "Taken From idFaceImage",
  "refFace": "Taken From refFaceImage",
}
```

### <a name="XendityScannerCallback"></a> XendityScannerCallback callback functions
---
```swift
// For Swift Implementation
func scanResults(_ rawOCRResults: NSDictionary!, onBoardingID: String!, errorMessage: String!)
```
```objectivec
// For Objective-C Implementation
- (void)ScanResults:(NSDictionary *)rawOCRResults onBoardingID:(NSString *)onBoardingID errorMessage:(NSString *)errorMessage;
```
<b>Description:</b>
Callback function that provides Scanning Results from ID Scanning Process<br>
<b>Parameters:</b>
* rawOCRResults : Result card info from the reader.
* onBoardingID : The Overall Transaction ID for the whole Onboarding Process.
* errorMessage : Error passed from processing ID Card result.
---
```swift
// For Swift Implementation
func ScanMetaDocFrontResults(frontdocImage: UIImage!, refFrontDocImage: String!, errorMessage: String!)
```
```objectivec
// For Objective-C Implementation
- (void)ScanMetaDocFrontResults:(UIImage *)frontdocImage refFrontDocImage:(NSString *)refFrontDocImage errorMessage:(NSString *)errorMessage;
```
<b>Description:</b>
Callback function that provides Meta Scan Results from ID Scanning Process<br>
<b>Parameters:</b>
* frontdocImage : The Front ID Card Image from ID Scanner.
* refFrontDocImage : The reference Front ID of the ID Card Image.
* errorMessage : Error passed from processing ID Card result.
---
```swift
// For Swift Implementation
func ScanMetaDocBackResults(backDocImage: UIImage!, refBackDocImage: String!, errorMessage: String!)
```
```objectivec
// For Objective-C Implementation
- (void)ScanMetaDocBackResults:(UIImage *)backDocImage refBackDocImage:(NSString *)refBackDocImage errorMessage:(NSString *)errorMessage;
```
<b>Description:</b>
Callback function that provides Meta Scan Results from ID Scanning Process<br>
<b>Parameters:</b>
* backDocImage : The Back ID Card Image from ID Scanner.
* refBackDocImage : The reference Back ID of the ID Card Image.
* errorMessage : Error passed from processing ID Card result.
---
```swift
// For Swift Implementation
func ScanMetaDocFaceResults(_ idFaceImage: UIImage!, refFace: String!, errorMessage: String!)
```
```objectivec
// For Objective-C Implementation
- (void)sSanMetaDocFaceResults:(UIImage *)idFaceImage refFaceImage:(NSString *)refFaceImage errorMessage:(NSString *)errorMessage;
```
<b>Description:</b>
Callback function that provides Meta Scan Results from ID Scanning Process<br>
<b>Parameters:</b>
* idFaceBitmap : Refers to Cropped Face Image from ID Card Image.
* refFaceImage : The reference ID of the Cropped Face Image.
* errorMessage : Error passed from processing ID Card result.
---
```swift
// For Swift Implementation
func ScanSimilarityResults(_ nameIsSimilar: bool!, _ documentNoIsSimilar: bool!, _ frontBackIsSimilar: bool!)
```
```objectivec
// For Objective-C Implementation
- (void)ScanSimilarityResults:(bool)nameIsSimilar documentNoIsSimilar:(bool)documentNoIsSimilar frontBackIsSimilar:(bool)frontBackIsSimilar;
```
<b>Description:</b>
Callback function that provides Text Similarity features. Only applicable if the app has executed `setPreDeployment` function. Used to determine the legitimacy of the ID Card.<br>
<b>Parameters:</b>
* nameIsSimilar : Show whether the name obtained from Scanner is similar to the value submitted in `setPreDeployment` function.
* documentNoIsSimilar : Show whether the document number obtained from Scanner is similar to the value submitted in `setPreDeployment` function.
* frontBackIsSimilar : Show whether the front ID and back ID is similar. Only applicable for MyKad Scanning.
---
```swift
// For Swift Implementation
func ScanLandmarkInformation(_ landmarkScores: [AnyHashable : Any]!)
```
```objectivec
// For Objective-C Implementation
- (void)ScanLandmarkInformation:(NSDictionary *)landmarkScores;
```
<b>Description:</b>
Callback function that provides the Landmark Scores of the ID Cards. Used to determine the legitimacy of the ID Card.<br>
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
```swift
// For Swift Implementation
func ScanServiceReferenceID(_ serviceReferenceID: String!, errorMessage: String!)
```
```objectivec
// For Objective-C Implementation
- (void)ScanServiceReferenceID:(NSString *)serviceReferenceID errorMessage:(NSString *)errorMessage;
```
<b>Description:</b>
Callback function that is called for each OCR Scanning.<br>
<b>Parameters:</b>
* serviceReferenceID : Billing reference is returned if all the important attributes of the ID Card are returned successfully during the scanning process.
* errorMessage : Error passed from processing ID Card result.
---
```swift
// For Swift Implementation
func ScanCompleteDeployment(_ status: Bool, errorMessage: String!)
```
```objectivec
// For Objective-C Implementation
-(void) ScanCompleteDeployment:(bool)status errorMessage:(NSString *)errorMessage;
```
<b>Description:</b>
Callback function that is called when the Scanning has been charged (billed) completely.<br>
<b>Parameters:</b>
* status : Represents whether the `completeScanDeployment` is successfully called or not.
* errorMessage : Error passed from processing `completeScanDeployment`.

### <a name="OCRType"></a> Scanning Types
This Scanning Types determines the OCR Results being produced from the Scanner.

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
```objectivec
@property (nonatomic, strong) NSString* mDocumentType;
```
<b>Description:</b><br>
Get document type from ID Card.

---
```objectivec
@property (nonatomic, strong) NSString* mDocumentNumber;
```
<b>Description:</b>
Get document ID Number from ID Card.

---
```objectivec
@property (nonatomic, strong) NSString* mCardNumber;
```
<b>Description:</b>
Get ID card Number for the Passport.

---
```objectivec
@property (nonatomic, strong) NSString* mArmyNumber;
```
<b>Description:</b>
Get Army Number from ID Card.

---
```objectivec
@property (nonatomic, strong) NSString* mBackDocumentNumber;
```
<b>Description:</b>
Get document ID Number from Back ID Card.

---
```objectivec
@property (nonatomic, strong) NSString* mFrontName;
```
<b>Description:</b>
Get Name from Front ID Card.

---
```objectivec
@property (nonatomic, strong) NSString* mBackName;
```
<b>Description:</b>
Get Name from Back ID Card.

---
```objectivec
@property (nonatomic, strong) NSString* mBloodType;
```
<b>Description:</b>
Get blood type from ID Card.

---
```objectivec
@property (nonatomic, strong) NSString* mAddress;
```
<b>Description:</b>
Get address from ID Card.

---
```objectivec
@property (nonatomic, strong) NSString* mVillage;
```
<b>Description:</b>
Get village from ID Card (Only in Indonesia eKTP).

---
```objectivec
@property (nonatomic, strong) NSString* mRTRW;
```
<b>Description:</b>
Get RT/RW from ID Card (Only in Indonesia eKTP).

---
```objectivec
@property (nonatomic, strong) NSString* mDistrict;
```
<b>Description:</b>
Get district from ID Card (Only in Indonesia eKTP).

---
```objectivec
@property (nonatomic, strong) NSString* mCity;
```
<b>Description:</b>
Get city from ID Card.

---
```objectivec
@property (nonatomic, strong) NSString* mProvince;
```
<b>Description:</b>
Get province from ID Card (Only in Indonesia eKTP).

---
```objectivec
@property (nonatomic, strong) NSString* mReligion;
```
<b>Description:</b>
Get religion status from ID Card.

---
```objectivec
@property (nonatomic, strong) NSString* mStatus;
```
<b>Description:</b>
Get marital status from ID Card.

---
```objectivec
@property (nonatomic, strong) NSString* mJob;
```
<b>Description:</b>
Get job from ID Card.

---
```objectivec
@property (nonatomic, strong) NSString* mGender;
```
<b>Description:</b>
Get gender from ID Card.

---
```objectivec
@property (nonatomic, strong) NSString* mCitizenship;
```
<b>Description:</b>
Get citizenship from ID Card.

---
```objectivec
@property (nonatomic, strong) NSString* mNationality;
```
<b>Description:</b>
Get nationality from ID Card.

---
```objectivec
@property (nonatomic, strong) NSString* mRace;
```
<b>Description:</b>
Get race from ID Card.

---
```objectivec
@property (nonatomic, strong) NSString* mPlaceOfBirth;
```
<b>Description:</b>
Get place of birth from ID Card.

---
```objectivec
@property (nonatomic, strong) NSString* mDateOfBirth;
```
<b>Description:</b>
Get date of birth from ID Card.

---
```objectivec
@property (nonatomic, strong) NSString* mCountryOfBirth;
```
<b>Description:</b>
Get country of birth from ID Card.

---
```objectivec
@property (nonatomic, strong) NSString* mFrontDateIssued;
```
<b>Description:</b>
Get date of issued from front ID Card.

---
```objectivec
@property (nonatomic, strong) NSString* mBackDateIssued;
```
<b>Description:</b>
Get date of issued from Back ID Card.

---
```objectivec
@property (nonatomic, strong) NSString* mDateUpdated;
```
<b>Description:</b>
Get date of updated from ID Card.

---
```objectivec
@property (nonatomic, strong) NSString* mFrontExpiry;
```
<b>Description:</b>
Get date of expiry from front ID Card.

---
```objectivec
@property (nonatomic, strong) NSString* mBackExpiry;
```
<b>Description:</b>
Get date of expiry from Back ID Card.

---
```objectivec
@property (nonatomic, strong) NSString* mChipNumber;
```
<b>Description:</b>
Get chip number from ID card.

---
```objectivec
@property (nonatomic, strong) NSString* mSerialNumber;
```
<b>Description:</b>
Get Serial Number from ID Card

---
```objectivec
@property (nonatomic, strong) NSString* mEmployerInfo;
```
<b>Description:</b>
Get Employer Info from ID Card (Only in Singapore PASS or Work Permit).

---
```objectivec
@property (nonatomic, strong) NSString* mSector;
```
<b>Description:</b>
Get Employer Sector from ID Card (Only in Singapore PASS or Work Permit).

---
```objectivec
@property (nonatomic, strong) NSString* mEmploymentOccupation;
```
<b>Description:</b>
Get Employment Occupation from ID Card (Only in Singapore PASS or Work Permit).

---
```objectivec
@property (nonatomic, strong) NSString* mDateOfApplication;
```
<b>Description:</b>
Get Date of Application from ID Card (Only in Singapore PASS or Work Permit).

---
```objectivec
@property (nonatomic, strong) NSString* mForeignIdentificationNo;
```
<b>Description:</b>
Get Foreign Identification No from ID Card (Only in Singapore PASS or Work Permit).

---
```objectivec
@property (nonatomic, strong) NSString* mFacultyInfo;
```
<b>Description:</b>
Get Faculty Information from ID Card (Only in Singapore PASS or Work Permit).

---
```objectivec
@property (nonatomic, strong) NSString* mFacultyCityZipcodeState;
```
<b>Description:</b>
Get Faculty City Zip Code State from ID Card (Only in Singapore PASS or Work Permit).

---
```objectivec
@property (nonatomic, strong) NSString* mFacultyAddress;
```
<b>Description:</b>
Get Faculty Address from ID Card (Only in Singapore PASS or Work Permit).

---

## <a name="ImplementationFaceMatch"></a> Implementation Face Match feature
### <a name="XFaceRecordViewController"></a> Implementation of Custom Face Match Activity
Before proceeding to call the `DeployFaceMatch` function, the app must have an Extended `XFaceMatchViewController` class, in which the extended class will be used to process Liveness video. The minimum implementation of the Extended `XFaceMatchViewController` class is shown below.
```swift
/** Sample Swift Class of Extended XFaceMatchViewController */
class FaceMatchViewController: XFaceMatchViewController {
    override func viewDidLoad() {
        super.viewDidLoad()
    }

    override func viewDidAppear(_ animated: bool) {
        super.viewDidAppear(animated)

        // Call this function to start the Face Match
        self.startFaceMatch();
    }

    override func preSmileDetection() {
        print("This function is called to tell the App that the Scanner is ready to detect Smile.")
    }

    override func smileDetected() {
        print("This function is called when the Scanner has detected Smile.")
    }

    override func processingSmile() {
        print("This function is called to tell the App that the Scanner is processing Smile picture.")
    }

    override func preBlinkDetection() {
        print("This function is called to tell the App that the Scanner is ready to detect Blink Eye.")
    }

    override func blinkDetected() {
        print("This function is called when the Scanner has detected Eye Blink.")
    }

    override func processingBlink() {
        print("This function is called to tell the App that the Scanner is processing Eye Blink picture.")
    }

    override func completingFaceMatchProcess() {
        print("This function is called when the Scanner is about to complete the Face Match Process.")
    }
}
```
```objectivec
/** Sample Objective-C Class of Extended XFaceMatchViewController */
@interface FaceMatchViewController : XFaceMatchViewController

@end

@implementation FaceMatchViewController
    - (void)viewDidLoad {
        [super viewDidLoad];
    }

    - (void)viewDidAppear:(BOOL)animated {
        [super viewDidAppear:animated];

        // Call this function to start the Face Match
        [self startFaceMatch];
    }

    -(void) preSmileDetection {
        NSLog(@"This function is called to tell the App that the Scanner is ready to detect Smile.");
    }

    -(void) smileDetected {
        NSLog(@"This function is called when the Scanner has detected Smile.");
    }

    -(void) processingSmile {
        NSLog(@"This function is called to tell the App that the Scanner is processing Smile picture.");
    }

    -(void) preBlinkDetection {
        NSLog(@"This function is called to tell the App that the Scanner is ready to detect Blink Eye.");
    }

    -(void) blinkDetected {
        NSLog(@"This function is called when the Scanner has detected Eye Blink.");
    }

    -(void) processingBlink {
        NSLog(@"This function is called to tell the App that the Scanner is processing Eye Blink picture.");
    }

    -(void) completingFaceMatchProcess {
        NSLog(@"This function is called when the Scanner is about to complete the Face Match Process.");
    }
@end
```

### <a name="StartFaceMatch"></a> Start Face Match Function
Kindly note that ID Scan Feature must be implemented and executed first before proceeding to Face Match Feature.
```swift
// For Swift Implementation
XenditySDK.DeployFaceMatch(self, onBoardingID: mOnBoardingID, imageRef: mRefFaceImage, inputController: self, extendedController: self.storyboard!.instantiateViewController(withIdentifier: "FaceMatchViewController"), completionHandler: self)
```
```objectivec
// For Objective-C Implementation
[XenditySDK DeployFaceMatch:self onBoardingID:mOnBoardingID imageRef:mRefFaceImage inputController:self extendedController:[self.storyboard instantiateViewControllerWithIdentifier:@"FaceMatchViewController"] completionHandler:self];
```
| Parameter         |  Description                                                        |
|--------------------|--------------------------------------------------------------------|
| onBoardingID       | Refers to the particular OnBoarding Transaction ID.                |
| imageRef           | The reference ID of the `refFace` from `scanMetaResults` function. |
| inputController    | ViewController class that is used to call the scanner. |
| extendedController | The extended `XFaceMatchViewController` class that is used as overlay for the Camera ViewController. |
| completionHandler  | Callback function for ID Scanning. |
| completionHandler  | Callback function for Face Match Scanning.                         |

## <a name="ImplementationLiveness"></a> Implementation Liveness feature
### <a name="XFaceRecordViewController"></a> Implementation of Custom Face Record Activity
Before proceeding to call the `deployFaceRecord` function, the app must have an Extended `XFaceRecordViewController` class, in which the extended class will be used to process Liveness video. The minimum implementation of the Extended `XFaceRecordViewController` class is shown below.
```swift
/** Sample Swift Class of Extended XFaceRecordViewController */
class FaceRecordViewController: XFaceRecordViewController {
    override func viewDidLoad() {
        super.viewDidLoad()
    }

    override func processImageFailure(_ errorMessage: String?) {
        print("Xendity Log: %s", errorMessage ?? "")
    }

    @IBAction func startRecordAction(_ sender: UIButton) {
        // Call 'startVideoRecord' function to start record & process video.
        self.startVideoRecord()
    }
}
```
```objectivec
/** Sample Objective-C Class of Extended XFaceRecordViewController */
@interface FaceRecordViewController : XFaceRecordViewController

@end

@implementation FaceRecordViewController
    - (void)viewDidLoad {
        [super viewDidLoad];
    }

    - (void)processImageFailure:(NSString *)errorMessage {
        NSLog(@"Xendity Log: %@", errorMessage);
    }

    - (IBAction)startRecordAction:(id)sender {
        // Call 'startVideoRecord' function to start record & process video.
        [self startVideoRecord];
    }
@end
```

### <a name="StartFaceRecord"></a> Start Face Record Function
Kindly note that ID Scan Feature must be implemented and executed first before proceeding to Face Record / Liveness Feature.
```swift
// For Swift Implementation
XenditySDK.DeployFaceRecord(onBoardingID, inputController: self, extendedController: self.storyboard!.instantiateViewController(withIdentifier: "FaceRecordViewController"), completionHandler: self)
```
```objectivec
// For Objective-C Implementation
[XenditySDK DeployFaceRecord:onBoardingID inputController:self extendedController:[self.storyboard instantiateViewControllerWithIdentifier:@"FaceRecordViewController"] completionHandler:self];
```
| Parameter          | Description |
|--------------------|-------------|
| onBoardingID       | Refers to the particular OnBoarding Transaction ID. |
| inputController    | ViewController class that is used to call the scanner. |
| extendedController | The extended `XFaceRecordViewController` class that is used as overlay for the Camera ViewController. Value can be `nil` for default UI. |
| completionHandler  | Callback function for ID Scanning. |
| callback           | Callback function for Face Match Scanning. |

### <a name="XendityFaceCallback"></a> XendityFaceCallback callback functions
---
```swift
// For Swift Implementation
func faceMatchResult(_ isMatched: Bool, percentMatched: Double, error: String!)
```
```objectivec
// For Objective-C Implementation
- (void)FaceMatchResult:(bool)isMatched percentMatched:(double)percentMatched error:(NSString *)error;
```
<b>Description:</b>
Callback function that provides Face Match Results (isMatched, percentMatched, error) from Face Match Process<br>
<b>Parameters:</b>
* isMatched : True for Matched Face. Otherwise, False.
* percentMatched : Percentage of Face Matching.
* error : Error passed from processing Face Match result.
---
```swift
// For Swift Implementation
func faceMatchMetaResult(_ outputImage: UIImage!, outputRef: String!)
```
```objectivec
// For Objective-C Implementation
- (void)FaceMatchMetaResult:(UIImage *)outputImage outputRef:(NSString *)outputRef;
```
<b>Description:</b>
Callback function that provides meta Face Match Results (outputBitmap, outputRef) from Face Match Process<br>
<b>Parameters:</b>
* outputBitmap : The Face Image captured during Face Match Process.
* outputRef : The reference ID of the image captured.

## <a name="ImplementationKBAVerification"></a> Implementation KBA Verification related feature.
### <a name="IDVerification"></a> Implementation of ID Verification for KBA Verification
Kindly note that ID Scan Feature must be implemented and executed first before proceeding to ID Verification feature.
```swift
// For Swift Implementation
XenditySDK.IDVerificationForOnBoarding(mOnBoardingID, completionHandler: self)
```
```objectivec
// For Objective-C Implementation
[XenditySDK IDVerificationForOnBoarding:mOnBoardingID completionHandler:self];
```
| Parameter         | Description                                                                                  |
|-------------------|----------------------------------------------------------------------------------------------|
| onBoardingID      | Refers to the particular OnBoarding Transaction ID.                                          |
| completionHandler | Callback function for KBA Verification.                                                      |

### <a name="KBARequest"></a> Implementation of KBA Request for Onboarding.
Kindly note that ID Scan Feature & ID Verification Feature must be implemented and executed first before proceeding to KBA Request. This feature will be used to provide questions for the user to answer.
```swift
// For Swift Implementation
XenditySDK.RequestKBAForOnBoarding(mOnBoardingID, referenceNo:mReferenceNo, completionHandler: self)
```
```objectivec
// For Objective-C Implementation
[XenditySDK RequestKBAForOnBoarding:mOnBoardingID referenceNo:mReferenceNo completionHandler:self];
```
| Parameter         | Description                                                                                  |
|-------------------|----------------------------------------------------------------------------------------------|
| onBoardingID      | Refers to the particular OnBoarding Transaction ID.                                          |
| referenceNo       | Refers to the particular `ref_no` taken from the `IDVerificationStatus` callback function.   |
| callback          | Callback function for KBA Verification.                                                      |

### <a name="KBAVerification"></a> Implementation of KBA Verification for Onboarding.
Kindly note that ID Scan Feature, ID Verification Feature, & KBA Request Feature must be implemented and executed first before proceeding to KBA Verification.
```swift
// For Swift Implementation
XenditySDK.VerifyKBAForOnBoarding(mOnBoardingID, referenceNo:mReferenceNo, answers:mAnswers, completionHandler: self)
```
```objectivec
// For Objective-C Implementation
[XenditySDK VerifyKBAForOnBoarding:mOnBoardingID referenceNo:mReferenceNo answers:mAnswers completionHandler:self];
```
| Parameter         | Description |
|-------------------|-------------|
| onBoardingID      | Refers to the particular OnBoarding Transaction ID. |
| referenceNo       | Refers to the particular `ref_no` taken from the `IDVerificationStatus` callback function. |
| answers           | Refers to the `AnswerKBA` class. This variable will be used to verify the KBA questions provided to the users. |
| inputActivity     | Activity class that is used for the scanner. |
| callback          | Callback function for KBA Verification. |

### <a name="AnswerKBA"></a> AnswerKBA Class Details
This class will be used to verify the answers provided by the user to the KBA questions.
```swift
// For Swift Implementation
/** The Question ID will be provided from `questionObject` passed from the `KBARequestStatus` callback function. */
func setQuestionID(_ value :String)
func getQuestionID() ->  String?
/** Answer of the Question is in Boolean format. */
func setAnswer(_ value :Bool)
func getAnswer() -> String?
```
```objectivec
// For Objective-C Implementation
/** The Question ID will be provided from `questionObject` passed from the `KBARequestStatus` callback function. */
- (void)setQuestionID:(NSString * _Nonnull)value;
- (NSString * _Nullable)getQuestionID;
/** Answer of the Question is in Boolean format. */
- (void)setAnswer:(bool)value;
- (NSString * _Nullable)getAnswer;
```

### <a name="XendityKBACallback"></a> XendityKBACallback callback functions
---
```swift
// For Swift Implementation
func IDVerificationStatus(_status: int, _ profileObject: NSDictionary!, errorMessage: String!)
```
```objectivec
// For Objective-C Implementation
-(void) IDVerificationStatus:(int)status profileObject:(NSDictionary *)profileObject errorMessage:(NSString *)errorMessage
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
```swift
// For Swift Implementation
func KBARequestStatus(_ questionObject: NSDictionary!, errorMessage: String!)
```
```objectivec
// For Objective-C Implementation
-(void) KBARequestStatus:(NSDictionary *)questionObject errorMessage:(NSString *)errorMessage
```
<b>Description:</b>
Callback function that provides meta Face Match Results from Face Match Process<br>
<b>Parameters:</b>
* questionObject : Contains the details of the questions that has to be answered by the user. Refer to the sample JSON below for details.
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
```swift
// For Swift Implementation
func KBAVerificationStatus(_ totalCorrect: Int, errorMessage: String!)
```
```objectivec
// For Objective-C Implementation
-(void) KBAVerificationStatus:(int)totalCorrect errorMessage:(NSString *)errorMessage
```
<b>Description:</b>
Callback function that provide results of the KBA Verification<br>
<b>Parameters:</b>
* totalCorrect : The number of correct answers submitted by the user.
* errorMessage : Error passed from verifying answers.

### <a name="ErrorCode"></a> Possible Error Codes generated by SDKs
Below show the list of Error Codes that will pass back to the App based on the number of fallback testing.
Please note that the Error Code structure starts with the Error Code followed by description of the error code with dash as it's separator.
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
