---
nav_title: In-App Message Delivery
article_title: In-App Message Delivery for iOS
platform: Swift
page_order: 3
description: "This article covers iOS in-app message delivery, listing different trigger types, delivery semantics, and event triggering steps."
channel:
  - in-app messages

---

# In-app message delivery

## Trigger types

Our in-app message product allows you to trigger in-app message display as a result of several different event types: `Any Purchase`, `Specific Purchase`, `Session Start`, `Custom Event`, and `Push Click`. Furthermore, `Specific Purchase` and `Custom Event` triggers contain robust property filters.

{% alert note %}
Triggered in-app messages only work with custom events logged through the Braze SDK. In-app messages can't be triggered through the API or by API events (such as purchase events). If you're working with iOS, visit our [tracking custom events]({{site.baseurl}}/developer_guide/platform_integration_guides/swift/analytics/tracking_custom_events/) article to learn more. 
{% endalert %}

## Delivery semantics

All in-app messages that a user is eligible for are delivered to the user's device on session start. For more information about the SDK's session start semantics, read about our [session lifecycle][45]. Upon delivery, the SDK will prefetch assets to be available immediately at trigger time, minimizing display latency.

When a trigger event has more than one eligible in-app message associated with it, only the in-app message with the highest priority will be delivered.

There can be some latency for in-app messages that display immediately on delivery (session start, push click) due to assets not being prefetched.

## Minimum time interval between triggers

By default, we rate limit in-app messages to once every 30 seconds to ensure a quality user experience.

You can override this value by setting the `triggerMinimumTimeInterval` property in your Braze configuration. Be sure to configure this value before initializing your Braze instance. Set the `triggerMinimumTimeInterval` to the integer value you want as your minimum time in seconds between in-app messages:

{% tabs %}
{% tab swift %}

```swift
let configuration = Braze.Configuration(
  apiKey: "YOUR-APP-IDENTIFIER-API-KEY",
  endpoint: "YOUR-BRAZE-ENDPOINT"
)
// Sets the minimum trigger time interval to 5 seconds
configuration.triggerMinimumTimeInterval = 5
let braze = Braze(configuration: configuration) 
AppDelegate.braze = braze
```
{% endtab %}
{% tab OBJECTIVE-C %}

```objc
BRZConfiguration *configuration =
    [[BRZConfiguration alloc] initWithApiKey:@"<BRAZE_API_KEY>"
                                    endpoint:@"<BRAZE_ENDPOINT>"];
// Sets the minimum trigger time interval to 5 seconds
configuration.triggerMinimumTimeInterval = 5;
Braze *braze = [BrazePlugin initBraze:configuration];
AppDelegate.braze = braze;
```
{% endtab %}
{% endtabs %}

## Local in-app message delivery

### The in-app message stack

#### Showing in-app messages

When a user is eligible to receive an in-app message, the `BrazeInAppMessagePresenter` will be offered the latest in-app message off the in-app message stack. The stack only persists stored in-app messages in memory and is cleared up between app launches from suspended mode.

To allow Braze to display in-app messages, create an implementation of the `BrazeInAppMessagePresenter` protocol and assign it to the optional `inAppMessagePresenter` on your Braze instance. You can also use the default Braze UI presenter by instantiating a `BrazeInAppMessageUI` object.

Note that you will need to import the `BrazeUI` library to access the `BrazeInAppMessageUI` class.

{% tabs %}
{% tab swift %}

```swift
AppDelegate.braze?.inAppMessagePresenter = BrazeInAppMessageUI()
```

{% endtab %}
{% tab OBJECTIVE-C %}

```objc
AppDelegate.braze.inAppMessagePresenter = [[BrazeInAppMessageUI alloc] init];
```
{% endtab %}
{% endtabs %}

#### Adding in-app messages to the stack

Users are eligible to receive an in-app message in the following situations:

- An in-app message trigger event is fired
- Session start event
- The app is opened from a push notification

Triggered in-app messages are placed on the stack when their trigger event is fired. If multiple in-app messages are in the stack and waiting to be displayed, Braze will display the most recently received in-app message first (last in, first out).

#### Returning in-app messages to the stack

A triggered in-app message can be returned to the stack in the following situations:

- The in-app message is triggered when the app is in the background.
- Another in-app message is currently visible.

#### Discarding in-app messages

A triggered in-app message will be discarded in the following situations:

- The asset (image or ZIP file) of the in-app message failed to download.
- The in-app message is ready to be displayed but past the timeout duration.
- The device orientation doesn't match the triggered in-app message's orientation.
- The in-app message is a full in-app message but has no image.
- The in-app message is an image-only modal in-app message but has no image.

### Real-time in-app message creation and display

If you wish to display an in-app message at other times within your app, you may manually call the [`present(message:)`](https://braze-inc.github.io/braze-swift-sdk/documentation/brazekit/brazeinappmessagepresenter/present(message:)) method on your `inAppMessagePresenter`. In-app messages can be locally created within the app and displayed via Braze. This is particularly useful for displaying messages you wish to trigger within the app in real-time.

{% tabs %}
{% tab swift %}

```swift
  let customInAppMessage = Braze.InAppMessage.slideup(
    .init(message: "YOUR_CUSTOM_SLIDEUP_MESSAGE", slideFrom: .bottom, themes: .defaults)
  )
  AppDelegate.braze?.inAppMessagePresenter?.present(message: customInAppMessage)
```

{% endtab %}
{% tab OBJECTIVE-C %}

```objc
  BRZInAppMessageRaw *customInAppMessage = [[BRZInAppMessageRaw alloc] init];
  customInAppMessage.type = BRZInAppMessageRawTypeSlideup;
  customInAppMessage.message = @"YOUR_CUSTOM_SLIDEUP_MESSAGE";
  customInAppMessage.slideFrom = BRZInAppMessageRawSlideFromBottom;
  customInAppMessage.themes = @{
    @"light": BRZInAppMessageRawTheme.defaultLight,
    @"dark": BRZInAppMessageRawTheme.defaultDark
  };
  [AppDelegate.braze.inAppMessagePresenter presentMessage:customInAppMessage];
```

{% endtab %}
{% endtabs %}

[30]: {{site.baseurl}}/developer_guide/platform_integration_guides/ios/in-app_messaging/customization/setting_delegates/#core-in-app-message-delegate
[38]: {{site.baseurl}}/developer_guide/platform_integration_guides/ios/in-app_messaging/customization/setting_delegates/#in-app-message-delegate
[45]: {{site.baseurl}}/developer_guide/platform_integration_guides/ios/analytics/tracking_sessions/#session-lifecycle
