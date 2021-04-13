Loyalty SDK [![Language](https://img.shields.io/badge/Swift-5.0-%234c20f0.svg)]() [![Release](https://img.shields.io/badge/Release-0.1.0-%234c20f0.svg)]()
=====

`PhunToken Loyalty SDK` is an iOS SDK that allows you to reward your users for in-app customer behavior that helps promote increased brand awareness, engagement and loyalty.

***<sub>note</sub>*** <br/>
> `PhunToken Loyalty SDK` currently only supports iOS projects written in **Swift 5.0**+.

## [Using Loyalty SDK](#installation)

### **CocoaPods**

If using [CocoaPods](https://cocoapods.org/), add the following to your Podfile:

```ruby
pod 'Loyalty', '0.1.0'
```

***
## [Usage Overview](#usage-overview)

### **Initialization**
`PhunToken Loyalty SDK` is initialized along with your current [MaaS SDK integration](https://github.com/phunware/maas-core-ios-sdk).  That being said, the important integration steps are setting up MaaS Core with relevant appId, accessKey, and secret.

***
### **Opt In**
`PhunToken Loyalty SDK` is opt in by default and based around your own system of registered users.  To opt your user in you will need to provide the SDK with a unique identifier for the user that maps cleanly to the representation of the user in your own system (such as the email they used to register with your app). It is expected that you will track the opt in state in your own app.


```swift
Loyalty.linkManager.linkUser(user: "joe@phunware.com") { [weak self] result in
    switch result {
    case .success:
        print("Success!")
    case .failure(let error):
        print("Failure")
    }
}
```

***
### **Checking the users balance**

Phunware will maintain a pending balance for your previously opted in users on our servers.  You can request this balance at any time (after opt in).

The actual user balance will be returned along with the provided image and metadata you have previously setup in the portal for your loyalty token(url).

```swift
Loyalty.assetManager.balance { [weak self] result in
    switch result {
    case .success(let asset):
        print("Balance is \(asset.balance)")
    case .failure(let error):
        print("Failed to get balance")
    }
}
```

***
### **Events**
Instrumented Events can be used to reward your user with new loyalty tokens or to deduct from their balance to unlock digital content.

Your instrumented events must be setup ahead of time on the portal, along with any additional thresholds and limits.


```swift
// Share a recipe.  This earns the user Dessert Coins.
Loyalty.assetManager.fireEvent(eventName: "share_recipe", parameters: ["donut"]) { [weak self] result in
    switch result {
    case .success(let sideEffects):
        // List of SideEffects will have displayable values
        // setup on the portal.
        print("Success!")
    case .failure(let error):
        print("Failure")
    }
}
```

***
### **Linking to PhunToken**
You have the option of letting your users link their loyalty token balance to the Phunware PhunWallet app.  If you have enabled conversion of your loyalty token into PhunToken, your users will be able to convert at the threshold you specify.

```swift
Loyalty.linkManager.linkWallet { [weak self] result in
    switch result {
    case .success:
        print("PhunWallet app installed and linking is in progress.")
    case .failure(let error):
        print("PhunWallet app not installed or other failure.")
    }
}
```

***
<a id="class"></a>
## Class Reference Documentation
The [Reference Documentation](https://phunware.github.io/maas-loyalty-sdk-ios) has all of the detailed usage information including all the public methods, parameters, and convenience initializers.

***
<a id="privacy"></a>
## Privacy
You understand and consent to Phunware’s Privacy Policy located at www.phunware.com/privacy. If your use of Phunware’s software requires a Privacy Policy of your own, you also agree to include the terms of Phunware’s Privacy Policy in your Privacy Policy to your end users.
***
<a id="terms"></a>
## Terms
Use of this software requires review and acceptance of our terms and conditions for developer use located at http://www.phunware.com/terms/
