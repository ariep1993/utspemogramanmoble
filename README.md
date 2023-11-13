## **Repositori ini dibuat untuk memenuhi penilaian tengah semester matakuliah pemrograman mobile**  
 Nama  : saripuidn  
 Nim   : 312210077  
 Kelas : TI.22.B1  
 Mata Kuliah : Pemrograman Mobile  
**Tugas : Membuat tombol yang setiap diklik dapat bertambah angkanya, namun dengan urutan angka fibonacci, lalu lengkapi dengan fitur toast**  
berikut adalah link video aplikasi yang di jalankan (dijalankan pada device menggunakan usb debugging) : [tonton video](https://youtu.be/GEkIEAe5ZnY)  
<br>
Source Code:  
* activity_main.Xml (dibuat dengan design pada android studio):
```
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    android:layout_width="match_parent"
    android:layout_height="match_parent">


    <Button
        android:id="@+id/buttonToast"
        android:layout_width="408dp"
        android:layout_height="wrap_content"
        android:text="Tampilkan Toast"
        android:textAlignment="center"
        android:textStyle="bold" />

    <LinearLayout
        android:id="@+id/linear"
        android:layout_width="match_parent"
        android:layout_height="682dp"
        android:layout_below="@id/buttonToast"
        android:layout_alignParentStart="true"
        android:layout_alignParentBottom="true"
        android:layout_marginStart="0dp"
        android:layout_marginTop="-2dp"
        android:layout_marginBottom="3dp"
        android:background="#FFEB3B"
        android:gravity="center"
        android:orientation="vertical"
        android:paddingLeft="20dp"
        android:paddingRight="20dp">

        <TextView
            android:id="@+id/textNama"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_marginTop="-50dp"
            android:layout_marginBottom="20dp"
            android:text="SARIPUDIN 312210077"
            android:textAlignment="center"
            android:textSize="24sp" />

        <TextView
            android:id="@+id/textCount"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="Tombol Hitung diklik sebanyak : 0"
            android:textAlignment="center"
            android:textSize="20sp" />

        <TextView
            android:id="@+id/textCountFibo"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_marginTop="30dp"
            android:layout_marginBottom="-70dp"
            android:text="0"
            android:textAlignment="center"
            android:textColor="#0000ff"
            android:textSize="180sp" />

    </LinearLayout>

    <Button
        android:id="@+id/buttonCount"
        android:layout_width="132dp"
        android:layout_height="wrap_content"
        android:layout_alignParentEnd="true"
        android:layout_alignParentBottom="true"
        android:layout_marginStart="1dp"
        android:layout_marginLeft="1dp"
        android:layout_marginEnd="2dp"
        android:layout_marginBottom="4dp"
        android:text="HITUNG"
        android:textAlignment="center"
        android:textStyle="bold" />

    <Button
        android:id="@+id/buttonReset"
        android:layout_width="142dp"
        android:layout_height="wrap_content"
        android:layout_alignParentStart="true"
        android:layout_alignParentBottom="true"
        android:layout_marginStart="6dp"
        android:layout_marginLeft="1dp"
        android:layout_marginTop="87dp"
        android:layout_marginBottom="3dp"
        android:text="RESET"
        android:backgroundTint="@color/merah"
        android:textStyle="bold" />

</RelativeLayout>
```
* MainActivity.java

 ```
package com.example.app1;

import android.annotation.SuppressLint;
import android.graphics.Color;
import android.support.v4.app.RemoteActionCompatParcelizer;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.TextView;
import android.widget.Toast;

import androidx.appcompat.app.AppCompatActivity;

import com.example.app1.R;

public class MainActivity extends AppCompatActivity {
    public int count = 0;
    public int countFibo = 0;
    public TextView showCount;
    public TextView showCountFibo;
    public Button buttonToast;
    public Button buttonCount;
    public Button buttonReset;
    public Toast toastA;

    @SuppressLint("MissingInflatedId")
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        buttonToast = (Button) findViewById(R.id.buttonToast);
        buttonCount = (Button) findViewById(R.id.buttonCount);
        buttonReset = (Button) findViewById(R.id.buttonReset);
        showCount = (TextView) findViewById(R.id.textCount);
        showCountFibo = (TextView) findViewById(R.id.textCountFibo);


        buttonToast.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                if (toastA != null) {
                    toastA.cancel();
                }
                toastA = Toast.makeText(getApplicationContext(), "Angka Fibonacci : " + countFibo, Toast.LENGTH_SHORT);
                toastA.show();
            }
        });

        buttonCount.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                calculate(view);
            }
        });

        buttonReset.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                reset(view);
            }
        });


    }

    protected void calculate(View view) {

        count++;
        countFibo = calculateFibo(count);
        showCount.setText("Tombol Hitung diklik sebanyak : " + Integer.toString(count));
        showCountFibo.setText(Integer.toString(countFibo));
        if (count % 2 == 0) {
            if (toastA != null) toastA.cancel();
            toastA = Toast.makeText(getApplicationContext(), "Tombol hitung diklik : " + count + " Kali", Toast.LENGTH_SHORT);
            toastA.show();
            showCountFibo.setTextColor(Color.RED);
        }
        else {
            showCountFibo.setTextColor(Color.BLUE);
        }
    }

    protected int calculateFibo(int n) {
        if (n <= 1) return n;
        int prev, current, next;
        prev = 0;
        current = 1;
        for (int i = 2; i <= n; i++) {
            next = prev + current;
            prev = current;
            current = next;
        }
        return current;
    }

    protected void reset(View view) {
        count = 0;
        countFibo = 0;
        showCount.setText(Integer.toString(count));
        showCountFibo.setText(Integer.toString(countFibo));
    }
}

```
* AndroidManifeast.xml
```
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools">

    <application
        android:allowBackup="true"
        android:dataExtractionRules="@xml/data_extraction_rules"
        android:fullBackupContent="@xml/backup_rules"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:roundIcon="@mipmap/ic_launcher_round"
        android:supportsRtl="true"
        android:theme="@style/Theme.App1"
        tools:targetApi="34">
        <activity
            android:name=".MainActivity"
            android:exported="true">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />

                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
    </application>

</manifest>
```
* color.xml
```
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <color name="black">#FF000000</color>
    <color name="white">#FFFFFFFF</color>
    <color name="biru">#0000ff</color>

    <color name="colorPrimary">#3F51B5</color>
    <color name="colorPrimaryDark">#303F9F</color>
    <color name="colorAccent">#FF4081</color>
    <color name="kuning">#FFFF00</color>
    <color name="hijau">#00ff00</color>
    <color name="merah">#ff0006</color>

</resources>
