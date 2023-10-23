---
layout: post
title: Android Intents and Intent Filters
date: '2023-10-23 05:39:12 +0300'
image: /assets/img/cover_images/1.png
categories: [Android hacking, Android Intents and Intent Filters]
tags: [Intents, Intent Filters, ]
---

## Intents and intent filters
An Intent is a messaging object you can use to request an action from another app component. They facilitate communication between components.

## Types of intents
### Explicit intents 
You explicitly provide the target app's package name or a fully-qualified component class name. here we use a fully-qualified component class name in our own app. 
```java
class MainActivity: ComponentActivity(){
    ovveride fun onCreate(SavedInstanceState: Bundle?){
        super.onCreate(savedInstanceState)
        setContent{
            Button(onClick = {
                Intent(applicationContext, SecondActivity::class.java).also {
                    startActivity(it)
                }
            })
        }
    }
}
```
Here we provide the target app's package name to launch the main activity of the specified app
```java
class MainActivity: ComponentActivity(){
    ovveride fun onCreate(SavedInstanceState: Bundle?){
        super.onCreate(savedInstanceState)
        setContent{
            Button(onClick = {
                Intent(Intent.ACTION_MAIN).also {
                    it.`package` = "com.google.android.youtube"
                    startActivity(it)
                }
            })
        }
    }
}
```
## Fundamental use cases of Intents
### Starting an activity
You can start a new instance of an Activity by passing an Intent to startActivity(). The Intent describes the activity to start and carries any necessary data. If you want to receive a result from the activity when it finishes, call startActivityForResult(). Your activity receives the result as a separate Intent object in your activity's onActivityResult() callback.

### Starting a service
A Service is a component that performs operations in the background without a user interface. With Android 5.0 (API level 21) and later, you can start a service with JobScheduler.
For versions earlier than Android 5.0 (API level 21), you can start a service by using methods of the Service class. You can start a service to perform a one-time operation (such as downloading a file) by passing an Intent to startService(). The Intent describes the service to start and carries any necessary data.If the service is designed with a client-server interface, you can bind to the service from another component by passing an Intent to bindService().

### Delivering a broadcast
A broadcast is a message that any app can receive. The system delivers various broadcasts for system events, such as when the system boots up or the device starts charging. You can deliver a broadcast to other apps by passing an Intent to sendBroadcast() or sendOrderedBroadcast().
