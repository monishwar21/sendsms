
# Ex.No:6 Design an android application Send SMS using Intent.


## AIM:

To create and design an android application Send SMS using Intent using Android Studio.

## EQUIPMENTS REQUIRED:

Android Studio(Latest Version)

## ALGORITHM:

Step 1: Open Android Stdio and then click on File -> New -> New project.

Step 2: Then type the Application name as smsintent and click Next. 

Step 3: Then select the Minimum SDK as shown below and click Next.

Step 4: Then select the Empty Activity and click Next. Finally click Finish.

Step 5: Design layout in activity_main.xml.

Step 6: Send SMS and Display details give in MainActivity file.

Step 7: Save and run the application.

## PROGRAM:
```
/*
Program to create and design an android application Send SMS using Intent.
Developed by: K MONISHWAR
Registeration Number : 212225230188
*/
```
## Activity_main.xml
```
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/main"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="#E3F2FD"
    android:padding="24dp"
    tools:context=".MainActivity">

    <TextView
        android:id="@+id/textView"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="16dp"
        android:gravity="center"
        android:text="@string/title_sending_sms"
        android:textColor="#1A237E"
        android:textSize="24sp"
        android:textStyle="bold"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent" />

    <TextView
        android:id="@+id/textView2"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="32dp"
        android:text="@string/label_phone_number"
        android:textColor="#0D0D0D"
        android:textSize="16sp"
        android:textStyle="bold"
        app:layout_constraintStart_toStartOf="@+id/editTextText"
        app:layout_constraintTop_toBottomOf="@+id/textView" />

    <EditText
        android:id="@+id/editTextText"
        android:layout_width="0dp"
        android:layout_height="wrap_content"
        android:layout_marginTop="8dp"
        android:background="#FFFFFF"
        android:backgroundTint="#FFFFFF"
        android:ems="10"
        android:hint="@string/hint_enter_number"
        android:importantForAutofill="no"
        android:inputType="phone"
        android:padding="12dp"
        android:textColor="#100F0F"
        android:textColorHint="#9E9E9E"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.0"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/textView2" />

    <TextView
        android:id="@+id/textView3"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="24dp"
        android:text="@string/label_message"
        android:textColor="#070707"
        android:textSize="16sp"
        android:textStyle="bold"
        app:layout_constraintStart_toStartOf="@+id/editTextTextMultiLine2"
        app:layout_constraintTop_toBottomOf="@+id/editTextText" />

    <EditText
        android:id="@+id/editTextTextMultiLine2"
        android:layout_width="0dp"
        android:layout_height="wrap_content"
        android:layout_marginTop="8dp"
        android:background="#FFFFFF"
        android:backgroundTint="#FFFFFF"
        android:ems="10"
        android:gravity="start|top"
        android:hint="@string/hint_enter_message"
        android:importantForAutofill="no"
        android:inputType="textMultiLine"
        android:minLines="4"
        android:padding="12dp"
        android:textColor="#0F0E0E"
        android:textColorHint="#9E9E9E"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.0"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/textView3" />

    <LinearLayout
        android:id="@+id/buttonLayout"
        android:layout_width="0dp"
        android:layout_height="wrap_content"
        android:layout_marginTop="32dp"
        android:gravity="center"
        android:orientation="horizontal"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/editTextTextMultiLine2">

        <Button
            android:id="@+id/buttonSend"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:layout_marginEnd="8dp"
            android:backgroundTint="#4CAF50"
            android:text="@string/btn_send"
            android:textColor="#FFFFFF"
            android:textStyle="bold" />

        <Button
            android:id="@+id/buttonClear"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:layout_marginStart="8dp"
            android:backgroundTint="#FF5722"
            android:text="@string/btn_clear"
            android:textColor="#FFFFFF"
            android:textStyle="bold" />

    </LinearLayout>

</androidx.constraintlayout.widget.ConstraintLayout>

```
## MainActivity.java
```
package com.example.sms;

import android.content.ActivityNotFoundException;
import android.content.Intent;
import android.net.Uri;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.EditText;
import android.widget.Toast;

import androidx.appcompat.app.AppCompatActivity;

public class MainActivity extends AppCompatActivity {

    private EditText inputPh;
    private EditText inputMsg;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        inputPh = findViewById(R.id.editTextText);
        inputMsg = findViewById(R.id.editTextTextMultiLine2);
        Button btn = findViewById(R.id.buttonSend);

        btn.setOnClickListener(this::sendSms);
    }

    public void sendSms(View v) {
        String phoneNumber = inputPh.getText().toString().trim();
        String message = inputMsg.getText().toString().trim();

        if (phoneNumber.isEmpty() || message.isEmpty()) {
            Toast.makeText(this, "Please enter both phone number and message", Toast.LENGTH_SHORT).show();
            return;
        }

        Intent i = new Intent(Intent.ACTION_SENDTO);
        i.setData(Uri.parse("smsto:" + Uri.encode(phoneNumber)));
        i.putExtra("sms_body", message);
        i.putExtra(Intent.EXTRA_TEXT, message);

        try {
            startActivity(i);
        } catch (ActivityNotFoundException e) {
            Toast.makeText(this, "No SMS app found on this device", Toast.LENGTH_SHORT).show();
        }
    }
}

```
## AndroidManifest.xml
```
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools">

    <queries>
        <intent>
            <action android:name="android.intent.action.SENDTO" />
            <data android:scheme="smsto" />
        </intent>
    </queries>

    <application
        android:allowBackup="true"
        android:dataExtractionRules="@xml/data_extraction_rules"
        android:fullBackupContent="@xml/backup_rules"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:roundIcon="@mipmap/ic_launcher_round"
        android:supportsRtl="true"
        android:theme="@style/Theme.SendingSms">
        <activity
            android:name=".MainActivity"
            android:exported="true"
            android:windowSoftInputMode="adjustResize">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />

                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
    </application>

</manifest>
```
## OUTPUT
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/230a0b38-10ed-4e92-9143-bea504982ce0" />
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/db7e0fb3-1b51-433b-86dc-35f9ace6392e" />
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/a76ab169-4663-48e9-ab3d-f5e7671d5cdc" />
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/072550b5-241c-401a-9e81-c17739590b7c" />



## RESULT
Thus a Simple Android Application create and design an android application Send SMS using Intent using Android Studio is developed and executed successfully.
