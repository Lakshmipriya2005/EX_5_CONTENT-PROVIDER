
# Ex.No:5 Create Your Own Content Providers to get Contacts details.


## AIM:

To create your own content providers to get contacts details using Android Studio.

## EQUIPMENTS REQUIRED:

Android Studio(Latest Version)

## ALGORITHM:

Step 1: Open Android Stdio and then click on File -> New -> New project.

Step 2: Then type the Application name as “contentprovider″ and click Next. 

Step 3: Then select the Minimum SDK as shown below and click Next.

Step 4: Then select the Empty Activity and click Next. Finally click Finish.

Step 5: Design layout in activity_main.xml.

Step 6: Get contacts details and Display details give in MainActivity file.

Step 7: Save and run the application.

## PROGRAM:
```
/*
Program to print the contact name and phone number using content providers.
Developed by:APARNA RB
Registeration Number :212222220005
*/
```
## Mainactivity.java:
```
package com.example.ex5;
import android.support.v7.app.AppCompatActivity;
import android.database.Cursor;
import android.os.Bundle;
import android.provider.ContactsContract;
import android.util.Log;
import android.view.View;
import android.widget.Button;
import android.widget.TextView;
import android.widget.Toast;


public class MainActivity extends AppCompatActivity {

    private TextView textViewContacts;
    int count=0;

    @Override
    protected void onCreate(Bundle savedInstanceState) {

        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        Button buttonLoadContacts = findViewById(R.id.button);

        buttonLoadContacts.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                loadContacts();
            }
        });
    }

    private void loadContacts() {
        StringBuilder stringBuilder = new StringBuilder();

        Cursor cursor = getContentResolver().query(ContactsContract.CommonDataKinds.Phone.CONTENT_URI,
                null, null, null, null);

        if (cursor != null && cursor.getCount() > 0) {
            int nameIndex = cursor.getColumnIndex(ContactsContract.CommonDataKinds.Phone.DISPLAY_NAME_PRIMARY);
            int phoneIndex = cursor.getColumnIndex(ContactsContract.CommonDataKinds.Phone.NUMBER);

            while (cursor.moveToNext()) {
                String name = nameIndex != -1 ? cursor.getString(nameIndex) : "No Name";
                String phoneNumber = phoneIndex != -1 ? cursor.getString(phoneIndex) : "No Phone Number";

                stringBuilder.append("Name: ").append(name).append("\n").append("Phone: ").append(phoneNumber).append("\n\n");
                count = count+1;
            }
            cursor.close();
            textViewContacts.setText(stringBuilder.toString());
            Log.i("Content Provider Demo",stringBuilder.toString());
        } else {
            Toast.makeText(this, "No contacts found", Toast.LENGTH_SHORT).show();
        }

        System.out.println("Total Count of Contacts: "+count);}
}
```
## Activitymain.XML:
```
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">

    <Button
        android:id="@+id/button"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Load Contacts"
        android:layout_centerHorizontal="true"
        android:backgroundTint="#2196F3"
        android:layout_marginTop="50dp"/>


</RelativeLayout>
```

## OUTPUT

![369594913-fc6194d0-2547-4b2b-b77f-be7c2d0b2899](https://github.com/user-attachments/assets/3f495962-7758-4e8a-89db-75dccb28c411)
![369594924-25f9c3b7-d55d-4138-8027-752d06507e34](https://github.com/user-attachments/assets/30786beb-f522-4f92-a1e2-382cb2bf9eec)



## RESULT
Thus a Simple Android Application create your own content providers to get contacts details using Android Studio is developed and executed successfully.
