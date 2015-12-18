# iOS 9 App Transport Security #

Starting from [iOS 9](https://developer.apple.com/library/prerelease/ios/releasenotes/General/WhatsNewIniOS/Articles/iOS9.html#//apple_ref/doc/uid/TP40016198-SW1), [App Transport Security](https://developer.apple.com/library/prerelease/ios/technotes/App-Transport-Security-Technote/) enforces to use secure HTTPS requests [by default](https://developer.apple.com/library/prerelease/ios/technotes/App-Transport-Security-Technote/index.html#//apple_ref/doc/uid/TP40016240-CH1-SW2).

>  **App Transport Security**

> App Transport Security (ATS) enforces best practices in the secure connections between an app and its back end. ATS prevents accidental disclosure, provides secure default behavior, and is easy to adopt; it is also on by default in iOS 9 and OS X v10.11. You should adopt ATS as soon as possible, regardless of whether you’re creating a new app or updating an existing one.

> If you’re developing a new app, you should use HTTPS exclusively. If you have an existing app, you should use HTTPS as much as you can right now, and create a plan for migrating the rest of your app as soon as possible. In addition, your communication through higher-level APIs needs to be encrypted using TLS version 1.2 with forward secrecy. If you try to make a connection that doesn't follow this requirement, an error is thrown. If your app needs to make a request to an insecure domain, you have to specify this domain in your app's Info.plist file.

In short, when an application is compiled with Xcode 7 and iOS 9, and attempt to connect to HTTP server that doesn't support latest SSL technology ([TLS 1.2](https://en.wikipedia.org/wiki/Transport_Layer_Security#TLS_1.2)), it will fail with an error like this:

```objective-c
CFNetwork SSLHandshake failed (-9801)
Error Domain=NSURLErrorDomain Code=-1200 "An SSL error has occurred and a secure connection to the server cannot be made." UserInfo=0x7fb080442170 {NSURLErrorFailingURLPeerTrustErrorKey=<SecTrustRef: 0x7fb08043b380>, NSLocalizedRecoverySuggestion=Would you like to connect to the server anyway?, _kCFStreamErrorCodeKey=-9802, NSUnderlyingError=0x7fb08055bc00 "The operation couldn’t be completed. (kCFErrorDomainCFNetwork error -1200.)", NSLocalizedDescription=An SSL error has occurred and a secure connection to the server cannot be made., NSErrorFailingURLKey=https://yourserver.com, NSErrorFailingURLStringKey=https://yourserver.com, _kCFStreamErrorDomainKey=3}
```

From [App Transport Security Technote](https://developer.apple.com/library/prerelease/ios/technotes/App-Transport-Security-Technote/index.html#//apple_ref/doc/uid/TP40016240-CH1-SW2):

> All connections using the NSURLConnection, CFURL, or NSURLSession APIs use App Transport Security default behavior in apps built for iOS 9.0 or later, and OS X 10.11 or later. Connections that do not follow the requirements will fail. For more information on various the connection methods, see NSURLConnection Class Reference, CFURL Reference, or NSURLSession Class Reference.

Fortunately we can specify exceptions from default behavior in `Info.plist`. Doing this, we can leverage App Transport Security where possible, while disabling it in places where you cannot support it.

### Per-Domain Exceptions ###

```xml
<key>NSAppTransportSecurity</key>
<dict>
  <key>NSExceptionDomains</key>
  <dict>
    <key>yourserver.com</key>
    <dict>
      <!--Include to allow subdomains-->
      <key>NSIncludesSubdomains</key>
      <true/>
      <!--Include to allow HTTP requests-->
      <key>NSTemporaryExceptionAllowsInsecureHTTPLoads</key>
      <true/>
      <!--Include to specify minimum TLS version-->
      <key>NSTemporaryExceptionMinimumTLSVersion</key>
      <string>TLSv1.1</string>
    </dict>
  </dict>
</dict>
```

### For arbitrary content ###

This is considerably a dangerous approach and should not be used sparingly.

```xml
<key>NSAppTransportSecurity</key>
<dict>
  <!--Include to allow all connections (DANGER)-->
  <key>NSAllowsArbitraryLoads</key>
      <true/>
</dict>
```

Some things to note:
+ Apps built using earlier SDK will behave [the same](https://forums.developer.apple.com/message/40668). But if compiled using Xcode 7 onwards, we must migrate.
+ For apps using the Facebook SDK, read [their guide](https://developers.facebook.com/docs/ios/ios9) to adapt changes.
+ For a short and more throughout information regarding this, you can read [this article](http://www.neglectedpotential.com/2015/06/working-with-apples-application-transport-security/).
+ For full list of exception keys, check out [this table from Apple](https://developer.apple.com/library/prerelease/ios/technotes/App-Transport-Security-Technote/index.html#//apple_ref/doc/uid/TP40016240-CH1-SW5).

# References #

Official documents:
+ [WWDC 15 - Networking with NSURLSession](https://developer.apple.com/videos/wwdc/2015/?id=711)
+ [App Transport Security Technote](https://developer.apple.com/library/prerelease/ios/technotes/App-Transport-Security-Technote/index.html)
+ [What's New in iOS 9] (https://developer.apple.com/library/prerelease/ios/releasenotes/General/WhatsNewIniOS/Articles/iOS9.html#//apple_ref/doc/uid/TP40016198-SW14)
+ [iOS 9 Release Notes](https://developer.apple.com/library/prerelease/ios/releasenotes/General/RN-iOSSDK-9.0/)
+ [Application Transport Security ? - Apple Developer Forums](https://forums.developer.apple.com/thread/3544)
+ [Application Transport Security (ATS) and app submission - Apple Developer Forums](https://forums.developer.apple.com/message/40668)

Note from Facebook SDK and Google Ads SDK:
+ [Preparing Your Apps for iOS9 - Facebook Developers](https://developers.facebook.com/docs/ios/ios9)
+ [Google Ads Developer Blog](http://googleadsdeveloper.blogspot.ch/2015/08/handling-app-transport-security-in-ios-9.html)

Articles and blogs:
+ [Configuring App Transport Security Exceptions in iOS 9 and OSX 10.11](http://ste.vn/2015/06/10/configuring-app-transport-security-ios-9-osx-10-11/)
+ [Working with Apple Application Transport Security](http://www.neglectedpotential.com/2015/06/working-with-apples-application-transport-security/)
+ [iOS 9 Security Privacy](https://nabla-c0d3.github.io/blog/2015/06/16/ios9-security-privacy/)
+ [Apple iOS 9: Security & Privacy Features](https://medium.com/@FredericJacobs/apple-ios-9-security-privacy-features-8d82d9da10eb)