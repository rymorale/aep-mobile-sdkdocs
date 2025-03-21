---
noIndex: true
---

<Variant platform="android" api="extension-version" repeat="5"/>

#### Java

**Syntax**

```java
public static String extensionVersion();
```

**Example**

```java
Messaging.extensionVersion();
```

<Variant platform="ios" api="extension-version" repeat="10"/>

#### Swift

**Syntax**

```swift
public static let extensionVersion
```

**Example**

```swift
Messaging.extensionVersion
```

#### Objective-C

**Syntax**

```swift
public static let extensionVersion
```

**Example**

```objc
[AEPMobileMessaging extensionVersion];
```

<Variant platform="android" api="handle-notification-response" repeat="6"/>

#### Java

**Syntax**

```java
public static void handleNotificationResponse(final Intent intent, final boolean applicationOpened, final String customActionId);
```

| **Parameter** | **Type** | **Description** |
| :----------- | :------- | :-------------- |
| `intent` | Intent | The intent contains information related to the messageId and the data. |
| `applicationOpened` | Boolean | Shows whether the application has been opened or not. |
| `actionId` | String | The ID of the custom action. |

**Example**

```java
// Intent can be retrieved from the Activity/BroadcastReceiver using the getIntent() method. 
Intent intent = getIntent();
Messaging.handleNotificationResponse(intent, true, "customActionId");
```

<Variant platform="ios" api="handle-notification-response" repeat="11"/>

#### Swift

**Syntax**

```swift
static func handleNotificationResponse(_ response: UNNotificationResponse, applicationOpened: Bool, customActionId: String?)
```

| **Parameter** | **Type** | **Description** |
| :----------- | :------- | :-------------- |
| `response` | UNNotificationResponse | An object containing information about the push notification details. |
| `applicationOpened` | Boolean | Shows whether the application has been opened or not. |
| `customActionId` | String | The ID of the custom action. |

**Example**

```swift
func userNotificationCenter(_: UNUserNotificationCenter,
                                didReceive response: UNNotificationResponse,
                                withCompletionHandler completionHandler: @escaping () -> Void) {
    Messaging.handleNotificationResponse(response, applicationOpened: true, customActionId: "customActionId")
    completionHandler()
}
```

#### Objective-C

**Syntax**

```objc
@objc(handleNotificationResponse:applicationOpened:withCustomActionId:)
static func handleNotificationResponse(_ response: UNNotificationResponse, applicationOpened: Bool, customActionId: String?)
```

**Example**

```objc
- (void)userNotificationCenter:(UNUserNotificationCenter *)center
didReceiveNotificationResponse:(UNNotificationResponse *)response
         withCompletionHandler:(void (^)())completionHandler {
    // Your code
    [AEPMobileMessaging handleNotificationResponse:response applicationOpened:true withCustomActionId:@"customActionId"];
    completionHandler();
}
```

<Variant platform="android" api="register-extension" repeat="5"/>

#### Java

**Syntax**

```java
public static void registerExtension();
```

**Example**

```java
Messaging.registerExtension();
```

<Variant platform="android" api="refresh" repeat="2"/>

#### Java

```java
Messaging.refreshInAppMessages();
```

<Variant platform="ios" api="refresh" repeat="2"/>

#### Swift

```swift
Messaging.refreshInAppMessages()
```

<Variant platform="android" api="set-push-identifier" repeat="7"/>

To retrieve the push token from Firebase Messaging Service, please follow the tutorial within the [Firebase documentation](https://firebase.google.com/docs/cloud-messaging/android/client#retrieve-the-current-registration-token).

#### Java

**Syntax**

```java
public static void setPushIdentifier(final String pushIdentifier);
```

| **Parameter** | **Type** | **Description** |
| :----------- | :------- | :-------------- |
| `pushIdentifier` | String | The push token that is synced with Adobe Experience Platform. |

**Example**

```java
FirebaseMessaging.getInstance().getToken()
        .addOnCompleteListener(new OnCompleteListener<String>() {
            @Override
            public void onComplete(@NonNull Task<String> task) {
                if (task.isSuccessful()) {
                    String token = task.getResult();
                    MobileCore.setPushIdentifier(token);
                }
            }
        });
```

<Variant platform="ios" api="set-push-identifier" repeat="13"/>

To retrieve the push token in iOS, please read the tutorial within [Apple's documentation](https://developer.apple.com/documentation/usernotifications/registering_your_app_with_apns).  

#### Swift

**Syntax**

```swift
public static func setPushIdentifier(_ deviceToken: Data?)
```

| **Parameter** | **Type** | **Description** |
| :----------- | :------- | :-------------- |
| `deviceToken` | Data | The push token that is synced with Adobe Experience Platform. |

**Example**

```swift
func application(_: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: Data) {
    MobileCore.setPushIdentifier(deviceToken)
}
```

#### Objective-C

**Syntax**

```objc
public static func setPushIdentifier(_ deviceToken: Data?)
```

| **Parameter** | **Type** | **Description** |
| :----------- | :------- | :-------------- |
| `deviceToken` | Data | The push token that is synced with Adobe Experience Platform. |

**Example**

```objc
- (void)application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken { 
    [AEPMobileCore setPushIdentifier:deviceToken];
}
```

<Variant platform="android" api="add-push-tracking-details" repeat="7"/>

#### Java

**Syntax**

```java
public static boolean addPushTrackingDetails(final Intent intent, final String messageId, final Map<String, String> data)
```

| **Parameter** | **Type** | **Description** |
| :----------- | :------- | :-------------- |
| `intent` | `Intent` | The pending intent that needs to be updated so it can be used when the user interacts with the notification. |
| `messageId` | `String` | The message ID for the push notification. |
| `data` | `Map<String, String>` | The data of the remoteMessage. |

This API returns a boolean, indicating whether the intent was updated with necessary information (messageId and Customer Journey data).

**Example**

```java
boolean success = addPushTrackingDetails(intent, messageId, data)
```

<Variant platform="android" api="messaging-push-payload" repeat="8"/>

#### Java

**Syntax**

```java
public MessagingPushPayload(RemoteMessage message)
```

| **Parameter** | **Type** | **Description** |
| :----------- | :------- | :-------------- |
| `message` | `RemoteMessage` | A message that contains the necessary attributes for creating a push notification. |

```java
public MessagingPushPayload(Map<String, String> data)
```

| **Parameter** | **Type** | **Description** |
| :----------- | :------- | :-------------- |
| `data` | `Map<String, String>` | A data payload that contains the necessary attributes for creating a push notification. |

**Examples**

```java
// Using the remote message
@Override
public void onMessageReceived(@NonNull RemoteMessage remoteMessage) {
    MessagingPushPayload payload = new MessagingPushPayload(remoteMessage);
}

// Using the data map
@Override
public void onMessageReceived(@NonNull RemoteMessage remoteMessage) {
    MessagingPushPayload payload = new MessagingPushPayload(remoteMessage.getData());
}
```

<Variant platform="android" api="public-apis" repeat="8"/>

#### Java

**Syntax**

```java
// Returns the title from the remote message
public String getTitle()

// Returns the body from the remote message 
public String getBody()

// Returns the sound from the remote message 
// The sound string represents the filename of a sound resource bundled in the app.
public String getSound()

// Returns the notification badge count from the remote message 
public int getBadgeCount()

// Returns the notification priority from the remote message. 
// For more information, please read the Firebase documentation (https://firebase.google.com/docs/reference/fcm/rest/v1/projects.messages#notificationpriority) 
public int getNotificationPriority()

// Returns the channel ID from the remote message. 
public String getChannelId()

// Returns the icon string from the remote message.
// The icon string represents the drawable resource name in the app.
public String getIcon()

// Returns the image URL from the remote message.
public String getImageUrl()

// Returns the data map from the remote message.
public Map<String, String> getData()

// Returns an ActionType object which represents the type of action which needs to be performed on push notification interaction.
// More information about the ActionType enum definition can be found in the ActionType section below.
public ActionType getActionType()

// Returns the action URI as a string. The action URI is used to direct the push notification interaction.
public String getActionUri()

// Returns a list of ActionButtons. More information about the ActionButtons class definition can be found in the ActionButtons section below.
public List<ActionButton> getActionButtons()
```

**Internal classes and enums**

**ActionType**

```java
public enum ActionType {
    DEEPLINK, WEBURL, OPENAPP, NONE
}
```

**ActionButtons**

```java
// Constructor
public ActionButton(final String label, final String link, final String type)

// Public APIs

// Returns the label for the action button
public String getLabel()

// Returns the link for the action button
public String getLink()

// Returns the ActionType for the action button
public ActionType getType()
```

<Variant platform="android" api="payload-keys" repeat="3"/>

You should use the `MessagingPushPayload` class to extract the payload values.

```json
{
   "message":{
      "android":{
         "collapse_key": "new_message",
         "priority": "HIGH",
         "data":{
            "adb_title":"Game Request",
            "adb_body":"Bob wants to play chess",
            "adb_sound" : "somesound_res",
            "adb_n_count" : "3",
            "adb_n_priority" : "PRIORITY_LOW",
            "adb_channel_id": "cid",
            "adb_icon" : "notification_icon",
            "adb_image": "www.imageUrl.com",           
            "adb_a_type": "DEEPLINK/WEBURL/OPENAPP",
            "adb_uri" : "deeplinkurl/weburl",
            "adb_act": [
                {
                    "label" : "deeplink",
                    "uri" : "notificationapp://",
                    "type" : "DEEPLINK"
                },
                {
                    "label" : "weburl",
                    "uri" : "https://www.yahoo.com",
                    "type" : "WEBURL"
                }
            ],          
            "some_custom_data_key": "some data"
         }
      }
   }
}
```

| **Key** | **Type** | **Description** |
| :------ | :------- | :-------------- |
| `adb_title` | String | The push notification's title |
| `adb_body` | String | The push notification's body |
| `adb_sound` | String | The push notification's sound |
| `adb_n_count` | String | The push notification badge count |
| `adb_n_priority` | String | The push notification's priority. For more information, please read the [Firebase documentation](https://firebase.google.com/docs/reference/fcm/rest/v1/projects.messages#notificationpriority) |
| `adb_channel_id` | String | The push notification's channel ID |
| `adb_icon` | String | The push notification's icon resource name |
| `adb_image` | String | The URL of the image to be displayed on the notification |
| `adb_a_type` | enum | An enum that determines what type of action will be performed when the notification is clicked. It can be one of the following values: `DEEPLINK`, `WEBURL`, or `OPENAPP`. |
| `adb_uri` | String | The URI used for deeplinking. The deeplink is used to open the appropriate webpage or app screen when the notification is clicked. |
| `adb_act` | Array | An array that contains the action object(s). |
| `adb_act.label` | String | The label for custom action button |
| `adb_act.uri` | String | The URI for custom action button |
| `adb_act.type` | enum | The action type for custom action button. It can be one of the following values: `DEEPLINK`, `WEBURL`, `OPENAPP` |

<Variant platform="ios" api="payload-keys" repeat="2"/>

```json
{
   "aps":{
      "alert":{
         "title": "Hello from CJM",
         "body": "Stay safe, wear a mask"
      },
      "sound": "dingDong",
      "badge":2,
      "mutable-content":1,
      "category": "iosCategory",
      "thread-id": "myGroup",
      "content-available":1
   },
   "some_custom_data_key": "some data",
   "adb_media": "www.imageUrl.com",
   "adb_a_type": "DEEPLINK/WEBURL/OPENAPP",
   "adb_uri": "deeplinkUrl/weburl",
}
```

| **Key** | **Type** | **Description** |
| :------ | :------- | :-------------- |
| `adb_media` | String | The URL of the media. In this situation, media refers to either an image or a video. This URL can be used to download the rich media before showing the push notification. |
| `adb_uri` | String | The URI used for deeplinking. The deeplink is used to open appropriate webpage or app screen when the notification is clicked. |
| `adb_a_type` | enum | An enum that determines what type of action will be performed when the notification is selected. It can be one of the following string values: `DEEPLINK`, `WEBURL`, `OPENAPP`. |
| `adb_act` | Array | An array that contains the action object(s). |
| `adb_act.aid` | String | The ID for the action object. |
| `adb_act.label` | String | The name for the action object |
| `adb_act.type` | String | The type for the action object. It can be one of the following string values: `DEEPLINK`, `WEBURL`, `DISMISS` |
