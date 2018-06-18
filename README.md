# OTP_Automatic_Detection
https://github.com/ajaygosh102/OTP_Automatic_Detection.git

[![codebeat badge](https://codebeat.co/badges/0d0a3e88-6da8-4e43-a0fc-999af604d0b4)](https://codebeat.co/projects/github-com-stfalcon-studio-smsverifycatcher-master) [ ![Download](https://api.bintray.com/packages/bevzaanton/maven/SmsVerifyCatcher/images/download.svg) ](https://bintray.com/bevzaanton/maven/SmsVerifyCatcher/_latestVersion)

![alt tag](http://i.imgur.com/7Kzzk5z.gif)



### Download

Download via Gradle:
```gradle
compile 'com.github.stfalcon:smsverifycatcher:0.3.1'
```

or Maven:
```xml
<dependency>
  <groupId>com.github.stfalcon</groupId>
  <artifactId>smsverifycatcher</artifactId>
  <version>0.3.1</version>
  <type>pom</type>
</dependency>
```

### Usage

Add permissions to AndroidManifest.xml:
```xml
  <uses-permission android:name="android.permission.RECEIVE_SMS" />
  <uses-permission android:name="android.permission.READ_SMS" />
```
Init SmsVerifyCatcher in method like onCreate activity:
```java
    smsVerifyCatcher = new SmsVerifyCatcher(this, new OnSmsCatchListener<String>() {
        @Override
        public void onSmsCatch(String message) {
            String code = parseCode(message);//Parse verification code
            etCode.setText(code);//set code in edit text
            //then you can send verification code to server
        }
    });
```
Override activity lifecicle methods:
```java
    @Override
    protected void onStart() {
        super.onStart();
        smsVerifyCatcher.onStart();
    }

    @Override
    protected void onStop() {
        super.onStop();
        smsVerifyCatcher.onStop();
    }

    /**
     * need for Android 6 real time permissions
     */
    @Override
    public void onRequestPermissionsResult(int requestCode, @NonNull String[] permissions, @NonNull int[] grantResults) {
        super.onRequestPermissionsResult(requestCode, permissions, grantResults);
        smsVerifyCatcher.onRequestPermissionsResult(requestCode, permissions, grantResults);
    }
```

You can set phone number filter:
```java
    smsVerifyCatcher.setPhoneNumberFilter("777");
```
or set message filter via regexp:
```java
   smsVerifyCatcher.setFilter("<regexp>");
```
That's all! 
Take a look at the [sample project](sample) for more information
