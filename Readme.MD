# Usabilla for Apps - iOS SDK
Usabilla for Apps allows you to collect feedback from your user with great ease and flexibility.

Take a look at our [Wiki](https://github.com/usabilla/usabilla-u4a-ios-sdk/wiki) for a complete and in depth guide on how to install and customize the SDK.

## Requirements

- iOS 9.0+ 
- Xcode 8.0+
- Swift 3.0+

For older versions of iOS you can use v2.3.0 of the SDK.

## Dependencies

The SDK depends on the following libraries:

- Alamofire	~> 4.0.0
- PromiseKit/CorePromise	~> 4.0.0
- PromiseKit/UIKit	~> 4.0.0


## Installation 

### CocoaPods

The Usabilla SDK is available on [CocoaPods](http://cocoapods.org). You can install cocoapods the following way:

```bash
$ gem install cocoapods
```


To use the SDK in your project, specify it in your `Podfile`:

```ruby
source 'https://github.com/CocoaPods/Specs.git'
platform :ios, '9.0'
use_frameworks!

target 'MyApp' do
    pod 'UsabillaFeedbackForm', '~> 3.0'
end
```

Then, run the following command:

```bash
$ pod install
```

## How to get started

### On the web
- Create a new form on your [Usabilla](https://app.usabilla.com/member/) Live for Apps section.
- Copy th Form ID of the form you just created and use it to open it in the SDK.


### In the SDK
The SDK uses the Form ID you previously got from [Usabilla](https://app.usabilla.com/member/) to fetch and display your form inside your app.

A basic implementation of the SDK would be the following.

```

class ViewController: UIViewController, UsabillaFeedbackFormDelegate {

    override func viewDidLoad() {
        super.viewDidLoad()
        UsabillaFeedbackForm.delegate = self
        UsabillaFeedbackForm.loadFeedbackForm("Form ID")
    }

    //Called when your form succesfully load
    func formLoadedCorrectly(_ form: UINavigationController, active: Bool) {
        present(form, animated: true, completion: nil)
    }
    //Called when your forms can not be loaded. Returns a default form
    func formFailedLoading(_ backupForm: UINavigationController) {
        present(backupForm, animated: true, completion: nil)
    }

}
```

## Usage

### Adding a screenshot

It is possible to attach a screenshot to a feedback form.

You can take a screenshot at any moment calling `let image = UsabillaFeedbackForm.takeScreenshot(self.view)`.

To attach the screenshot to the form, pass it as a parameter when calling `UsabillaFeedbackForm.loadFeedbackForm("Form Id", screenshot: image)`

Pass `nil` as the `screenshot` parameter if you don't want to have a screenshot of the current view.

**Custom Screenshot & Sensitive Informations**

Instead of taking the screenshot using the `UsabillaFeedbackForm.takeScreenshot()` method, you can provide any image you wish by passing it as the `image` parameter when calling `UsabillaFeedbackForm.loadFeedbackForm()`

This will allow you to hide any user sensitive or private information by, for example, taking the screenshot yourself, removing all unwanted information and submitting the censored version.

### Adding custom variables

You can pass along custom variables that will be attached to the feedback users send.
Custom variables are held in a dictionary.

After you have initialised your controller, you can easily set custom variables using
```
var customVariables: [String : Any] = [:]
customVariables["user"] = "Mario"
customVariables["age"] = 10
```

You can create one beforehand or on the fly, as shown in the example, and its content will be reported and displayed in the Usabilla web interface.

To make sure the variables are properly displayed in the web interface it is advised to keep the dictionary object fairly simple and to not nest more than one object into another.

Custom variables are added as a parameter when calling `UsabillaFeedbackForm.loadFeedbackForm("Form ID", screenshot: nil, customVariables: customVariables)
`


### Customising the form

You can customise the colors of all elements of the form.
For a more in depth guide on customisation see the [Wiki page](https://github.com/usabilla/usabilla-u4a-ios-swift-sdk/wiki/Changing-colors)


### App Store rating

It is possible to invite the user to leave a review of your application in the App Store once he has submitted the form.

This invitation will only be showed if:
* The user gave a positive rating (4-5 / 5) in the feedback form.
* You have set `UsabillaFeedbackForm.appStoreId = "id"` with the app store id of your application.
* You have enabled the feature in the Usabilla web interface, in the advanced edit settings of the form (default is disabled)  

You have to specify the app id omitting the initial "id", leaving only the numerical part.





