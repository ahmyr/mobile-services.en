---
description: After you configure the deep linking URL in the Adobe Mobile Services UI, this URL will be in the push payload with the adb_deeplink key.
seo-description: After you configure the deep linking URL in the Adobe Mobile Services UI, this URL will be in the push payload with the adb_deeplink key.
seo-title: Implement Push Messaging with Deep Linking
title: Implement Push Messaging with Deep Linking
uuid: e24f9248-8d48-4e57-84af-3a05b72e2a09
---

# Implement push messaging with deep linking {#implement-push-messaging-with-deep-linking}

After you configure the deep linking URL in the Adobe Mobile Services UI, this URL will be in the push payload with the adb_deeplink key.

You can get the URL by calling `data.getString("adb_deeplink")` in the customized `GcmListenerService` class or `remoteMessage.getData().get("adb_deeplink")` in the `FirebaseMessagingService`.

>[!TIP]
>
>You can define different intents depending on whether the payload has a deep linking URL.

1. Complete one of the following tasks:

    * If the deep linking URL **is** in the push payload, create a `ACTION_VIEW` intent with the URL.

      When the user clicks the push message, a deep link is triggered. 

    * If the deep linking URL **is not** in the push payload, create an intent that will open one of your activities.

## Examples

Here is an example that uses a GCM implementation to pass data to the Mobile SDK after the message is received: 

```java
        @Override 
public void onMessageReceived(String from, Bundle data) { 
   String message = data.getString("message"); 
   String deeplink = data.getString("adb_deeplink"); 
   sendNotification(message, deeplink); 
} 
  
private void sendNotification(String messageBody, String deeplink) { 
    Intent intent; 
    if (deeplink!=null) { 
        intent = new Intent(Intent.ACTION_VIEW, Uri.parse(deeplink)); 
    } else { 
        intent = new Intent(this, MainActivity.class); 
    } 
  
    intent.addFlags(Intent.FLAG_ACTIVITY_CLEAR_TOP); 
    PendingIntent pendingIntent = PendingIntent.getActivity(this, 0 /* Request code */, intent, 
        PendingIntent.FLAG_ONE_SHOT);

    Uri defaultSoundUri= RingtoneManager.getDefaultUri(RingtoneManager.TYPE_NOTIFICATION); 
    NotificationCompat.Builder notificationBuilder = new NotificationCompat.Builder(this) 
        .setSmallIcon(R.drawable.ic_stat_ic_notification) 
        .setContentTitle("Deep Link Push") 
        .setContentText(messageBody) 
        .setAutoCancel(true) 
        .setSound(defaultSoundUri) 
        .setContentIntent(pendingIntent); 
  
    NotificationManager notificationManager = 
        (NotificationManager) getSystemService(Context.NOTIFICATION_SERVICE); 
  
    notificationManager.notify(0 /* ID of notification */, notificationBuilder.build()); 
          } 

```

This is a sample implementation for the class extending from `FirebaseMessagingService`: 

```java
public void onMessageReceived(RemoteMessage message) { 
 
       Map<String, String> data = message.getData(); 
       String messageStr = data.get("message"); 
       String deepLink = data.get("adb_deeplink"); 
 
       sendNotification(deepLink, messageStr, data); 
    } 
 
private void sendNotification(String deeplink, String message, Map<String, String> data) { 
       Intent intent; 
 
       if (deeplink!=null) { 
           intent = new Intent(Intent.ACTION_VIEW, Uri.parse(deeplink)); 
       } else { 
           intent = new Intent(this, MainActivity.class); 
       } 
 
       intent.addFlags(Intent.FLAG_ACTIVITY_CLEAR_TOP); 
 
       //put the data map into the intent to track clickthroughs 
       Bundle pushData = new Bundle(); 
       Set<String> keySet = data.keySet(); 
       for (String key : keySet) { 
           pushData.putString(key, data.get(key)); 
       } 
 
       intent.putExtras(pushData); 
 
       PendingIntent pendingIntent = PendingIntent.getActivity(this, 0, intent, 
               PendingIntent.FLAG_ONE_SHOT); 
 
       Uri defaultSoundUri= RingtoneManager.getDefaultUri(RingtoneManager.TYPE_NOTIFICATION); 
 
       NotificationCompat.Builder notificationBuilder = new NotificationCompat.Builder(this) 
                .setSmallIcon(R.drawable.icon) 
                .setContentTitle("FCM Deep Link Push") 
                .setContentText(message) 
                .setAutoCancel(true) 
                .setSound(defaultSoundUri) 
                .setContentIntent(pendingIntent); 
 
       NotificationManager notificationManager =  
       (NotificationManager)getApplicationContext().getSystemService(Context.NOTIFICATION_SERVICE); 
           notificationManager.notify(0, notificationBuilder.build()); 
       } 

```