# POSITIVE-PAY iOS SDK
![version](https://img.shields.io/badge/version-v1.0.0-blue) ```Online```

![version](https://img.shields.io/badge/version-v2.0.0-blue) ```Offline```


The Positive pay iOS SDK is a real-time MICR code capture for bank cheques in iOS.

Features available are :
- MICR Capture.
- Manual Crop.
- Online and Offline MICR capture support.

**Find the changelog and release history at [Here](CHANGELOG.md)**

# Table Of Content

- [Prerequisite](#prerequisite)
- [Requirements](#requirements)
- [Permission](#permission)
- [Installation](#installation)
- [Getting Started](#getting-started)
- [Positive Pay Error Codes](#positivepay-error-codes)
- [Help](#help)

## Prerequisite

You will need a valid license and Netrc credentials to use the Positive Pay SDK, which can be obtained by contacting support@frslabs.com. 

Once you have the license , follow the below instructions for a successful integration of Positive Pay SDK onto your iOS Application.

## Requirements

- Swift 5.0
- iOS 12.0+

## Permission

In Info.plist file add following code to allow your application to access iPhone's camera:
``<key>NSCameraUsageDescription</key>
<string>Allow access to camera</string>``

## Installation

### Cocoapods


You can use [CocoaPods](http://cocoapods.org/) to install `PositivePay` by adding it to your `Podfile`:

```ruby
source 'https://gitlab.com/frslabs-public/ios/positivepay-ios.git'
source 'https://github.com/CocoaPods/Specs.git'
platform :ios, '12.0'
target '<Your Target Name>' do
use_frameworks!

// Online
pod 'PositivePay', '1.0.0' 

//Offline
pod 'PositivePay', '2.0.0' 
pod 'TesseractOCRiOS'

end
```

###### Save/Edit Netrc settings to install custom pod

You will need a valid netrc credentials to install PositivePay from maven, which can be obtained by contacting `support@frslabs.com`. 

1. Create or edit .netrc file under current user's home directory
2. Write the below lines into that file, replace <YOUR_USERNAME> and <YOUR_PASSWORD> with your credentials which is shared through email and save the file.
```ruby
 machine positivepay-ios.repo.frslabs.space
 login <YOUR_USERNAME>
 password <YOUR_PASSOWRD>
```
3. In terminal enter below command to install the pod

   "pod install" or "pod update" or "pod install --repo-update".

4. Connect with physical device to build and run PositivePay, It will not build/run in simulator due to camera dependency.

#### Supported Tessdata installation [Offline]
1. Download and drop ```mcr.traineddata``` and ```eng.traineddata``` in tessdata folder of your project for OCR detection.
2. Congratulations! 

To get the full benefits import `PositivePay` wherever you import UIKit

``` swift
import UIKit
import PositivePay
```

## Getting Started

### Swift

1. Invoke PositivePay Online SDK

```swift
    // ...
    
    override func viewDidAppear(_ animated: Bool) {
            let ocrVC = PositivePayNavigationViewController(delegate: self)
            ocrVC.modalPresentationStyle = .fullScreen
            ocrVC.LICENCE_KEY = "LICENSE_KEY"
            ocrVC.BASE_URL = "BASE_URL"
            ocrVC.PAY_API_CRED1 = "ENTER_API_CRED1"
            ocrVC.PAY_API_CRED2 = "ENTER_API_CRED2"
            ocrVC.numberOfSide = 1 // 1 or 2 based on cheque sides
            present(ocrVC, animated: false)
      }
    // ...    
```
2. Invoke PositivePay Offline SDK

```swift
    // ...
    
    override func viewDidAppear(_ animated: Bool) {
            let ocrVC = PositivePayNavigationViewController(delegate: self)
            ocrVC.modalPresentationStyle = .fullScreen
            ocrVC.LICENCE_KEY = "LICENSE_KEY"
            ocrVC.numberOfSide = 1 // 1 or 2 based on cheque sides
            present(ocrVC, animated: false)
      }
    // ...    
```

3. Handling the result and import delegate PayDelegate

```swift
 class YourViewController: UIViewController,PayDelegate {

 func positivePaySuccessResponse(pay: PositivePayNavigationViewController, didFinishOcrWithResult results: PositivePayResults) {
        print("POSITIVEPAY: RESULT",results.payeeDeatils)  
    }
  func positivePayFailureResponse(pay: PositivePayNavigationViewController, didFailWithError error: String) {
      print("POSITIVEPAY: ERROR",error)
    }
```
  
 ## PositivePay Error Codes

   Following error codes will be returned on the `on didFailWithError` method of the callback

   | CODE | DESCRIPTION                  |
   | ---- | ---------------------------- |
   | 803  | Camera permission denied    |
   | 804  | PositivePay interrupted            |
   | 805  | PositivePay SDK License has expired             |
   | 806  | PositivePay SDK License is invalid             |
   | 807  | Network error               |
   | 808  | Server response failed                  |
   


   Sets the PositivePay SDK apiCredentials . Obtain the appropriate api credentials through a REST API call , for details about     the REST API, contact `support@frslabs.com`


   ## Help
   For any queries/feedback , contact us at `support@frslabs.com` 
