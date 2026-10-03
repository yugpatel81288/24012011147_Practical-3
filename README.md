# Practical-3: Intent Demonstration in Android

## AIM

Create an Android application that demonstrates **Implicit Intent** and **Explicit Intent**.

## Practical Requirements

The application demonstrates the following operations:

1. 📞 Make a call to a specific number
2. 🌐 Open a specific URL
3. 📋 Open Call Log
4. 🖼️ Open Gallery
5. ⏰ Set Alarm
6. 📷 Open Camera
7. 🔐 Open Login Activity

## Concepts Studied

* Intent
* Types of Intent

  * Implicit Intent
  * Explicit Intent
* Intent Actions
* `Intent.setData()`
* `Intent.setType()`
* `Button`
* `ConstraintLayout`
* `CoordinatorLayout`
* `startActivity()`
* `ActivityResultContracts`
* Runtime Permissions
* `ContextCompat.checkSelfPermission()`
* `ActivityCompat.requestPermissions()`
* `Uri.parse()`
* `ContactsContract.Contacts.CONTENT_TYPE`
* `CallLog.Calls.CONTENT_TYPE`
* `"image/*"`
* `"tel:"`

## Implicit Intent

An **Implicit Intent** does not specify a particular component or activity. Instead, it specifies an action that should be performed, and Android finds an appropriate application to handle that action.

Examples used in this practical:

```kotlin
Intent(Intent.ACTION_VIEW, Uri.parse("https://www.google.com"))
```

```kotlin
Intent(Intent.ACTION_DIAL, Uri.parse("tel:9876543210"))
```

```kotlin
Intent(Intent.ACTION_VIEW).apply {
    type = "image/*"
}
```

## Explicit Intent

An **Explicit Intent** specifies the exact activity or component that should be opened.

Example:

```kotlin
val intent = Intent(this, LoginActivity::class.java)
startActivity(intent)
```

Here, `LoginActivity` is explicitly specified, so Android directly opens that activity.

## Intent Operations

### 1. Make Call / Open Dialer

```kotlin
val intent = Intent(Intent.ACTION_DIAL)
intent.data = Uri.parse("tel:9876543210")
startActivity(intent)
```

### 2. Open Specific URL

```kotlin
val intent = Intent(Intent.ACTION_VIEW)
intent.data = Uri.parse("https://www.google.com")
startActivity(intent)
```

### 3. Open Call Log

```kotlin
val intent = Intent(Intent.ACTION_VIEW)
intent.type = CallLog.Calls.CONTENT_TYPE
startActivity(intent)
```

### 4. Open Gallery

```kotlin
val intent = Intent(Intent.ACTION_GET_CONTENT)
intent.type = "image/*"
startActivity(intent)
```

### 5. Set Alarm

```kotlin
val intent = Intent(AlarmClock.ACTION_SET_ALARM).apply {
    putExtra(AlarmClock.EXTRA_HOUR, 7)
    putExtra(AlarmClock.EXTRA_MINUTES, 0)
}
startActivity(intent)
```

### 6. Open Camera

```kotlin
val intent = Intent(MediaStore.ACTION_IMAGE_CAPTURE)
startActivity(intent)
```

### 7. Open Login Activity

```kotlin
val intent = Intent(this, LoginActivity::class.java)
startActivity(intent)
```

## Permissions

Some Android operations require permissions. Permissions are declared in `AndroidManifest.xml` and, where required, requested at runtime.

Example:

```xml
<uses-permission android:name="android.permission.CALL_PHONE" />
<uses-permission android:name="android.permission.READ_CALL_LOG" />
<uses-permission android:name="android.permission.CAMERA" />
```

Permission checking can be performed using:

```kotlin
ContextCompat.checkSelfPermission()
```

and permissions can be requested using:

```kotlin
ActivityCompat.requestPermissions()
```

## Activity Result API

Modern Android applications can use **ActivityResultContracts** to launch activities and receive results.

Example:

```kotlin
val galleryLauncher = registerForActivityResult(
    ActivityResultContracts.GetContent()
) { uri ->
    // Handle selected image
}

galleryLauncher.launch("image/*")
```

## Important Methods and Constants

| Method / Constant            | Purpose                      |
| ---------------------------- | ---------------------------- |
| `Intent()`                   | Creates an Intent            |
| `startActivity()`            | Starts another Activity      |
| `setData()`                  | Sets data URI for an Intent  |
| `setType()`                  | Sets MIME type               |
| `Uri.parse()`                | Converts a string into a URI |
| `ACTION_VIEW`                | Views a resource             |
| `ACTION_DIAL`                | Opens phone dialer           |
| `ACTION_GET_CONTENT`         | Selects content              |
| `ACTION_IMAGE_CAPTURE`       | Opens camera                 |
| `ACTION_SET_ALARM`           | Creates an alarm             |
| `CallLog.Calls.CONTENT_TYPE` | Accesses call log            |
| `"image/*"`                  | Represents image MIME types  |
| `"tel:"`                     | Represents telephone numbers |

## Result

The Android application successfully demonstrates both **Implicit Intent** and **Explicit Intent** by performing different operations such as opening the dialer, URL, call log, gallery, alarm, camera, and Login Activity.

## Conclusion

This practical provides an understanding of how **Intents** are used for communication between Android components and applications. Implicit intents are useful for requesting an action from any suitable application, while explicit intents are used to navigate directly to a specific Activity within the application.
