# practical

Practical 1
Objective: Consider a scenario: 

A developer develops the simple “SMS App”. The app functionality is as follows 
a. Simple SMS functionality. 
b. When you open the app it asks you your “age”. 
c. If “age” is less than 16, then the app will ask you your parent’s number. 
d. If you send more than 10 messages the report goes to your parent. Test this app. Write all the possible test cases for this app. 

Prerequisites: Candidate should familiar with how to use controls and basic operations in android application environment.

Steps/Process
 

Main Activity file (xml)
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:paddingBottom="@dimen/activity_vertical_margin"
    android:paddingLeft="@dimen/activity_horizontal_margin"
    android:paddingRight="@dimen/activity_horizontal_margin"
    android:paddingTop="@dimen/activity_vertical_margin"
    tools:context="com.example.kaushal.sms_parent.MainActivity">

    <EditText
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:id="@+id/editText"
        android:height="50dp"
        android:width="200dp"
        android:hint="Enter Name"
        android:layout_alignParentTop="true"
        android:layout_centerHorizontal="true" />

    <EditText
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:id="@+id/editText2"
        android:height="50dp"
        android:width="200dp"
        android:layout_below="@+id/editText"
        android:layout_centerHorizontal="true"
        android:layout_marginTop="46dp"
        android:hint="Enter Age" />

    <EditText
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:id="@+id/editText3"
        android:layout_centerVertical="true"
        android:layout_alignEnd="@+id/editText2"
        android:width="200dp"
        android:height="50dp"
        android:hint="Enter Parent Number"
        android:visibility="gone" />

    <Button
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Enter"
        android:id="@+id/button"
        android:onClick="transferdata"
        android:layout_alignParentBottom="true"
        android:layout_centerHorizontal="true"
        android:layout_marginBottom="96dp" />
</RelativeLayout>

Manifest File 
 

Java File
 

Java Code:
package com.example.kaushal.sms_parent;

import android.Manifest;
import android.os.Bundle;
import android.support.v4.app.ActivityCompat;
import android.support.v7.app.AppCompatActivity;
import android.widget.Button;
import android.widget.EditText;
import android.view.View;
import android.content.Intent;

public class MainActivity extends AppCompatActivity {
    EditText et1,et2,et3;
    Button bt1;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        ActivityCompat.requestPermissions(this, new String[]{Manifest.permission.SEND_SMS}, 1);
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        et1 = (EditText) findViewById(R.id.editText2);
        et3 = (EditText) findViewById(R.id.editText);
        et2 = (EditText) findViewById(R.id.editText3);
        bt1 = (Button) findViewById(R.id.button);
        et1.setOnFocusChangeListener(new View.OnFocusChangeListener() {
            @Override
            public void onFocusChange(View v, boolean hasFocus) {
                if (!hasFocus) {
                    // Always use a TextKeyListener when clearing a TextView to prevent android
                    // warnings in the log
                    checkage();
                }
            }
        });
    }
    public void checkage()
    {
        variables.age=Integer.parseInt(et1.getText().toString());
        if(variables.age<=16)
        {
            et2.setVisibility(View.VISIBLE);
        }
    }
    public void transferdata(View v)
    {
        variables.name=et3.getText().toString();
        variables.age=Integer.parseInt(et1.getText().toString());
        variables.parentno=et2.getText().toString();

        startActivity(new Intent(this,Main2Activity.class));
    }
}

Second Activity Page
 

Main Activity file (xml)
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:paddingBottom="@dimen/activity_vertical_margin"
    android:paddingLeft="@dimen/activity_horizontal_margin"
    android:paddingRight="@dimen/activity_horizontal_margin"
    android:paddingTop="@dimen/activity_vertical_margin"
    app:layout_behavior="@string/appbar_scrolling_view_behavior"
    tools:context="com.example.kaushal.sms_parent.Main2Activity"
    tools:showIn="@layout/activity_main2">

    <EditText
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:id="@+id/editText4"
        android:layout_alignParentTop="true"
        android:layout_centerHorizontal="true"
        android:layout_marginTop="53dp"
        android:hint="Enter Number"
        android:height="50dp"
        android:width="200dp" />

    <EditText
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:inputType="textMultiLine"
        android:ems="10"
        android:id="@+id/editText5"
        android:layout_below="@+id/editText4"
        android:layout_alignParentStart="true"
        android:layout_marginTop="45dp"
        android:layout_alignParentEnd="true"
        android:height="200dp"
        android:hint="Enter Message" />

    <Button
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Send"
        android:id="@+id/button2"
        android:layout_marginTop="47dp"
        android:layout_below="@+id/editText5"
        android:layout_centerHorizontal="true"
        android:onClick="sendMessage" />
</RelativeLayout>

Java File
 

Java Code:
package com.example.kaushal.sms_parent;

import android.os.Bundle;
import android.support.v7.app.AppCompatActivity;
import android.telephony.SmsManager;
import android.view.View;
import android.widget.Button;
import android.widget.EditText;
import android.widget.Toast;

public class Main2Activity extends AppCompatActivity {
    EditText et5,et6;
    Button bt3;

    @Override
    protected void onCreate(Bundle savedInstanceState) {


        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main2);

        et5 = (EditText) findViewById(R.id.editText4);
        et6 = (EditText) findViewById(R.id.editText5);
        bt3 = (Button) findViewById(R.id.button2);
    }
    public void sendMessage(View v)
    {
        //ActivityCompat.requestPermissions(this, new String[]{Manifest.permission.SEND_SMS}, 1);
        variables.phone=et5.getText().toString();
        variables.message=et6.getText().toString();
        if(variables.count>10)
        {
            SmsManager smsManager = SmsManager.getDefault();
            smsManager.sendTextMessage(variables.parentno, null, variables.message, null, null);
            variables.count=0;
            Toast.makeText(getApplicationContext(), "Limit exceeded.... Sms is sending to ur parent!", Toast.LENGTH_LONG).show();
            et5.setText("");
            et6.setText("");
        }
        else
        {
            SmsManager smsManager = SmsManager.getDefault();
            smsManager.sendTextMessage(variables.phone, null, variables.message, null, null);
            Toast.makeText(getApplicationContext(), "SMS Sent!", Toast.LENGTH_LONG).show();
            variables.count++;
            et5.setText("");
            et6.setText("");

        }
    }

}

Test Code File:
 
Test Code:
package com.example.kaushal.sms_parent;

import android.test.ActivityInstrumentationTestCase2;
import android.widget.EditText;
import android.widget.TextView;

import com.robotium.solo.Solo;


public class ApplicationTest extends ActivityInstrumentationTestCase2 {
    private Solo solo;
    public ApplicationTest() {
        super(Main2Activity.class);
    }
    public void setUp() throws Exception {
        solo = new Solo(getInstrumentation(), getActivity());
    }

    public void testCase() throws Exception {
        String vResult="Message Send";
        EditText vEditText4 = (EditText) solo.getView(R.id.editText4);
        EditText vEditText5 = (EditText) solo.getView(R.id.editText5);
        solo.clearEditText(vEditText4);
        solo.clearEditText(vEditText5);
        solo.enterText(vEditText4,"9876543215");
        solo.enterText(vEditText5,"hello");
        solo.clickOnButton("Send");
        assertTrue(solo.searchText(vResult));
        TextView textField = (TextView) solo.getView(R.id.textView);
        assertEquals(vResult, textField.getText().toString());
    }

    @Override
    public void tearDown() throws Exception {
        solo.finishOpenedActivities();
    }
}

Output
If the Tests are successful
 
If the tests are unsuccessful
 

Conclusion 
After completing this practical we are able to check any application whether it is working or not.




Practical 2
Objective: A developer develops the simple “Calculator” application - plain java application. The application has all the basic functionalities of calculator. As a JUnit Tester; write a java code to test the “Calculator” application
Prerequisites: Candidate should familiar with how to use controls and basic operations in android application environment.

Steps/Process
 

Main Activity file (xml)
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/activity_main"
    android:layout_width="fill_parent"
    android:layout_height="fill_parent"
    android:orientation="vertical"
    android:paddingLeft="@dimen/activity_horizontal_margin"
    android:paddingRight="@dimen/activity_horizontal_margin"
    android:paddingTop="@dimen/activity_vertical_margin"
    android:paddingBottom="@dimen/activity_vertical_margin"
    tools:context="com.example.kaushal.calculator.MainActivity">
    <EditText
        android:layout_weight="1"
        android:layout_height="wrap_content"
        android:layout_marginRight="5pt"
        android:id="@+id/etNum1"
        android:layout_width="match_parent"
        android:inputType="numberDecimal">
    </EditText>
    <EditText
        android:layout_height="wrap_content"
        android:layout_weight="1"
        android:layout_marginLeft="5pt"
        android:id="@+id/etNum2"
        android:layout_width="match_parent"
        android:inputType="numberDecimal">
    </EditText>

<Button
    android:layout_height="wrap_content"
    android:layout_width="match_parent"
    android:layout_weight="1"
    android:text="+"
    android:textSize="8pt"
    android:id="@+id/btnAdd">
</Button>
<Button
    android:layout_height="wrap_content"
    android:layout_width="match_parent"
    android:layout_weight="1"
    android:text="-"
    android:textSize="8pt"
    android:id="@+id/btnSub">
</Button>
<Button
    android:layout_height="wrap_content"
    android:layout_width="match_parent"
    android:layout_weight="1"
    android:text="*"
    android:textSize="8pt"
    android:id="@+id/btnMult">
</Button>
<Button
    android:layout_height="wrap_content"
    android:layout_width="match_parent"
    android:layout_weight="1"
    android:text="/"
    android:textSize="8pt"
    android:id="@+id/btnDiv">
</Button>
<TextView
android:layout_height="wrap_content"
android:layout_width="match_parent"
android:layout_marginLeft="5pt"
android:layout_marginRight="5pt"
android:textSize="12pt"
android:layout_marginTop="3pt"
android:id="@+id/tvResult"
android:gravity="center_horizontal">
</TextView>

</LinearLayout>


Manifest File 
 

Java File
 

Java Code:
package com.example.kaushal.calculator;

import android.support.v7.app.AppCompatActivity;
import android.os.Bundle;
import android.text.TextUtils;
import android.view.Menu;
import android.view.MenuItem;
import android.view.View;
import android.widget.EditText;
import android.widget.Button;
import android.widget.TextView;

public class MainActivity extends AppCompatActivity{
    EditText etNum1;
    EditText etNum2;

    Button btnAdd;
    Button btnSub;
    Button btnMult;
    Button btnDiv;

    int num1=0,num2=0,num3=0;

    TextView tvResult;

    String oper = "";
    final int MENU_RESET_ID = 1;
    final int MENU_QUIT_ID = 2;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        etNum1 = (EditText) findViewById(R.id.etNum1);
        etNum2 = (EditText) findViewById(R.id.etNum2);

        btnAdd = (Button) findViewById(R.id.btnAdd);
        btnSub = (Button) findViewById(R.id.btnSub);
        btnMult = (Button) findViewById(R.id.btnMult);
        btnDiv = (Button) findViewById(R.id.btnDiv);

        tvResult = (TextView) findViewById(R.id.tvResult);

        num1 = Integer.parseInt(etNum1.getText().toString());
        num2 = Integer.parseInt(etNum2.getText().toString());

    }
    public static int addap(int a,int b)
    {
        return a+b;
    }
    public static int subap(int a,int b)
    {
        return a-b;
    }
    public static int multiap(int a,int b)
    {
        return a*b;
    }
    public static int divap(int a,int b)
    {
        return a/b;
    }
    public void add(View v)
    {
        num3 = addap(num1,num2);
        tvResult.setText(num1 + " " + oper + " " + num2 + " = " + num3);

    }
    public void sub(View v)
    {
        num3 = subap(num1, num2);
        tvResult.setText(num1 + " " + oper + " " + num2 + " = " + num3);
    }
    public void multi(View v)
    {
        num3 = multiap(num1,num2);
        tvResult.setText(num1 + " " + oper + " " + num2 + " = " + num3);
    }
    public void div(View v)
    {
        num3 = divap(num1, num2);
        tvResult.setText(num1 + " " + oper + " " + num2 + " = " + num3);
    }
    public void cleartext(View v)
    {
        etNum1.setText(0);
        etNum2.setText(0);
        tvResult.setText(0);
    }
}

Test code File
 

Junit Test Code
package com.example.kaushal.calculator;

import org.junit.Test;

import static org.junit.Assert.*;

/**
 * Example local unit test, which will execute on the development machine (host).
 *
 * @see <a href="http://d.android.com/tools/testing">Testing documentation</a>
 */
public class ExampleUnitTest {
    @Test    public void addition_isCorrect() throws Exception
    {
        int result = MainActivity.addap(2, 3);
        assertEquals(5, result);
    }
    @Test    public void subtraction_isCorrect() throws Exception
    {
        int result = MainActivity.addap(5, 3);
        assertEquals(2, result);
    }
    @Test    public void multiplication_isCorrect() throws Exception
    {
        int result = MainActivity.addap(2,3);
        assertEquals(6, result);
    }
    @Test    public void division_isCorrect() throws Exception
    {
        int result = MainActivity.addap(5,3);
        assertEquals(1, result);
    }

}

Output
 
If the Tests are successful
 
If the Tests are unsuccessful
 

Conclusion 
After completing this practical we are able to check any application whether it is working or not.





Practical 3
Objective: Write a java code to test “Activity” using Android Testing Framework.
Given: “Login App”
Prerequisites: Candidate should familiar with how to use controls and basic operations in android application environment.

Steps/Process
 

Main Activity file (xml)
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/activity_main"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:paddingBottom="@dimen/activity_vertical_margin"
    android:paddingLeft="@dimen/activity_horizontal_margin"
    android:paddingRight="@dimen/activity_horizontal_margin"
    android:paddingTop="@dimen/activity_vertical_margin"
    tools:context="com.example.kaushal.loginapp.MainActivity">

    <TextView
        android:text="@string/enter_your_id"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_alignParentTop="true"
        android:layout_alignParentStart="true"
        android:layout_marginStart="16dp"
        android:layout_marginTop="53dp"
        android:id="@+id/textView" />

    <TextView
        android:text="@string/enter_password"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_below="@+id/textView"
        android:layout_alignStart="@+id/textView"
        android:layout_marginTop="67dp"
        android:id="@+id/textView2" />

    <EditText
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:inputType="textPersonName"
        android:ems="10"
        android:id="@+id/editText"
        android:layout_alignBaseline="@+id/textView"
        android:layout_alignBottom="@+id/textView"
        android:layout_alignParentEnd="true"
        tools:ignore="LabelFor,RelativeOverlap" />

    <EditText
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:inputType="textPassword"
        android:ems="10"
        android:layout_below="@+id/editText"
        android:layout_alignStart="@+id/editText"
        android:layout_marginTop="40dp"
        android:id="@+id/editText2"
        tools:ignore="LabelFor" />

    <Button
        android:text="@string/login"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_below="@+id/editText2"
        android:layout_alignEnd="@+id/textView2"
        android:layout_marginTop="97dp"
        android:id="@+id/button"
        android:onClick="loginbutton" />

    <Button
        android:text="@string/cancel"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_alignBottom="@+id/button"
        android:layout_alignStart="@+id/editText2"
        android:layout_marginStart="45dp"
        android:id="@+id/button2"
        android:onClick="cancelbutton" />

</RelativeLayout>


Manifest File 
 

Java File
 

Java Code:
package com.example.kaushal.login_app_android_test;

import android.app.Activity;
import android.graphics.Color;
import android.support.v7.app.AppCompatActivity;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.EditText;
import android.widget.TextView;
import android.widget.Toast;


public class MainActivity extends AppCompatActivity {
    Button b1,b2;
    EditText ed1,ed2;
    TextView tv1;
    int counter = 3;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        b1 = (Button) findViewById(R.id.button);
        ed1 = (EditText) findViewById(R.id.editText);
        ed2 = (EditText) findViewById(R.id.editText2);
        tv1=(TextView) findViewById(R.id.textView3);
        b2 = (Button) findViewById(R.id.button2);
    }
    public static String checklogin(String user,String pass)
    {
        if (user.equals("admin") && pass.equals("admin")) {
            //Toast.makeText(getApplicationContext(), "Correct User", Toast.LENGTH_SHORT).show();
            String check="Correct User";
            return check;
        } else {
            //Toast.makeText(getApplicationContext(), "Wrong Credentials", Toast.LENGTH_SHORT).show();
            String check="InCorrect User";
            return check;
        }
    }
    public void loginbutton(View v)
    {
        String name = ed1.getText().toString();
        String pass = ed2.getText().toString();
        String checkuser=checklogin(name,pass);
        tv1.setText(checkuser);
    }
    public void cancelbutton(View v)
    {
        finish();
    }
}

Test File Code:
package com.example.kaushal.login_app_android_test;

import android.app.Application;
import android.test.ApplicationTestCase;


public class ApplicationTest extends ApplicationTestCase<Application> {
    public ApplicationTest() {
        super(Application.class);
    }
    public void login_correct() throws Exception
    {
        String result = MainActivity.checklogin("admin","admin");
        assertEquals("Correct User", result);
    }

}

dependencies
apply plugin: 'com.android.application'

android {
    compileSdkVersion 23
    buildToolsVersion "25.0.1"

    defaultConfig {
        applicationId "com.example.kaushal.login_app_android_test"
        minSdkVersion 19
        targetSdkVersion 23
        versionCode 1
        versionName "1.0"
    }
    buildTypes {
        release {
            minifyEnabled false
            proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.pro'
        }
    }
}

dependencies {
    compile fileTree(dir: 'libs', include: ['*.jar'])
    testCompile 'junit:junit:4.12'
    compile 'com.android.support:appcompat-v7:23.4.0'
}

Output
If the tests are successful
 

If the tests are unsuccessful
 


Conclusion 
After completing this practical we are able to check username and password and test the app.













Practical 4

Objective: Write a code to test “Activity” using Robotium Framework. 
Given: “Login App” 
Prerequisites: Candidate should familiar with how to use controls and basic operations in android application environment.

Steps/Process
 

Main Activity file (xml)
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/activity_main"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:paddingBottom="@dimen/activity_vertical_margin"
    android:paddingLeft="@dimen/activity_horizontal_margin"
    android:paddingRight="@dimen/activity_horizontal_margin"
    android:paddingTop="@dimen/activity_vertical_margin"
    tools:context="com.example.kaushal.loginapp.MainActivity">

    <TextView
        android:text="@string/enter_your_id"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_alignParentTop="true"
        android:layout_alignParentStart="true"
        android:layout_marginStart="16dp"
        android:layout_marginTop="53dp"
        android:id="@+id/textView" />

    <TextView
        android:text="@string/enter_password"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_below="@+id/textView"
        android:layout_alignStart="@+id/textView"
        android:layout_marginTop="67dp"
        android:id="@+id/textView2" />

    <EditText
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:inputType="textPersonName"
        android:ems="10"
        android:id="@+id/editText"
        android:layout_alignBaseline="@+id/textView"
        android:layout_alignBottom="@+id/textView"
        android:layout_alignParentEnd="true"
        tools:ignore="LabelFor,RelativeOverlap" />

    <EditText
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:inputType="textPassword"
        android:ems="10"
        android:layout_below="@+id/editText"
        android:layout_alignStart="@+id/editText"
        android:layout_marginTop="40dp"
        android:id="@+id/editText2"
        tools:ignore="LabelFor" />

    <Button
        android:text="@string/login"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:id="@+id/button"
        android:onClick="loginbutton"
        android:layout_marginLeft="24dp"
        android:layout_alignTop="@+id/button2"
        android:layout_toStartOf="@+id/editText2" />

    <Button
        android:text="@string/cancel"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginStart="46dp"
        android:id="@+id/button2"
        android:onClick="cancelbutton"
        android:layout_alignParentBottom="true"
        android:layout_alignStart="@+id/editText2"
        android:layout_marginBottom="102dp" />

    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:id="@+id/textView3"
        android:layout_centerVertical="true"
        android:layout_alignStart="@+id/button"
        android:width="200dp"
        android:height="50dp" />

</RelativeLayout>

Manifest File 
 

Java File
 

Java Code:
package com.example.kaushal.loginapp;



import android.app.Activity;

import android.graphics.Color;

import android.support.v7.app.AppCompatActivity;

import android.os.Bundle;

import android.view.View;

import android.widget.Button;

import android.widget.EditText;

import android.widget.TextView;

import android.widget.Toast;



public class MainActivity extends Activity {



    Button b1,b2;

    EditText ed1,ed2;

    TextView tv1;

    TextView tx1;

    int counter = 3;

    @Override

    protected void onCreate(Bundle savedInstanceState) {

        super.onCreate(savedInstanceState);

        setContentView(R.layout.activity_main);



        b1 = (Button) findViewById(R.id.button);

        ed1 = (EditText) findViewById(R.id.editText);

        ed2 = (EditText) findViewById(R.id.editText2);

        tv1=(TextView) findViewById(R.id.textView);

        b2 = (Button) findViewById(R.id.button2);



        }

    public void loginbutton(View v)

    {

        String name = ed1.getText().toString();

        String uname = String.format("%s", name);

        String pass = ed2.getText().toString();

        String upass = String.format("%s", pass);



        if (uname.equals("admin") && upass.equals("admin")) {

            Toast.makeText(getApplicationContext(),

                    "Correct User", Toast.LENGTH_SHORT).show();

            tv1.setText("Correct User");

        } else {

            Toast.makeText(getApplicationContext(), "Wrong Credentials", Toast.LENGTH_SHORT).show();

            tv1.setText("InCorrect User");

        }

    }

    public void cancelbutton(View v)

    {

        finish();

    }

}

Install Android images and tools.
Click on SDK Manager – and install
•	Intel x86 Atom System Image
•	Intel x64 Atom System Image
For all operating systems.
 

Test File Code
1.	In the java folder, in androidTest Package, create another androidTest java class and add this code.
2.	Add the file here as this picture shows.
 

package com.example.kaushal.loginapp;



import com.robotium.solo.Solo;

import android.test.ActivityInstrumentationTestCase2;

import android.widget.EditText;

import android.widget.TextView;





public class ActivityTest extends ActivityInstrumentationTestCase2<MainActivity> {

    private Solo solo;

    public ActivityTest () {

        super(MainActivity.class);

    }



    public void setUp() throws Exception {

        solo = new Solo(getInstrumentation(), getActivity());

    }



    public void testCase() throws Exception {

        String vResult="Correct User";

        EditText vEditText = (EditText) solo.getView(R.id.editText);

        EditText vEditText2 = (EditText) solo.getView(R.id.editText2);

        solo.clearEditText(vEditText);

        solo.clearEditText(vEditText2);

        solo.enterText(vEditText, "admin");

        solo.enterText(vEditText2,"admin");

        solo.clickOnButton("Login");

        assertTrue(solo.searchText(vResult));

        TextView textField = (TextView) solo.getView(R.id.textView);

        //Assert to verify result with visible value

        assertEquals(vResult, textField.getText().toString());

    }



    @Override

    public void tearDown() throws Exception {

        solo.finishOpenedActivities();

    }

}

Download and add Robotium.jar file
Dependencies
apply plugin: 'com.android.application'



android {

    compileSdkVersion 23

    buildToolsVersion "25.0.1"

    defaultConfig {

        applicationId "com.example.kaushal.loginapp"

        minSdkVersion 19

        targetSdkVersion 23

        versionCode 1

        versionName "1.0"

        testInstrumentationRunner "android.support.test.runner.AndroidJUnitRunner"

    }

    buildTypes {

        release {

            minifyEnabled false

            proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.pro'

        }

    }

}



dependencies {



    androidTestCompile 'com.jayway.android.robotium:robotium-solo:5.6.3'

    compile fileTree(dir: 'libs', include: ['*.jar'])

    androidTestCompile('com.android.support.test.espresso:espresso-core:2.2.2', {

        exclude group: 'com.android.support', module: 'support-annotations'

    })

    compile 'com.android.support:appcompat-v7:23.4.0'

    testCompile 'junit:junit:4.12'



}

Output
If the tests are successful
 

If the tests are unsuccessful 
 
Conclusion 
After completing this practical we are able to check any application whether it is working or not.




Practical 5
Objective: Write a code to test “Service” using Android Testing Framework.
Given: “Service App”
Prerequisites: Candidate should familiar with how to use controls and basic operations in android application environment.

Steps/Process
 

Main Activity file (xml)
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/activity_main"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:paddingBottom="@dimen/activity_vertical_margin"
    android:paddingLeft="@dimen/activity_horizontal_margin"
    android:paddingRight="@dimen/activity_horizontal_margin"
    android:paddingTop="@dimen/activity_vertical_margin"
    tools:context="com.example.kaushal.create_service.MainActivity">

    <Button
        android:text="@string/start_service"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_alignParentTop="true"
        android:layout_alignParentStart="true"
        android:layout_marginStart="64dp"
        android:layout_marginTop="37dp"
        android:id="@+id/button"
        android:onClick="startService" />

    <Button
        android:text="@string/stop_service"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="73dp"
        android:id="@+id/button3"
        android:layout_below="@+id/button"
        android:layout_alignStart="@+id/button"
        android:onClick="stopService" />

    <Button
        android:text="@string/next_page"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="100dp"
        android:id="@+id/button4"
        android:onClick="nextpage"
        android:layout_below="@+id/button3"
        android:layout_alignStart="@+id/button3" />
</RelativeLayout>


Manifest File 
 

Java File
 

Java Code:
package com.example.kaushal.create_service;

import android.support.v7.app.AppCompatActivity;
import android.os.Bundle;
import android.view.View;
import android.content.Intent;
import android.app.Activity;
import android.util.Log;
import android.view.View;

public class MainActivity extends Activity {
    String msg = "Android : ";
    @Override
    public void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        Log.d(msg, "The onCreate() event");
    }

    public void startService(View view) {
        startService(new Intent(getBaseContext(), MyService.class));
    }

    // Method to stop the service
    public void stopService(View view) {
        stopService(new Intent(getBaseContext(), MyService.class));
    }
    public void nextpage(View v)
    {
        Intent intent=new Intent(this,NextPage.class);
        startActivity(intent);
    }
}
Service Class:
package com.example.kaushal.exp_5_service;

import android.app.Service;
import android.content.Intent;
import android.os.IBinder;
import android.widget.Toast;

public class MyService extends Service {
    public MyService() {
    }

    @Override
    public IBinder onBind(Intent intent) {
        // TODO: Return the communication channel to the service.
        throw new UnsupportedOperationException("Not yet implemented");
    }
    @Override
    public int onStartCommand(Intent intent, int flags, int startId) {
        // Let it continue running until it is stopped.
        Toast.makeText(this, "Service Started", Toast.LENGTH_LONG).show();
        return START_STICKY;
    }

    @Override
    public void onDestroy() {
        super.onDestroy();
        Toast.makeText(this, "Service Destroyed", Toast.LENGTH_LONG).show();
    }
}

NextPage
 

Test File Code

package com.example.kaushal.exp_5_service;

import android.test.ActivityInstrumentationTestCase2;
import android.widget.TextView;
import com.robotium.solo.Solo;

public class ServiceTest extends ActivityInstrumentationTestCase2<MainActivity> {
    private Solo solo;
    public ServiceTest() {
        super(MainActivity.class);
    }
    public void setUp() throws Exception {
        solo = new Solo(getInstrumentation(), getActivity());
    }

    public void testCase() throws Exception {
        String vResult="Service Started";
        String vResult1="Service Destroyed";
        String vResult2="Transfer to another page";
        solo.clickOnButton("Start Service");
        assertTrue(solo.searchText(vResult));
        TextView textField = (TextView) solo.getView(R.id.textView);
        //Assert to verify result with visible value
        assertEquals(vResult, textField.getText().toString());
    }

    @Override
    public void tearDown() throws Exception {
        solo.finishOpenedActivities();
    }
}

Download and add Robotium.jar file
Dependencies
apply plugin: 'com.android.application'

android {
    compileSdkVersion 23
    buildToolsVersion "25.0.1"

    defaultConfig {
        applicationId "com.example.kaushal.exp_5_service"
        minSdkVersion 19
        targetSdkVersion 23
        versionCode 1
        versionName "1.0"
    }
    buildTypes {
        release {
            minifyEnabled false
            proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.pro'
        }
    }
}

dependencies {

    androidTestCompile 'com.jayway.android.robotium:robotium-solo:5.6.3'
    compile fileTree(dir: 'libs', include: ['*.jar'])
    testCompile 'junit:junit:4.12'
    compile 'com.android.support:appcompat-v7:23.4.0'
    compile 'com.android.support:design:23.4.0'
}

Output
If the tests are successful
 
If the tests are unsuccessful
 

Conclusion 
After completing this practical we are able to create a service and check whether it is working or not.

