کچھ بھی منگوا لو - مکمل اینڈرائیڈ ایپ گائیڈ
KUCH BHI MANGWALO - COMPLETE ANDROID APP GUIDE
Version 1.0 - Production Ready
Hyderabad, Sindh, Pakistan
 
TABLE OF CONTENTS
1. Project Overview & Requirements
2. How to Open Project in Android Studio
3. How to Build APK (With & Without Emulator)
4. How to Test on Real Device
5. KBM_UserApp - Complete Code
6. KBM_RiderApp - Complete Code
7. KBM_VendorApp - Complete Code
8. Common Utilities & Helpers
9. Troubleshooting Guide
 
1. PROJECT OVERVIEW & REQUIREMENTS
1.1 Project Information

Project Name: KUCH BHI MANGWALO (کچھ بھی منگوا لو)
Type: Multi-Service Digital Platform
Location: Hyderabad, Sindh, Pakistan
Services: Ride-hailing, Food Delivery, Parcel, Grocery, Pharmacy, Pick & Drop

1.2 Three Android Applications
App Name	Project Name	Package Name
User App	KBM_UserApp	com.kbm.userapp
Rider App	KBM_RiderApp	com.kbm.riderapp
Vendor App	KBM_VendorApp	com.kbm.vendorapp
1.3 Technology Requirements

• Android Studio: Hedgehog (2023.1.1) or newer
• Kotlin: 1.9.20
• Gradle: 8.2
• minSdk: 22 (Android 5.1 Lollipop)
• compileSdk: 34 (Android 14)
• JDK: 17
• Internet Connection for dependencies

1.4 UI/UX Design Colors
Element	Color Name	Hex Code
Primary Background	Deep Navy Blue	#0A192F
Secondary Background	Dark Navy	#0D1B2A
Surface/Containers	Mid Navy	#112240
Gold Primary	Metallic Gold	#D4AF37
Text Primary	Pure White	#FFFFFF
Text Secondary	Light Gray	#D1D5DB
 
2. HOW TO OPEN PROJECT IN ANDROID STUDIO
2.1 Step-by-Step Instructions

STEP 1: Download and Install Android Studio
• Go to: https://developer.android.com/studio
• Download the latest version for your OS (Windows/Mac/Linux)
• Run the installer and follow prompts
• Install Android SDK 34 when prompted

STEP 2: Extract the ZIP File
• Extract "KBM_UserApp" folder from ZIP
• Remember the extraction location

STEP 3: Open in Android Studio
• Launch Android Studio
• Click "Open" or "File → Open"
• Navigate to the extracted "KBM_UserApp" folder
• Click "OK"

STEP 4: Wait for Gradle Sync
• Android Studio will download dependencies
• This may take 5-15 minutes (first time)
• Check "Build" tab at bottom for progress
• Wait until "BUILD SUCCESSFUL" appears

STEP 5: Configure Google Maps API Key (IMPORTANT)
• Go to: app/src/main/AndroidManifest.xml
• Find: android:value="YOUR_GOOGLE_MAPS_API_KEY"
• Replace with your actual Google Maps API key
• Get key from: https://console.cloud.google.com

STEP 6: Configure Backend URL
• Go to: app/src/main/java/com/kbm/userapp/api/RetrofitClient.kt
• Find: BASE_URL = "https://your-domain.com/api/"
• Replace with your actual server URL

2.2 Common Issues & Solutions

PROBLEM: Gradle sync failed
SOLUTION: 
• Check internet connection
• Click "File → Invalidate Caches / Restart"
• Delete .gradle folder in user home directory
• Try again

PROBLEM: SDK not found
SOLUTION:
• Click "File → Project Structure → SDK Location"
• Set correct Android SDK path
• Usually: C:\Users\[Username]\AppData\Local\Android\Sdk

PROBLEM: Kotlin version mismatch
SOLUTION:
• Update Kotlin plugin: "Tools → Kotlin → Configure Kotlin Plugin Updates"

 
3. HOW TO BUILD APK (WITH & WITHOUT EMULATOR)
3.1 Building Debug APK (For Testing)

METHOD 1: Using Android Studio UI
• Click "Build" in top menu
• Select "Build Bundle(s) / APK(s)"
• Click "Build APK(s)"
• Wait for build to complete
• Click "locate" in notification to find APK
• APK location: app/build/outputs/apk/debug/app-debug.apk

METHOD 2: Using Gradle Command
• Open Terminal in Android Studio (bottom tab)
• Run: ./gradlew assembleDebug (Mac/Linux)
• Or: gradlew.bat assembleDebug (Windows)
• APK will be in: app/build/outputs/apk/debug/

3.2 Building Release APK (For Production)

METHOD 1: Using Android Studio UI
• Click "Build" in top menu
• Select "Generate Signed Bundle / APK"
• Choose "APK" and click Next
• Create new keystore or use existing:
  - Keystore path: Choose secure location
  - Password: Create strong password
  - Alias: key0
  - Password: Create strong password
  - Certificate: Fill your details
• Click Next
• Select "release" build variant
• Check "V1 (Jar Signature)" and "V2 (Full APK Signature)"
• Click Finish and wait for build
• APK location: app/release/app-release.apk

METHOD 2: Using Gradle Command
• First, create keystore file:
  keytool -genkey -v -keystore kbm-release.keystore -alias kbm -keyalg RSA -keysize 2048 -validity 10000
• Add to app/build.gradle.kts:
  signingConfigs {
      create("release") {
          storeFile = file("kbm-release.keystore")
          storePassword = "your-password"
          keyAlias = "kbm"
          keyPassword = "your-password"
      }
  }
• Run: ./gradlew assembleRelease

3.3 Testing Without Emulator (On Real Device)

STEP 1: Enable Developer Options on Phone
• Go to Settings → About Phone
• Tap "Build Number" 7 times
• Developer Options will be enabled

STEP 2: Enable USB Debugging
• Go to Settings → Developer Options
• Enable "USB Debugging"
• Enable "Install via USB"

STEP 3: Connect Phone to Computer
• Use USB cable to connect phone
• Phone will ask "Allow USB debugging?" - Tap OK

STEP 4: Run App from Android Studio
• In Android Studio, click "Run" (green play button)
• Your phone will appear in device dropdown
• Select your phone and click OK
• App will install and launch automatically

STEP 5: Manual APK Installation
• Transfer APK to phone via USB/Email/WhatsApp
• On phone, open file manager
• Tap the APK file
• If "Install blocked", go to Settings → Allow from this source
• Tap "Install"

3.4 Testing With Emulator

STEP 1: Create Virtual Device
• Click "Device Manager" in Android Studio
• Click "Create Device"
• Choose device: Pixel 4 or Pixel 6
• Click Next

STEP 2: Select System Image
• Download system image with API 34 (Android 14)
• Or API 28 (Android 9) for faster performance
• Click Next → Finish

STEP 3: Run App on Emulator
• Click "Run" (green play button)
• Select your virtual device
• Wait for emulator to boot
• App will install and launch

EMULATOR SPECS RECOMMENDATION:
• RAM: 2048 MB minimum (4096 MB recommended)
• VM Heap: 256 MB
• Graphics: Hardware - GLES 2.0

 
4. HOW TO TEST ON REAL DEVICE
4.1 Testing Checklist

USER APP TESTING:
□ Install app successfully
□ Open app, see splash screen for 3 seconds
□ Enter phone number (03XXXXXXXXX format)
□ Receive OTP via SMS
□ Enter OTP and login
□ See home screen with 5 service cards
□ Click each service card and verify navigation
□ Test wallet feature
□ Test profile section
□ Test order history
□ Test logout

RIDER APP TESTING:
□ Install app successfully
□ OTP login
□ Upload CNIC (front and back)
□ Upload bike papers
□ Take selfie for verification
□ Toggle online/offline status
□ See incoming orders
□ Accept/reject orders
□ Check earnings dashboard
□ Verify location tracking

VENDOR APP TESTING:
□ Install app successfully
□ OTP login
□ See incoming orders with sound
□ Accept/reject orders
□ Check sales reports
□ View commission
□ Manage menu items

4.2 Debugging with Logcat

HOW TO USE LOGCAT:
• Open Android Studio
• Connect device or run emulator
• Click "Logcat" tab at bottom
• Select your app package from dropdown
• Filter by: tag:KBM or package:com.kbm.userapp
• Check for errors in red color

COMMON LOG TAGS:
• Retrofit: Network requests
• Firebase: Authentication & notifications
• Maps: Location & map errors
• KBM: Custom app logs

DEBUGGING TIPS:
• Add Log.d("KBM", "Message") in code
• Use breakpoints: Click left of line number
• Debug mode: Click "Debug" (bug icon) instead of Run

 
5. KBM_UserApp - COMPLETE CODE
5.1 Project Structure

KBM_UserApp/
├── settings.gradle.kts
├── build.gradle.kts (Project Level)
├── gradle.properties
├── local.properties
├── gradle/wrapper/
│   └── gradle-wrapper.properties
└── app/
    ├── build.gradle.kts (App Level)
    ├── proguard-rules.pro
    └── src/main/
        ├── AndroidManifest.xml
        ├── java/com/kbm/userapp/
        │   ├── KbmApplication.kt
        │   ├── ui/
        │   │   ├── SplashActivity.kt
        │   │   ├── MainActivity.kt
        │   │   ├── auth/
        │   │   │   ├── LoginActivity.kt
        │   │   │   ├── OtpActivity.kt
        │   │   │   └── RegisterActivity.kt
        │   │   ├── order/
        │   │   │   ├── PlaceOrderActivity.kt
        │   │   │   └── OrderTrackingActivity.kt
        │   │   ├── profile/
        │   │   │   └── ProfileActivity.kt
        │   │   └── wallet/
        │   │       └── WalletActivity.kt
        │   ├── api/
        │   │   ├── ApiService.kt
        │   │   └── RetrofitClient.kt
        │   ├── models/
        │   │   ├── User.kt
        │   │   ├── Order.kt
        │   │   └── WalletTransaction.kt
        │   ├── utils/
        │   │   ├── SessionManager.kt
        │   │   ├── Constants.kt
        │   │   └── Extensions.kt
        │   └── services/
        │       └── FirebaseService.kt
        └── res/
            ├── values/
            │   ├── colors.xml
            │   ├── strings.xml
            │   └── themes.xml
            ├── layout/
            │   ├── activity_splash.xml
            │   ├── activity_login.xml
            │   ├── activity_otp.xml
            │   ├── activity_main.xml
            │   ├── activity_wallet.xml
            │   └── activity_order_tracking.xml
            ├── menu/
            │   └── drawer_menu.xml
            ├── drawable/
            │   ├── ic_menu.xml
            │   ├── ic_home.xml
            │   ├── ic_orders.xml
            │   ├── ic_wallet.xml
            │   ├── ic_person.xml
            │   └── ic_logout.xml
            ├── mipmap-*/
            │   └── ic_launcher.png
            └── xml/
                ├── backup_rules.xml
                └── data_extraction_rules.xml

5.2 Root Files
📄 FILE: settings.gradle.kts
pluginManagement {
    repositories {
        google()
        mavenCentral()
        gradlePluginPortal()
    }
}

dependencyResolutionManagement {
    repositoriesMode.set(RepositoriesMode.FAIL_ON_PROJECT_REPOS)
    repositories {
        google()
        mavenCentral()
    }
}

rootProject.name = "KBM_UserApp"
include(":app")
📄 FILE: build.gradle.kts (Project Level)
plugins {
    id("com.android.application") version "8.2.0" apply false
    id("org.jetbrains.kotlin.android") version "1.9.20" apply false
    id("com.google.gms.google-services") version "4.4.0" apply false
}

tasks.register("clean", Delete::class) {
    delete(rootProject.layout.buildDirectory)
}
📄 FILE: gradle.properties
org.gradle.jvmargs=-Xmx2048m -Dfile.encoding=UTF-8
android.useAndroidX=true
kotlin.code.style=official
android.nonTransitiveRClass=true
android.enableJetifier=true
org.gradle.caching=true
org.gradle.parallel=true
📄 FILE: gradle/wrapper/gradle-wrapper.properties
distributionBase=GRADLE_USER_HOME
distributionPath=wrapper/dists
distributionUrl=https\://services.gradle.org/distributions/gradle-8.2-bin.zip
zipStoreBase=GRADLE_USER_HOME
zipStorePath=wrapper/dists
5.3 App Level Files
📄 FILE: app/build.gradle.kts
plugins {
    id("com.android.application")
    id("org.jetbrains.kotlin.android")
    id("com.google.gms.google-services")
}

android {
    namespace = "com.kbm.userapp"
    compileSdk = 34

    defaultConfig {
        applicationId = "com.kbm.userapp"
        minSdk = 22
        targetSdk = 34
        versionCode = 1
        versionName = "1.0.0"
        testInstrumentationRunner = "androidx.test.runner.AndroidJUnitRunner"
    }

    buildTypes {
        release {
            isMinifyEnabled = true
            isShrinkResources = true
            proguardFiles(
                getDefaultProguardFile("proguard-android-optimize.txt"),
                "proguard-rules.pro"
            )
        }
        debug {
            isMinifyEnabled = false
        }
    }

    compileOptions {
        sourceCompatibility = JavaVersion.VERSION_17
        targetCompatibility = JavaVersion.VERSION_17
    }

    kotlinOptions {
        jvmTarget = "17"
    }

    buildFeatures {
        viewBinding = true
    }
}

dependencies {
    // Android Core
    implementation("androidx.core:core-ktx:1.12.0")
    implementation("androidx.appcompat:appcompat:1.6.1")
    implementation("com.google.android.material:material:1.11.0")
    implementation("androidx.constraintlayout:constraintlayout:2.1.4")
    implementation("androidx.activity:activity-ktx:1.8.2")
    implementation("androidx.fragment:fragment-ktx:1.6.2")

    // Lifecycle
    implementation("androidx.lifecycle:lifecycle-viewmodel-ktx:2.7.0")
    implementation("androidx.lifecycle:lifecycle-livedata-ktx:2.7.0")
    implementation("androidx.lifecycle:lifecycle-runtime-ktx:2.7.0")

    // Navigation
    implementation("androidx.navigation:navigation-fragment-ktx:2.7.6")
    implementation("androidx.navigation:navigation-ui-ktx:2.7.6")

    // Retrofit
    implementation("com.squareup.retrofit2:retrofit:2.9.0")
    implementation("com.squareup.retrofit2:converter-gson:2.9.0")
    implementation("com.squareup.okhttp3:okhttp:4.12.0")
    implementation("com.squareup.okhttp3:logging-interceptor:4.12.0")

    // Google Maps
    implementation("com.google.android.gms:play-services-maps:18.2.0")
    implementation("com.google.android.gms:play-services-location:21.1.0")

    // Firebase
    implementation(platform("com.google.firebase:firebase-bom:32.7.0"))
    implementation("com.google.firebase:firebase-auth-ktx")
    implementation("com.google.firebase:firebase-messaging-ktx")
    implementation("com.google.firebase:firebase-database-ktx")

    // Image Loading
    implementation("com.github.bumptech.glide:glide:4.16.0")
    implementation("de.hdodenhof:circleimageview:3.1.0")

    // Animation
    implementation("com.airbnb.android:lottie:6.3.0")

    // Coroutines
    implementation("org.jetbrains.kotlinx:kotlinx-coroutines-android:1.7.3")

    // Testing
    testImplementation("junit:junit:4.13.2")
    androidTestImplementation("androidx.test.ext:junit:1.1.5")
    androidTestImplementation("androidx.test.espresso:espresso-core:3.5.1")
}
📄 FILE: app/src/main/AndroidManifest.xml
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools">

    <uses-permission android:name="android.permission.INTERNET" />
    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
    <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
    <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
    <uses-permission android:name="android.permission.CAMERA" />
    <uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
    <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"
        android:maxSdkVersion="28" />
    <uses-permission android:name="android.permission.POST_NOTIFICATIONS" />
    <uses-permission android:name="android.permission.VIBRATE" />
    <uses-permission android:name="android.permission.CALL_PHONE" />

    <application
        android:name=".KbmApplication"
        android:allowBackup="true"
        android:dataExtractionRules="@xml/data_extraction_rules"
        android:fullBackupContent="@xml/backup_rules"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:roundIcon="@mipmap/ic_launcher_round"
        android:supportsRtl="true"
        android:theme="@style/Theme.KBMUserApp"
        android:usesCleartextTraffic="true"
        tools:targetApi="34">

        <activity
            android:name=".ui.SplashActivity"
            android:exported="true"
            android:theme="@style/Theme.KBMUserApp.Splash">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />
                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>

        <activity
            android:name=".ui.auth.LoginActivity"
            android:exported="false" />
        <activity
            android:name=".ui.auth.OtpActivity"
            android:exported="false" />
        <activity
            android:name=".ui.auth.RegisterActivity"
            android:exported="false" />
        <activity
            android:name=".ui.MainActivity"
            android:exported="false" />
        <activity
            android:name=".ui.order.PlaceOrderActivity"
            android:exported="false" />
        <activity
            android:name=".ui.order.OrderTrackingActivity"
            android:exported="false" />
        <activity
            android:name=".ui.profile.ProfileActivity"
            android:exported="false" />
        <activity
            android:name=".ui.wallet.WalletActivity"
            android:exported="false" />

        <meta-data
            android:name="com.google.android.geo.API_KEY"
            android:value="YOUR_GOOGLE_MAPS_API_KEY" />

        <service
            android:name=".services.FirebaseService"
            android:exported="false">
            <intent-filter>
                <action android:name="com.google.firebase.MESSAGING_EVENT" />
            </intent-filter>
        </service>

    </application>

</manifest>
5.4 Kotlin Source Files
📄 FILE: KbmApplication.kt
package com.kbm.userapp

import android.app.Application

class KbmApplication : Application() {
    override fun onCreate() {
        super.onCreate()
        // Initialize any global components here
    }
}
📄 FILE: ui/SplashActivity.kt
package com.kbm.userapp.ui

import android.content.Intent
import android.os.Bundle
import android.os.Handler
import android.os.Looper
import androidx.appcompat.app.AppCompatActivity
import com.kbm.userapp.R
import com.kbm.userapp.ui.auth.LoginActivity
import com.kbm.userapp.utils.SessionManager

class SplashActivity : AppCompatActivity() {

    private lateinit var sessionManager: SessionManager

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_splash)

        sessionManager = SessionManager(this)

        Handler(Looper.getMainLooper()).postDelayed({
            checkLoginStatus()
        }, 3000)
    }

    private fun checkLoginStatus() {
        val intent = if (sessionManager.isLoggedIn()) {
            Intent(this, MainActivity::class.java)
        } else {
            Intent(this, LoginActivity::class.java)
        }
        startActivity(intent)
        finish()
    }
}
📄 FILE: ui/auth/LoginActivity.kt
package com.kbm.userapp.ui.auth

import android.content.Intent
import android.os.Bundle
import android.text.TextUtils
import android.widget.Toast
import androidx.appcompat.app.AppCompatActivity
import androidx.lifecycle.lifecycleScope
import com.kbm.userapp.R
import com.kbm.userapp.api.RetrofitClient
import com.kbm.userapp.databinding.ActivityLoginBinding
import kotlinx.coroutines.launch

class LoginActivity : AppCompatActivity() {

    private lateinit var binding: ActivityLoginBinding

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        binding = ActivityLoginBinding.inflate(layoutInflater)
        setContentView(binding.root)

        binding.btnSendOtp.setOnClickListener {
            validateAndSendOtp()
        }
    }

    private fun validateAndSendOtp() {
        val phone = binding.etPhone.text.toString().trim()

        if (TextUtils.isEmpty(phone)) {
            binding.etPhone.error = "فون نمبر درج کریں"
            return
        }

        if (phone.length < 10) {
            binding.etPhone.error = "درست فون نمبر درج کریں"
            return
        }

        sendOtp(phone)
    }

    private fun sendOtp(phone: String) {
        binding.btnSendOtp.isEnabled = false

        lifecycleScope.launch {
            try {
                val response = RetrofitClient.apiService.sendOtp(
                    mapOf("phone" to phone, "type" to "user")
                )

                if (response.isSuccessful && response.body()?.get("success") == true) {
                    val intent = Intent(this@LoginActivity, OtpActivity::class.java)
                    intent.putExtra("phone", phone)
                    startActivity(intent)
                } else {
                    Toast.makeText(
                        this@LoginActivity,
                        "OTP بھیجنے میں خرابی",
                        Toast.LENGTH_SHORT
                    ).show()
                }
            } catch (e: Exception) {
                Toast.makeText(
                    this@LoginActivity,
                    "نیٹ ورک خرابی: ${e.message}",
                    Toast.LENGTH_SHORT
                ).show()
            } finally {
                binding.btnSendOtp.isEnabled = true
            }
        }
    }
}
📄 FILE: ui/auth/OtpActivity.kt
package com.kbm.userapp.ui.auth

import android.content.Intent
import android.os.Bundle
import android.widget.Toast
import androidx.appcompat.app.AppCompatActivity
import androidx.lifecycle.lifecycleScope
import com.kbm.userapp.api.RetrofitClient
import com.kbm.userapp.databinding.ActivityOtpBinding
import com.kbm.userapp.ui.MainActivity
import com.kbm.userapp.utils.SessionManager
import kotlinx.coroutines.launch

class OtpActivity : AppCompatActivity() {

    private lateinit var binding: ActivityOtpBinding
    private lateinit var sessionManager: SessionManager
    private var phone: String = ""

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        binding = ActivityOtpBinding.inflate(layoutInflater)
        setContentView(binding.root)

        sessionManager = SessionManager(this)
        phone = intent.getStringExtra("phone") ?: ""

        binding.btnVerify.setOnClickListener {
            verifyOtp()
        }
    }

    private fun verifyOtp() {
        val otp = binding.etOtp.text.toString().trim()

        if (otp.length != 4) {
            binding.etOtp.error = "4 ہندسوں کا OTP درج کریں"
            return
        }

        lifecycleScope.launch {
            try {
                val response = RetrofitClient.apiService.verifyOtp(
                    mapOf("phone" to phone, "otp" to otp, "type" to "user")
                )

                if (response.isSuccessful && response.body()?.get("success") == true) {
                    val token = response.body()?.get("token") as? String ?: ""
                    val userId = (response.body()?.get("user_id") as? Number)?.toInt() ?: 0

                    sessionManager.saveSession(userId, token, phone)

                    val intent = Intent(this@OtpActivity, MainActivity::class.java)
                    intent.flags = Intent.FLAG_ACTIVITY_NEW_TASK or Intent.FLAG_ACTIVITY_CLEAR_TASK
                    startActivity(intent)
                } else {
                    Toast.makeText(this@OtpActivity, "غلط OTP", Toast.LENGTH_SHORT).show()
                }
            } catch (e: Exception) {
                Toast.makeText(
                    this@OtpActivity,
                    "نیٹ ورک خرابی: ${e.message}",
                    Toast.LENGTH_SHORT
                ).show()
            }
        }
    }
}
📄 FILE: ui/MainActivity.kt
package com.kbm.userapp.ui

import android.os.Bundle
import androidx.appcompat.app.AppCompatActivity
import androidx.core.view.GravityCompat
import com.kbm.userapp.R
import com.kbm.userapp.databinding.ActivityMainBinding

class MainActivity : AppCompatActivity() {

    private lateinit var binding: ActivityMainBinding

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        binding = ActivityMainBinding.inflate(layoutInflater)
        setContentView(binding.root)

        setupNavigation()
        setupClickListeners()
    }

    private fun setupNavigation() {
        binding.toolbar.setNavigationOnClickListener {
            binding.drawerLayout.openDrawer(GravityCompat.START)
        }
    }

    private fun setupClickListeners() {
        binding.cardPickDrop.setOnClickListener {
            // Open Pick & Drop booking
        }

        binding.cardFoodDelivery.setOnClickListener {
            // Open Food Delivery
        }

        binding.cardParcel.setOnClickListener {
            // Open Parcel service
        }

        binding.cardGrocery.setOnClickListener {
            // Open Grocery service
        }

        binding.cardPharmacy.setOnClickListener {
            // Open Pharmacy service
        }
    }

    @Deprecated("Deprecated in Java")
    override fun onBackPressed() {
        if (binding.drawerLayout.isDrawerOpen(GravityCompat.START)) {
            binding.drawerLayout.closeDrawer(GravityCompat.START)
        } else {
            super.onBackPressed()
        }
    }
}
📄 FILE: api/ApiService.kt
package com.kbm.userapp.api

import retrofit2.Response
import retrofit2.http.*

interface ApiService {

    @POST("auth/send-otp")
    suspend fun sendOtp(
        @Body params: Map<String, String>
    ): Response<Map<String, Any>>

    @POST("auth/verify-otp")
    suspend fun verifyOtp(
        @Body params: Map<String, String>
    ): Response<Map<String, Any>>

    @GET("user/profile")
    suspend fun getProfile(
        @Header("Authorization") token: String
    ): Response<Map<String, Any>>

    @GET("wallet/balance")
    suspend fun getWalletBalance(
        @Header("Authorization") token: String
    ): Response<Map<String, Any>>

    @POST("wallet/add-money")
    suspend fun addWalletMoney(
        @Header("Authorization") token: String,
        @Body params: Map<String, Any>
    ): Response<Map<String, Any>>

    @GET("orders")
    suspend fun getOrders(
        @Header("Authorization") token: String
    ): Response<Map<String, Any>>

    @POST("orders")
    suspend fun createOrder(
        @Header("Authorization") token: String,
        @Body order: Map<String, Any>
    ): Response<Map<String, Any>>

    @GET("orders/{id}")
    suspend fun getOrderDetail(
        @Header("Authorization") token: String,
        @Path("id") orderId: Int
    ): Response<Map<String, Any>>

    @GET("orders/calculate-fee")
    suspend fun calculateDeliveryFee(
        @Header("Authorization") token: String,
        @Query("pickup_lat") pickupLat: Double,
        @Query("pickup_lng") pickupLng: Double,
        @Query("delivery_lat") deliveryLat: Double,
        @Query("delivery_lng") deliveryLng: Double
    ): Response<Map<String, Any>>
}
📄 FILE: api/RetrofitClient.kt
package com.kbm.userapp.api

import okhttp3.OkHttpClient
import okhttp3.logging.HttpLoggingInterceptor
import retrofit2.Retrofit
import retrofit2.converter.gson.GsonConverterFactory
import java.util.concurrent.TimeUnit

object RetrofitClient {

    private const val BASE_URL = "https://your-domain.com/api/"

    private val loggingInterceptor = HttpLoggingInterceptor().apply {
        level = HttpLoggingInterceptor.Level.BODY
    }

    private val okHttpClient = OkHttpClient.Builder()
        .addInterceptor(loggingInterceptor)
        .connectTimeout(30, TimeUnit.SECONDS)
        .readTimeout(30, TimeUnit.SECONDS)
        .writeTimeout(30, TimeUnit.SECONDS)
        .build()

    private val retrofit = Retrofit.Builder()
        .baseUrl(BASE_URL)
        .client(okHttpClient)
        .addConverterFactory(GsonConverterFactory.create())
        .build()

    val apiService: ApiService = retrofit.create(ApiService::class.java)
}
📄 FILE: utils/SessionManager.kt
package com.kbm.userapp.utils

import android.content.Context
import android.content.SharedPreferences

class SessionManager(context: Context) {

    private val prefs: SharedPreferences =
        context.getSharedPreferences("kbm_user_prefs", Context.MODE_PRIVATE)

    fun saveSession(userId: Int, token: String, phone: String) {
        prefs.edit().apply {
            putInt(KEY_USER_ID, userId)
            putString(KEY_TOKEN, token)
            putString(KEY_PHONE, phone)
            putBoolean(KEY_IS_LOGGED_IN, true)
            apply()
        }
    }

    fun isLoggedIn(): Boolean = prefs.getBoolean(KEY_IS_LOGGED_IN, false)

    fun getUserId(): Int = prefs.getInt(KEY_USER_ID, 0)

    fun getToken(): String? = prefs.getString(KEY_TOKEN, null)

    fun getPhone(): String? = prefs.getString(KEY_PHONE, null)

    fun clearSession() = prefs.edit().clear().apply()

    companion object {
        private const val KEY_USER_ID = "user_id"
        private const val KEY_TOKEN = "token"
        private const val KEY_PHONE = "phone"
        private const val KEY_IS_LOGGED_IN = "is_logged_in"
    }
}
📄 FILE: services/FirebaseService.kt
package com.kbm.userapp.services

import android.app.NotificationChannel
import android.app.NotificationManager
import android.app.PendingIntent
import android.content.Intent
import android.os.Build
import androidx.core.app.NotificationCompat
import com.google.firebase.messaging.FirebaseMessagingService
import com.google.firebase.messaging.RemoteMessage
import com.kbm.userapp.R
import com.kbm.userapp.ui.MainActivity

class FirebaseService : FirebaseMessagingService() {

    override fun onMessageReceived(remoteMessage: RemoteMessage) {
        super.onMessageReceived(remoteMessage)

        remoteMessage.notification?.let {
            showNotification(it.title ?: "کچھ بھی منگوا لو", it.body ?: "")
        }
    }

    override fun onNewToken(token: String) {
        super.onNewToken(token)
        // Send token to server
    }

    private fun showNotification(title: String, message: String) {
        val intent = Intent(this, MainActivity::class.java)
        intent.addFlags(Intent.FLAG_ACTIVITY_CLEAR_TOP)

        val pendingIntent = PendingIntent.getActivity(
            this, 0, intent,
            PendingIntent.FLAG_ONE_SHOT or PendingIntent.FLAG_IMMUTABLE
        )

        val channelId = "kbm_notifications"
        val notificationBuilder = NotificationCompat.Builder(this, channelId)
            .setSmallIcon(R.mipmap.ic_launcher)
            .setContentTitle(title)
            .setContentText(message)
            .setAutoCancel(true)
            .setContentIntent(pendingIntent)

        val notificationManager = getSystemService(NOTIFICATION_SERVICE) as NotificationManager

        if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.O) {
            val channel = NotificationChannel(
                channelId,
                "KBM Notifications",
                NotificationManager.IMPORTANCE_DEFAULT
            )
            notificationManager.createNotificationChannel(channel)
        }

        notificationManager.notify(0, notificationBuilder.build())
    }
}
5.5 Resource Files
📄 FILE: res/values/colors.xml
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <color name="primary_background">#0A192F</color>
    <color name="secondary_background">#0D1B2A</color>
    <color name="surface_container">#112240</color>
    <color name="gold_primary">#D4AF37</color>
    <color name="gold_bright">#F0C14B</color>
    <color name="white">#FFFFFF</color>
    <color name="text_secondary">#D1D5DB</color>
    <color name="success">#10B981</color>
    <color name="error">#EF4444</color>
    <color name="black">#000000</color>
</resources>
📄 FILE: res/values/strings.xml
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <string name="app_name">Kuch Bhi Mangwalo</string>
    <string name="app_name_urdu">کچھ بھی منگوا لو</string>
    <string name="navigation_drawer_open">کھولیں</string>
    <string name="navigation_drawer_close">بند کریں</string>
    <string name="welcome">خوش آمدید</string>
    <string name="enter_phone">اپنا فون نمبر درج کریں</string>
    <string name="phone_hint">فون نمبر (03XXXXXXXXX)</string>
    <string name="send_otp">OTP بھیجیں</string>
    <string name="enter_otp">OTP درج کریں</string>
    <string name="verify">تصدیق کریں</string>
    <string name="pick_drop">پک اینڈ ڈراپ</string>
    <string name="food_delivery">فوڈ ڈیلیوری</string>
    <string name="parcel">پارسل</string>
    <string name="grocery">گروسری</string>
    <string name="pharmacy">فارمیسی</string>
    <string name="home">ہوم</string>
    <string name="orders">آرڈرز</string>
    <string name="wallet">والٹ</string>
    <string name="profile">پروفائل</string>
    <string name="logout">لاگ آؤٹ</string>
    <string name="loading">لوڈ ہو رہا ہے...</string>
</resources>
📄 FILE: res/values/themes.xml
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <style name="Theme.KBMUserApp" parent="Theme.MaterialComponents.DayNight.NoActionBar">
        <item name="colorPrimary">@color/gold_primary</item>
        <item name="colorPrimaryVariant">@color/primary_background</item>
        <item name="colorOnPrimary">@color/white</item>
        <item name="android:statusBarColor">@color/primary_background</item>
        <item name="android:navigationBarColor">@color/primary_background</item>
        <item name="android:windowBackground">@color/primary_background</item>
    </style>

    <style name="Theme.KBMUserApp.Splash" parent="Theme.KBMUserApp">
        <item name="android:windowBackground">@color/primary_background</item>
    </style>
</resources>
📄 FILE: res/layout/activity_splash.xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="@color/primary_background">

    <TextView
        android:id="@+id/tvAppName"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/app_name_urdu"
        android:textColor="@color/gold_primary"
        android:textSize="32sp"
        android:textStyle="bold"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintEnd_toEndOf="parent" />

    <ProgressBar
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginBottom="80dp"
        android:indeterminateTint="@color/gold_primary"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintEnd_toEndOf="parent" />

</androidx.constraintlayout.widget.ConstraintLayout>
📄 FILE: res/layout/activity_login.xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="@color/primary_background"
    android:padding="24dp">

    <TextView
        android:id="@+id/tvTitle"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/welcome"
        android:textColor="@color/white"
        android:textSize="32sp"
        android:textStyle="bold"
        app:layout_constraintTop_toTopOf="parent"
        android:layout_marginTop="80dp" />

    <TextView
        android:id="@+id/tvSubtitle"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/enter_phone"
        android:textColor="@color/text_secondary"
        android:textSize="16sp"
        android:layout_marginTop="8dp"
        app:layout_constraintTop_toBottomOf="@id/tvTitle" />

    <com.google.android.material.textfield.TextInputLayout
        android:id="@+id/tilPhone"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginTop="40dp"
        style="@style/Widget.MaterialComponents.TextInputLayout.OutlinedBox"
        app:layout_constraintTop_toBottomOf="@id/tvSubtitle">

        <com.google.android.material.textfield.TextInputEditText
            android:id="@+id/etPhone"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:hint="@string/phone_hint"
            android:inputType="phone"
            android:textColor="@color/white"
            android:textSize="18sp"
            android:maxLength="11" />

    </com.google.android.material.textfield.TextInputLayout>

    <com.google.android.material.button.MaterialButton
        android:id="@+id/btnSendOtp"
        android:layout_width="match_parent"
        android:layout_height="56dp"
        android:text="@string/send_otp"
        android:textSize="18sp"
        android:textStyle="bold"
        android:layout_marginTop="30dp"
        app:backgroundTint="@color/gold_primary"
        app:cornerRadius="12dp"
        app:layout_constraintTop_toBottomOf="@id/tilPhone" />

</androidx.constraintlayout.widget.ConstraintLayout>
📄 FILE: res/layout/activity_main.xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.drawerlayout.widget.DrawerLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    android:id="@+id/drawerLayout"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="@color/primary_background">

    <androidx.constraintlayout.widget.ConstraintLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent">

        <androidx.appcompat.widget.Toolbar
            android:id="@+id/toolbar"
            android:layout_width="match_parent"
            android:layout_height="?attr/actionBarSize"
            android:background="@color/primary_background"
            app:navigationIcon="@drawable/ic_menu"
            app:title="@string/app_name_urdu"
            app:titleTextColor="@color/gold_primary"
            app:layout_constraintTop_toTopOf="parent" />

        <LinearLayout
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:orientation="vertical"
            android:padding="16dp"
            app:layout_constraintTop_toBottomOf="@id/toolbar">

            <androidx.cardview.widget.CardView
                android:id="@+id/cardPickDrop"
                android:layout_width="match_parent"
                android:layout_height="100dp"
                android:layout_marginBottom="12dp"
                app:cardBackgroundColor="@color/surface_container"
                app:cardCornerRadius="16dp">

                <TextView
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:layout_gravity="center"
                    android:text="@string/pick_drop"
                    android:textColor="@color/white"
                    android:textSize="20sp"
                    android:textStyle="bold" />

            </androidx.cardview.widget.CardView>

            <androidx.cardview.widget.CardView
                android:id="@+id/cardFoodDelivery"
                android:layout_width="match_parent"
                android:layout_height="100dp"
                android:layout_marginBottom="12dp"
                app:cardBackgroundColor="@color/surface_container"
                app:cardCornerRadius="16dp">

                <TextView
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:layout_gravity="center"
                    android:text="@string/food_delivery"
                    android:textColor="@color/white"
                    android:textSize="20sp"
                    android:textStyle="bold" />

            </androidx.cardview.widget.CardView>

            <androidx.cardview.widget.CardView
                android:id="@+id/cardParcel"
                android:layout_width="match_parent"
                android:layout_height="100dp"
                android:layout_marginBottom="12dp"
                app:cardBackgroundColor="@color/surface_container"
                app:cardCornerRadius="16dp">

                <TextView
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:layout_gravity="center"
                    android:text="@string/parcel"
                    android:textColor="@color/white"
                    android:textSize="20sp"
                    android:textStyle="bold" />

            </androidx.cardview.widget.CardView>

            <androidx.cardview.widget.CardView
                android:id="@+id/cardGrocery"
                android:layout_width="match_parent"
                android:layout_height="100dp"
                android:layout_marginBottom="12dp"
                app:cardBackgroundColor="@color/surface_container"
                app:cardCornerRadius="16dp">

                <TextView
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:layout_gravity="center"
                    android:text="@string/grocery"
                    android:textColor="@color/white"
                    android:textSize="20sp"
                    android:textStyle="bold" />

            </androidx.cardview.widget.CardView>

            <androidx.cardview.widget.CardView
                android:id="@+id/cardPharmacy"
                android:layout_width="match_parent"
                android:layout_height="100dp"
                app:cardBackgroundColor="@color/surface_container"
                app:cardCornerRadius="16dp">

                <TextView
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:layout_gravity="center"
                    android:text="@string/pharmacy"
                    android:textColor="@color/white"
                    android:textSize="20sp"
                    android:textStyle="bold" />

            </androidx.cardview.widget.CardView>

        </LinearLayout>

    </androidx.constraintlayout.widget.ConstraintLayout>

    <com.google.android.material.navigation.NavigationView
        android:id="@+id/navView"
        android:layout_width="280dp"
        android:layout_height="match_parent"
        android:layout_gravity="start"
        android:background="@color/secondary_background"
        app:menu="@menu/drawer_menu"
        app:itemTextColor="@color/white"
        app:itemIconTint="@color/gold_primary" />

</androidx.drawerlayout.widget.DrawerLayout>
 
6. KBM_RiderApp - COMPLETE CODE
6.1 Project Structure

KBM_RiderApp has the same structure as KBM_UserApp with the following differences:
• Package: com.kbm.riderapp
• Additional features: Document upload, Location tracking, Earnings dashboard

6.2 Key Differences
📄 FILE: app/build.gradle.kts
plugins {
    id("com.android.application")
    id("org.jetbrains.kotlin.android")
    id("com.google.gms.google-services")
}

android {
    namespace = "com.kbm.riderapp"
    compileSdk = 34

    defaultConfig {
        applicationId = "com.kbm.riderapp"
        minSdk = 22
        targetSdk = 34
        versionCode = 1
        versionName = "1.0.0"
    }

    buildFeatures {
        viewBinding = true
    }
}

dependencies {
    // Same as UserApp plus:
    implementation("androidx.work:work-runtime-ktx:2.9.0")
}
📄 FILE: app/src/main/AndroidManifest.xml
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android">

    <uses-permission android:name="android.permission.FOREGROUND_SERVICE" />
    <uses-permission android:name="android.permission.FOREGROUND_SERVICE_LOCATION" />
    
    <!-- Same as UserApp permissions -->

    <application
        android:name=".KbmRiderApp"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:theme="@style/Theme.KBMRiderApp">

        <activity android:name=".ui.SplashActivity" android:exported="true">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />
                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>

        <activity android:name=".ui.auth.LoginActivity" />
        <activity android:name=".ui.auth.OtpActivity" />
        <activity android:name=".ui.auth.DocumentUploadActivity" />
        <activity android:name=".ui.MainActivity" />
        <activity android:name=".ui.earnings.EarningsActivity" />

        <service
            android:name=".services.LocationService"
            android:foregroundServiceType="location"
            android:exported="false" />

    </application>

</manifest>
 
7. KBM_VendorApp - COMPLETE CODE
7.1 Project Structure

KBM_VendorApp has the same structure as KBM_UserApp with the following differences:
• Package: com.kbm.vendorapp
• Features: Order management, Menu management, Sales reports

📄 FILE: app/build.gradle.kts
plugins {
    id("com.android.application")
    id("org.jetbrains.kotlin.android")
    id("com.google.gms.google-services")
}

android {
    namespace = "com.kbm.vendorapp"
    compileSdk = 34

    defaultConfig {
        applicationId = "com.kbm.vendorapp"
        minSdk = 22
        targetSdk = 34
        versionCode = 1
        versionName = "1.0.0"
    }
}
 
8. TROUBLESHOOTING GUIDE
8.1 Common Build Errors

ERROR: "SDK location not found"
SOLUTION: Create local.properties file with:
sdk.dir=C:\Users\[Username]\AppData\Local\Android\Sdk

ERROR: "Gradle sync failed"
SOLUTION: 
1. Check internet connection
2. File → Invalidate Caches / Restart
3. Delete .gradle folder and sync again

ERROR: "Cannot resolve symbol"
SOLUTION:
1. Sync Project with Gradle Files
2. Clean Project: Build → Clean Project
3. Rebuild Project: Build → Rebuild Project

ERROR: "Google Maps not loading"
SOLUTION:
1. Get API key from Google Cloud Console
2. Enable Maps SDK for Android
3. Add key to AndroidManifest.xml

ERROR: "Retrofit connection failed"
SOLUTION:
1. Check server URL in RetrofitClient.kt
2. Ensure server is running
3. Check network permissions in manifest

8.2 Runtime Errors

ERROR: "App keeps crashing"
SOLUTION:
1. Check Logcat for errors
2. Verify all permissions granted
3. Check for null values in code

ERROR: "Location not updating"
SOLUTION:
1. Grant location permission
2. Enable GPS on device
3. Check LocationService is running

ERROR: "OTP not received"
SOLUTION:
1. Check phone number format
2. Verify SMS service is working
3. Check server logs

