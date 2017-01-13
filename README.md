# Notifyvisitors
An Android sdk to show in-app popups, surveys, track events, create audience, send push notifications &amp; facilitate you with lots of powerful functionality.

Follow the steps given below to integrate the NotifyVisitors SDK in your android app:-

A. Using Gradle (Android Studio)

Add the following dependency to your build.gradle file:
dependencies {  compile project(":notifyvisitors")  }

B. Using Eclipse

1) Import the downloaded sdk as follows: 
    File -> Import -> Existing Android Code into Workspace
2) Right click on your project and select Properties. Click on Android and Add the notifyvisitors Android 
    library project to your application project.
3) Open the file named project.properties under your application project. Add the property 
    manifestmerger.enabled=true

Steps common for both Android Studio and Eclipse
1. Configure your AndroidManifest.xml
<manifest....>
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
 <uses-permission android:name="android.permission.INTERNET"/> 
<uses-permission android:name="android.permission.GET_ACCOUNTS" />
<uses-permission android:name="android.permission.GET_TASKS" />
<uses-permission android:name="android.permission.WAKE_LOCK" />
<uses-permission android:name="com.google.android.c2dm.permission.RECEIVE"/>
<permission android:name="your_app_package_name.permission.C2D_MESSAGE" android:protectionLevel="signature" />
<uses-permission android:name="your_app_package_name.permission.C2D_MESSAGE" />
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />   <aplication....>
<meta-data android:name="notifyvisitors_bid" android:value="xxxx" ></meta-data>
<meta-data android:name="notifyvisitors_bid_e" android:value="xxxxxxxxx" ></meta-data>

2. Initializing the sdk
a)  If you don’t have your own application class, then in the manifest file register our application class like this in application tag:
<aplication android:name="com.notifyvisitors.notifyvisitors.NotifyVisitorsApplication"></application>

b)  If you have your own application class then inside your application class onCreate method, call our register method like this:
 NotifyVisitorsApplication.register(this);

3. Showing InApp Notifications
To show in app popups in your app, you can call the show() method like this:-
 NotifyVisitorsApi.getInstance(this).show(null,null,null);

4. Showing Notification Center
To show notification center in your app, you can call the showNotifications() method like this:-
 NotifyVisitorsApi.getInstance(this).showNotifications(0);

5. Showing Instant Push Notification
To show instant push notification in your app, you can call the scheduleNotification() method like this:-
NotifyVisitorsApi.getInstance(this).scheduleNotification(String nid, String tag, String time,String title, String message,String url, String icon);
where:
nid  is the id of the notification.
tag is a unique tag(string value)
time is the time delay after which notification has to be shown
title is the title of notification.
message is the message of notification.
url is the package name of the activity to be open on click of the notification.
icon is the link of the image to be shown as image on the notification.
** nid, tag and time are mandatory fields.

5. Tracking events
To track the various app events, call the method event like:-
NotifyVisitorsApi.getInstance(getActivity()).event(String eventName, JSONArray attributes, String ltv, String scope);
where:-
eventName is the name of the event you want to track for example “sale”,
attributes is the json array containing different properties of the event in the form of json object like:-
JSONArray eventArray = new JSONArray();
JSONObject price = new JSONObject();
JSONObject category = new JSONObject();
try {
price.put("price","20000");
category.put("firstCategory","standard");
category.put("secondCategory","fancy");
} catch (JSONException e) {
    e.printStackTrace();
}
eventArray.put(price);
eventArray.put(category);

Ltv is the value you want to give to user corresponding to every particular event.
SCOPE - 1 (called every time the function is called)
               2 (called once for the session)
               3 (called once per lifetime)

6. User Identifiers
To identify the different app users, call the method userIdentifier like:-
NotifyVisitorsApi.getInstance(getActivity()).userIdentifier(String userID, JSONArray jsonArray);
where:-
userID is the unique identifier to identify different users like email, contact number or any other custom user id,
jsonArray is the json array containing user information in the form of json object like:-
JSONArray jsonArray = new JSONArray();
JSONObject name = new JSONObject();
JSONObject number = new JSONObject();
try {
name.put("name","Basant");
number.put("number","9898765489");
} catch (JSONException e) {
    e.printStackTrace();
}
jsonArray.put(name);
jsonArray.put(number);
