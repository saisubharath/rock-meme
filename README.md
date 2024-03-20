1.	Implementing Activities using Intents. activity_main.xml:
<?xmlversion="1.0"encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android" xmlns:app="http://schemas.android.com/apk/res-auto" xmlns:tools="http://schemas.android.com/tools" android:layout_width="match_parent" android:layout_height="match_parent" tools:context=".MainActivity">
<EditText android:id="@+id/name"
android:layout_width="wrap_content" android:layout_height="wrap_content" android:ems="10" android:hint="Name" android:inputType="textPersonName" android:minHeight="48dp"
app:layout_constraintBottom_toBottomOf="parent" app:layout_constraintEnd_toEndOf="parent" app:layout_constraintHorizontal_bias="0.497" app:layout_constraintStart_toStartOf="parent" app:layout_constraintTop_toTopOf="parent" app:layout_constraintVertical_bias="0.179" android:importantForAutofill="no"tools:ignore="HardcodedText" />
<Button
android:id="@+id/login" android:layout_width="wrap_content" android:layout_height="wrap_content" android:text="LOGIN" app:layout_constraintBottom_toBottomOf="parent" app:layout_constraintEnd_toEndOf="parent" app:layout_constraintHorizontal_bias="0.498" app:layout_constraintStart_toStartOf="parent" app:layout_constraintTop_toBottomOf="@+id/name" app:layout_constraintVertical_bias="0.413"
 
tools:ignore="HardcodedText"/>
<EditText android:id="@+id/pwd"
android:layout_width="wrap_content" android:layout_height="wrap_content" android:ems="10" android:hint="Password" android:inputType="textPassword"
app:layout_constraintBottom_toBottomOf="parent" app:layout_constraintEnd_toEndOf="parent" app:layout_constraintHorizontal_bias="0.497" app:layout_constraintStart_toStartOf="parent" app:layout_constraintTop_toTopOf="parent"
app:layout_constraintVertical_bias="0.37" tools:ignore="Autofill,HardcodedText,TouchTargetSizeCheck" />
</androidx.constraintlayout.widget.ConstraintLayout>

activity_sndpg.xml:
<?xmlversion="1.0"encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android" xmlns:app="http://schemas.android.com/apk/res-auto" xmlns:tools="http://schemas.android.com/tools" android:layout_width="match_parent" android:layout_height="match_parent" tools:context=".secondpg">
<TextView android:id="@+id/result"
android:layout_width="wrap_content" android:layout_height="wrap_content" android:text="@string/textview1" android:textSize="30sp" app:layout_constraintBottom_toBottomOf="parent" app:layout_constraintEnd_toEndOf="parent" app:layout_constraintHorizontal_bias="0.494" app:layout_constraintStart_toStartOf="parent" app:layout_constraintTop_toTopOf="parent" app:layout_constraintVertical_bias="0.224" android:textColor="@color/black"/>
<TextViewandroid:id="@+id/textView2" android:layout_width="wrap_content" android:layout_height="wrap_content" android:text="Welcome!"
 
app:layout_constraintBottom_toBottomOf="parent" app:layout_constraintEnd_toEndOf="parent" app:layout_constraintHorizontal_bias="0.498" app:layout_constraintStart_toStartOf="parent" app:layout_constraintTop_toTopOf="parent" app:layout_constraintVertical_bias="0.141" android:textSize="30sp" android:textColor="@color/black"tools:ignore="HardcodedText" />
</androidx.constraintlayout.widget.ConstraintLayout>

MainActivity.java:
package com.example.login; import android.content.Intent; import android.os.Bundle; import android.widget.Button; import android.widget.EditText;
import androidx.appcompat.app.AppCompatActivity; publicclassMainActivityextendsAppCompatActivity{
public static final String EXTRA_TEXT = "com.example.application.example.EXTRA_TEXT";
Buttonbut; @Override
protectedvoidonCreate(BundlesavedInstanceState){ super.onCreate(savedInstanceState); setContentView(R.layout.activity_main);
but = findViewById(R.id.login); but.setOnClickListener(v->activity2());
}
publicvoidactivity2(){
EditText editTextName= findViewById(R.id.name); String text =editTextName.getText().toString(); Intent intent = new Intent(this, secondpg.class); intent.putExtra(EXTRA_TEXT,text); startActivity(intent);
}
}

Secondpage.java:
package com.example.login; import android.content.Intent; import android.os.Bundle;importandroid.widget.TextView;
importandroidx.appcompat.app.AppCompatActivity; public class secondpg extends AppCompatActivity {
@Override
protectedvoidonCreate(BundlesavedInstanceState){ super.onCreate(savedInstanceState); setContentView(R.layout.activity_secondpg);
 
Intentintent=getIntent();
Stringtext=intent.getStringExtra(com.example.login.MainActivity.EXTRA_TEXT); TextView res= findViewById(R.id.result);
res.setText(text);
}
}
 
Inputscreen:

 
Outputscreen:

 
2.	DevelopeanApplicationtosetanimageaswallpaperandonclickofabuttontheimageshouldstartto change randomly


Activity_main.xml
<?xmlversion="1.0"encoding="utf-8"?>
<RelativeLayoutxmlns:android="http://schemas.android.com/apk/res/android"xmlns:tools="http://schemas.android.com/tools" android:layout_width="match_parent"android:layout_height="match_parent"
tools:context=".MainActivity">
<ImageView android:id="@+id/imageView" android:layout_width="match_parent" android:layout_height="match_parent"android:scaleType="centerCrop" />
<Button
android:id="@+id/changeWallpaperButton" android:layout_width="wrap_content" android:layout_height="wrap_content" android:layout_centerHorizontal="true" android:layout_alignParentBottom="true" android:layout_marginBottom="16dp"android:text="Change Wallpaper" />
</RelativeLayout>

MainActivity.java:
package com.example.activity.wallpaperchange; import android.Manifest;
import android.annotation.SuppressLint; import android.app.WallpaperManager; importandroid.content.pm.PackageManager; import android.os.Build;
import android.os.Bundle; import android.view.View; importandroid.widget.Button;
import android.widget.ImageView; importandroidx.annotation.NonNull;
importandroidx.appcompat.app.AppCompatActivity; import androidx.core.app.ActivityCompat;
import androidx.core.content.ContextCompat; import com.example.activity.wallpaperchange.R; import java.io.IOException;
importjava.util.Random;
publicclassMainActivityextendsAppCompatActivity{
privatestaticfinalintREQUEST_CODE_PERMISSION=123; private ImageView imageView;
privateButtonchangeWallpaperButton; private int[] wallpaperImages = {
 
R.drawable.wallpaper1, R.drawable.wallpaper2, R.drawable.wallpaper3
//Addmorewallpaperimagesasneeded
};
@Override
protectedvoidonCreate(BundlesavedInstanceState){ super.onCreate(savedInstanceState); setContentView(R.layout.activity_main); imageView = findViewById(R.id.imageView);
changeWallpaperButton=findViewById(R.id.changeWallpaperButton);
//Setinitialwallpaper
setRandomWallpaper();
//Setclicklistenerforthebutton
changeWallpaperButton.setOnClickListener(new View.OnClickListener() { @Override
publicvoidonClick(Viewv){
//Changewallpaperonbuttonclick
setRandomWallpaper();
}
});
//Requestpermissionifnotgranted
requestPermission();
}
privatevoidrequestPermission() {
if(Build.VERSION.SDK_INT>=Build.VERSION_CODES.M&&
ContextCompat.checkSelfPermission(this,Manifest.permission.SET_WALLPAPER)
!=PackageManager.PERMISSION_GRANTED){ ActivityCompat.requestPermissions(
this,
newString[]{Manifest.permission.SET_WALLPAPER},
REQUEST_CODE_PERMISSION
);
}
}
@SuppressLint("MissingSuperCall") @Override
publicvoidonRequestPermissionsResult(intrequestCode,@NonNullString[]permissions,@NonNullint[] grantResults) {
if(requestCode==REQUEST_CODE_PERMISSION&&grantResults.length>0 && grantResults[0] == PackageManager.PERMISSION_GRANTED) {
//Permissiongranted
}
}
privatevoidsetRandomWallpaper(){
//Choosearandomwallpaperimage
intrandomIndex=newRandom().nextInt(wallpaperImages.length); int resourceId = wallpaperImages[randomIndex];
//Setthechosenimageaswallpaper
 
try{
WallpaperManager.getInstance(this).setResource(resourceId);
}catch(IOExceptione){ e.printStackTrace();
}
//SetthechosenimageintheImageView
imageView.setImageResource(resourceId);
}
}

Inputscreen:

 



 
 
 
 
Outputscreen:



 
 
 
 
 
3.	ImplementingUIcomponentusingvariousviewlayout

activity_main.xml
<?xmlversion="1.0"encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android" xmlns:tools="http://schemas.android.com/tools" android:layout_width="match_parent" android:layout_height="match_parent" android:orientation="vertical"
android:padding="16dp">
<ImageView android:id="@+id/profileImage" android:layout_width="150dp" android:layout_height="150dp" android:layout_gravity="center" android:layout_marginBottom="16dp"
android:src="@drawable/ic_launcher_foreground"tools:ignore="ContentDescription,ImageContrastCheck"/>
<EditText android:id="@+id/editTextName" android:layout_width="375dp" android:layout_height="63dp" android:layout_marginBottom="8dp" android:hint="@string/name" tools:ignore="TextFields"android:importantForAutofill="no"/>
<EditText android:id="@+id/editTextEmail" android:layout_width="379dp" android:layout_height="59dp" android:layout_marginBottom="16dp" android:hint="Email" android:inputType="textEmailAddress" android:importantForAutofill="no"tools:ignore="HardcodedText" />
<Button
android:id="@+id/buttonSave" android:layout_width="289dp" android:layout_height="wrap_content"android:text="@string/save_changes"/>
</LinearLayout>

MainActivity.java:
packagecom.example.myapplication; import android.os.Bundle;
import android.view.View; import android.widget.Button; import android.widget.EditText;
 
import android.widget.ImageView; import android.widget.Toast;
import android.appcompat.app.AppCompatActivity; publicclassMainActivityextendsAppCompatActivity{
@Override
protectedvoidonCreate(BundlesavedInstanceState){ super.onCreate(savedInstanceState); setContentView(R.layout.ttt);
ImageViewprofileImage=findViewById(R.id.profileImage); EditText editTextName = findViewById(R.id.editTextName); EditText editTextEmail = findViewById(R.id.editTextEmail); Button buttonSave = findViewById(R.id.buttonSave); buttonSave.setOnClickListener(new View.OnClickListener() {
@Override
publicvoidonClick(Viewview){
Stringname=editTextName.getText().toString(); Stringemail=editTextEmail.getText().toString();
//Savelogichere(youcanreplacethiswithyouractualimplementation)
//Displayatoastmessagefordemonstrationpurposes
String message = "Name: " + name + "\nEmail: " + email; Toast.makeText(MainActivity.this, message, Toast.LENGTH_SHORT).show();
}
});
}
}
 
Inputscreen:




Outputscreen:

 
4.	Developanandroidapplicationusingcontrolslikebutton,textview,edittextfordesigningacalculator having basic functionality like addition, subtraction, multiplication and division.

activity_main.xml:

<?xmlversion="1.0"encoding="utf-8"?>
<LinearLayoutxmlns:android="http://schemas.android.com/apk/res/android"xmlns:tools="http://schemas.android.com/tools" android:layout_width="match_parent" android:layout_height="match_parent"
android:orientation="vertical" android:padding="16dp" tools:context=".MainActivity">
<EditText android:id="@+id/editText"
android:layout_width="match_parent" android:layout_height="wrap_content" android:layout_marginBottom="16dp" android:hint="0" android:inputType="text" android:textSize="24sp"
tools:ignore="Autofill,DuplicateSpeakableTextCheck,HardcodedText,VisualLintTextFieldSize"/>
<GridLayout android:layout_width="match_parent" android:layout_height="wrap_content"
android:background="@color/design_default_color_primary" android:columnCount="4"
android:rowCount="5">
<!--Buttons-->
<Button
style="?android:attr/borderlessButtonStyle" android:onClick="onClearButtonClick" android:text="C"tools:ignore="HardcodedText" />
<Button
style="?android:attr/borderlessButtonStyle" android:onClick="onOperatorClick" android:text="+"tools:ignore="HardcodedText" />
<Button
style="?android:attr/borderlessButtonStyle" android:onClick="onOperatorClick" android:text="-"tools:ignore="HardcodedText" />
<Button
style="?android:attr/borderlessButtonStyle" android:onClick="onOperatorClick" android:text="*"tools:ignore="HardcodedText" />
 
<Button
style="?android:attr/borderlessButtonStyle" android:onClick="onNumberClick" android:text="1"tools:ignore="HardcodedText" />
<Button
style="?android:attr/borderlessButtonStyle" android:onClick="onNumberClick" android:text="2"tools:ignore="HardcodedText" />
<Button
style="?android:attr/borderlessButtonStyle" android:onClick="onNumberClick" android:text="3"tools:ignore="HardcodedText" />
<Button
style="?android:attr/borderlessButtonStyle" android:onClick="onOperatorClick" android:text="/"tools:ignore="HardcodedText" />
<Button
style="?android:attr/borderlessButtonStyle" android:onClick="onNumberClick" android:text="4"tools:ignore="HardcodedText" />
<Button
style="?android:attr/borderlessButtonStyle" android:onClick="onNumberClick" android:text="5"tools:ignore="HardcodedText" />
<Button
style="?android:attr/borderlessButtonStyle" android:onClick="onNumberClick" android:text="6"tools:ignore="HardcodedText" />
<Button
style="?android:attr/borderlessButtonStyle" android:onClick="onNumberClick" android:text="."tools:ignore="HardcodedText" />
<Button
style="?android:attr/borderlessButtonStyle" android:onClick="onNumberClick" android:text="7"tools:ignore="HardcodedText" />
<Button
style="?android:attr/borderlessButtonStyle" android:onClick="onNumberClick" android:text="8"
 
tools:ignore="HardcodedText"/>
<Button
style="?android:attr/borderlessButtonStyle" android:onClick="onNumberClick" android:text="9"tools:ignore="HardcodedText" />
<Button
style="?android:attr/borderlessButtonStyle" android:onClick="onEqualButtonClick" android:text="="
tools:ignore="DuplicateSpeakableTextCheck,HardcodedText"/>
<Button
style="?android:attr/borderlessButtonStyle" android:onClick="onNumberClick" android:text="0"tools:ignore="HardcodedText" />
<Button
style="?android:attr/borderlessButtonStyle" android:layout_columnSpan="2" android:onClick="onEqualButtonClick" android:text="="tools:ignore="HardcodedText" />
</GridLayout>
</LinearLayout>

MainActivity.java:
package com.example.activity.myapplicationcalc; import android.annotation.SuppressLint;
import android.os.Bundle; import android.view.View; import android.widget.Button; import android.widget.EditText;
import androidx.appcompat.app.AppCompatActivity; import org.mariuszgromada.math.mxparser.Expression; publicclassMainActivityextendsAppCompatActivity{
privateEditTexteditText; @Override
protectedvoidonCreate(BundlesavedInstanceState){ super.onCreate(savedInstanceState); setContentView(R.layout.activity_main);
editText=findViewById(R.id.editText);
}
publicvoidonNumberClick(Viewview){ Button button = (Button) view; editText.append(button.getText());
}
public void onOperatorClick(View view) { Button button = (Button) view; editText.append(""+button.getText()+"");
 
}
publicvoidonClearButtonClick(Viewview){ editText.setText("");
}
@SuppressLint("SetTextI18n")
public void onEqualButtonClick(View view) { Stringexpression=editText.getText().toString(); try {
Expressionexpr=newExpression(expression); double result = expr.calculate(); editText.setText(Double.toString(result));
} catch (Exception e) { editText.setText("Error");
}
}
}
 
Inputscreen:

 
Outputscreen:

 
5.	ExerciseusingcontrolslikeRadiogroup,ButtonandCheckbox.

Layout.xml
<?xmlversion="1.0"encoding="utf-8"?>
<LinearLayoutxmlns:android="http://schemas.android.com/apk/res/android"xmlns:tools="http://schemas.android.com/tools" android:orientation="vertical"
android:layout_width="match_parent" android:layout_height="match_parent">
<TextView android:layout_width="match_parent" android:layout_height="wrap_content"android:text="select your subject"android:textStyle="bold" android:textSize="30dp" tools:ignore="HardcodedText,SpUsage" />
<CheckBox android:layout_width="match_parent" android:layout_height="wrap_content" android:id="@+id/tam" android:text="Tamil" android:textSize="25dp" tools:ignore="HardcodedText,SpUsage">
</CheckBox>
<CheckBox android:layout_width="match_parent" android:layout_height="wrap_content" android:id="@+id/eng" android:text="English" android:textSize="25dp" tools:ignore="HardcodedText,SpUsage">
</CheckBox>
<CheckBox android:id="@+id/social"
android:layout_width="match_parent" android:layout_height="wrap_content" android:text="Social" android:textSize="25dp"
tools:ignore="HardcodedText,SpUsage,TextSizeCheck">
</CheckBox>
<CheckBox android:layout_width="match_parent" android:layout_height="wrap_content" android:id="@+id/sci" android:text="Science" android:textSize="25dp" tools:ignore="HardcodedText,SpUsage">
</CheckBox>
<TextView
 
android:id="@+id/gender" android:layout_width="match_parent" android:layout_height="wrap_content"android:text="Select your Gender"android:textSize="30dp" android:textStyle="bold" tools:ignore="HardcodedText,SpUsage" />
<RadioGroup android:id="@+id/rgGender" android:layout_width="match_parent" android:layout_height="wrap_content" android:orientation="horizontal">
<RadioButton android:id="@+id/male"
android:layout_width="match_parent" android:layout_height="wrap_content" android:layout_weight="1" android:text="Male" android:textSize="25dp"
tools:ignore="HardcodedText,SpUsage,TextSizeCheck"/>
<RadioButton android:layout_width="match_parent" android:layout_height="wrap_content" android:layout_weight="1" android:id="@+id/female" android:text="Female" android:textSize="25dp" tools:ignore="HardcodedText,SpUsage" />
</RadioGroup>
<Button
android:layout_width="100dp" android:layout_height="50dp" android:id="@+id/subBtn" android:text="Submit" android:gravity="center" android:layout_gravity="center" tools:ignore="HardcodedText" />
</LinearLayout>

MainActivity.java:
packagecom.example.exercise5;
importandroidx.appcompat.app.AppCompatActivity; import android.annotation.SuppressLint;
importandroid.os.Bundle; import android.util.Log;
importandroid.widget.CheckBox;
importandroid.widget.CompoundButton; import android.widget.RadioButton; import android.widget.RadioGroup;
 
importandroid.widget.Toast;
publicclassMainActivityextendsAppCompatActivity{ String TAG=MainActivity.class.getName();
privateCheckBoxtam,eng,social,sci; private RadioGroup gender;
@SuppressLint({"MissingSuperCall","MissingInflatedId"}) @Override
protectedvoidonCreate(BundlesavedInstanceState){ super.onCreate(savedInstanceState); setContentView(R.layout.layout);
tam=findViewById(R.id.tam); eng=findViewById(R.id.eng); social=findViewById(R.id.social); sci=findViewById(R.id.sci);
tam.setOnCheckedChangeListener(newCompoundButton.OnCheckedChangeListener(){ @Override
public void onCheckedChanged(CompoundButton compoundButton, boolean b) { Log.d(TAG,tam.getText().toString()+"status"+b); Toast.makeText(getApplicationContext(),tam.getText().toString()+""+b,Toast.LENGTH_LONG).show();
}
});
eng.setOnCheckedChangeListener(newCompoundButton.OnCheckedChangeListener(){ @Override
public void onCheckedChanged(CompoundButton compoundButton, boolean b) { Log.d(TAG,eng.getText().toString()+"status"+b); Toast.makeText(getApplicationContext(),eng.getText().toString()+""+b,Toast.LENGTH_LONG).show();
}
});
gender=findViewById(R.id.rgGender); gender.setOnCheckedChangeListener((radioGroup,i)->{
RadioButton radioButton=gender.findViewById(i); Stringselectedstr=radioButton.getText().toString();
Toast.makeText(MainActivity.this,"Yourselectionis"+selectedstr,Toast.LENGTH_LONG).show();});
}
}
 
Inputscreen:

 
Outputscreen:

 
6.	ExerciseusingProgressBarviewandspinnerView

activity_main.xml:
<?xmlversion="1.0"encoding="utf-8"?>
<RelativeLayoutxmlns:android="http://schemas.android.com/apk/res/android"xmlns:tools="http://schemas.android.com/tools" android:layout_width="match_parent"android:layout_height="match_parent"
android:paddingLeft="16dp" android:paddingTop="16dp" android:paddingRight="16dp" android:paddingBottom="16dp" tools:context=".MainActivity">

<ProgressBar android:id="@+id/progressBar"
style="?android:attr/progressBarStyleHorizontal" android:layout_width="match_parent" android:layout_height="wrap_content" android:layout_centerVertical="true" android:layout_marginTop="20dp"/>

<Spinner android:id="@+id/spinner"
android:layout_width="match_parent" android:layout_height="wrap_content" android:layout_below="@id/progressBar" android:layout_marginTop="20dp"/>
</RelativeLayout>

MainActivity.java:
packagecom.example.record6;

import android.os.Bundle; importandroid.view.View;
importandroid.widget.AdapterView; importandroid.widget.ArrayAdapter; import android.widget.ProgressBar; import android.widget.Spinner;

importandroidx.appcompat.app.AppCompatActivity; import com.example.record6.R;
publicclassMainActivityextendsAppCompatActivity{

privateProgressBarprogressBar; private Spinner spinner; @Override
 
protectedvoidonCreate(BundlesavedInstanceState){ super.onCreate(savedInstanceState); setContentView(R.layout.activity_main);

//Initializeviews
progressBar = findViewById(R.id.progressBar); spinner = findViewById(R.id.spinner);

//Setupspinnerwithsample data
String[]spinnerItems={"Level1","Level2","Level3","Level4","Level5"};
ArrayAdapter<String>adapter=newArrayAdapter<>(this,android.R.layout.simple_spinner_dropdown_item, spinnerItems);
spinner.setAdapter(adapter);

//Setalistenerforspinneritemselection
spinner.setOnItemSelectedListener(new AdapterView.OnItemSelectedListener() { @Override
publicvoidonItemSelected(AdapterView<?>parentView,ViewselectedItemView,intposition,longid){
//Updateprogressbarbasedontheselecteditem int progress = (position + 1) * 20; progressBar.setProgress(progress);
}

@Override
publicvoidonNothingSelected(AdapterView<?>parentView){
//Donothinghere
}
});
}
}
 
Inputscreen:

 
Outputscreen:

 
7.	ExerciseusingImageViewandTextView.

activity_main.xml:
<?xmlversion="1.0"encoding="utf-8"?>
<RelativeLayoutxmlns:android="http://schemas.android.com/apk/res/android"xmlns:tools="http://schemas.android.com/tools" android:layout_width="match_parent"android:layout_height="match_parent" android:background="@color/teal_200"
tools:context=".MainActivity">
<!--ImageViewtodisplayanimage-->
<ImageView android:id="@+id/myImageView" android:layout_width="200dp" android:layout_height="200dp" android:layout_alignParentTop="true" android:layout_centerHorizontal="true" android:layout_marginTop="50dp"android:src="@drawable/img1" />
<!--TextViewtodisplaytext-->
<TextView android:id="@+id/myTextView" android:layout_width="wrap_content" android:layout_height="wrap_content"
android:layout_below="@id/myImageView" android:layout_alignParentStart="true" android:layout_alignParentEnd="true" android:layout_alignParentBottom="true" android:layout_marginStart="20dp" android:layout_marginTop="103dp" android:layout_marginEnd="15dp" android:layout_marginBottom="342dp"android:text="WELCOMETOANDROIDSTUDIO!"
android:textColor="@color/black"android:textSize="25sp" />
</RelativeLayout>

MainActivity.java:
packagecom.example.textviewandimage;
importandroidx.appcompat.app.AppCompatActivity; import android.os.Bundle;
importcom.example.textviewandimage.R;
publicclassMainActivityextendsAppCompatActivity{ @Override
protectedvoidonCreate(BundlesavedInstanceState){ super.onCreate(savedInstanceState); setContentView(R.layout.activity_main);
}


 5. PARTY MANAGEMENT APPLICATION

<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
xmlns:tools="http://schemas.android.com/tools"
android:layout_width="match_parent"
android:layout_height="match_parent"
android:padding="16dp"
tools:context=".MainActivity">

<EditText
android:id="@+id/guest_name_input"
android:layout_width="match_parent"
android:layout_height="wrap_content"
android:hint="Enter guest name"
android:layout_alignParentTop="true"/>

<Button
android:id="@+id/add_guest_button"
android:layout_width="wrap_content"
android:layout_height="wrap_content"
android:text="Add Guest"
android:layout_below="@id/guest_name_input"/>

<Button
android:id="@+id/delete_guest_button"
android:layout_width="wrap_content"
android:layout_height="wrap_content"
android:text="Delete Last Guest"
android:layout_below="@id/add_guest_button"
android:layout_marginTop="16dp"/>

<Button
android:id="@+id/update_guest_button"
android:layout_width="wrap_content"
android:layout_height="wrap_content"
android:text="Update Guest"
android:layout_below="@id/delete_guest_button"
android:layout_marginTop="16dp"/>

<TextView
android:id="@+id/guest_list_text_view"
android:layout_width="match_parent"
android:layout_height="wrap_content"
android:layout_below="@id/update_guest_button"
android:layout_marginTop="16dp"
android:text="Guest List:"
android:textStyle="bold"/>

</RelativeLayout>
package com.example.studentapplication;

import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.EditText;
import android.widget.TextView;
import androidx.appcompat.app.AppCompatActivity;
import java.util.ArrayList;
import java.util.List;

public class MainActivity extends AppCompatActivity {

EditText guestNameInput;
Button addGuestButton;
TextView guestListTextView;
Button deleteGuestButton;
Button updateGuestButton;

List<String> guestList;

@Override
protected void onCreate(Bundle savedInstanceState) {
super.onCreate(savedInstanceState);
setContentView(R.layout.activity_main);

guestNameInput = findViewById(R.id.guest_name_input);
addGuestButton = findViewById(R.id.add_guest_button);
guestListTextView = findViewById(R.id.guest_list_text_view);
deleteGuestButton = findViewById(R.id.delete_guest_button);
updateGuestButton = findViewById(R.id.update_guest_button);

guestList = new ArrayList<>();

addGuestButton.setOnClickListener(new View.OnClickListener() {
@Override
public void onClick(View v) {
String guestName = guestNameInput.getText().toString();
if (!guestName.isEmpty()) {
guestList.add(guestName);
updateGuestList();
guestNameInput.setText("");
}
}
});

deleteGuestButton.setOnClickListener(new View.OnClickListener() {
@Override
public void onClick(View v) {
if (!guestList.isEmpty()) {
guestList.remove(guestList.size() - 1);
updateGuestList();
}
}
});

updateGuestButton.setOnClickListener(new View.OnClickListener() {
@Override
public void onClick(View v) {
// Update functionality (not implemented in this example)
// You may implement it to update a guest's name
}
});
}

private void updateGuestList() {
StringBuilder guests = new StringBuilder();
for (String guest : guestList) {
guests.append(guest).append("\n");
}
guestListTextView.setText(guests.toString());
}
}

 

  

 

Calculator:

Java code
package com.example.myapplicationcalculator;

import android.os.Bundle;

import com.google.android.material.snackbar.Snackbar;

import androidx.appcompat.app.AppCompatActivity;

import android.view.View;

import androidx.navigation.NavController;
import androidx.navigation.Navigation;
import androidx.navigation.ui.AppBarConfiguration;
import androidx.navigation.ui.NavigationUI;

import com.example.myapplicationcalculator.databinding.ActivityMainBinding;

import android.view.Menu;
import android.view.MenuItem;
import android.widget.Button;
import android.widget.EditText;

import org.mariuszgromada.math.mxparser.Expression;

public class MainActivity extends AppCompatActivity {

   private EditText editText;

   @Override
   protected void onCreate(Bundle savedInstanceState) {
       super.onCreate(savedInstanceState);
       setContentView(R.layout.activity_main);
       editText = findViewById(R.id.editText);
   }

   public void onNumberClick(View view) {
       Button button = (Button) view;
       editText.append(button.getText());
   }

   public void onOperatorClick(View view) {
       Button button = (Button) view;
       editText.append(" " + button.getText() + " ");
   }

   public void onClearButtonClick(View view) {
       editText.setText("");
   }

   public void onEqualButtonClick(View view) {
       String expression = editText.getText().toString();
       try {
           Expression expr = new Expression(expression);
           double result = expr.calculate();
           editText.setText(Double.toString(result));
       } catch (Exception e) {
           editText.setText("Error");
       }
   }

}


 



 
Xml code:

<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
   xmlns:tools="http://schemas.android.com/tools"
   android:layout_width="match_parent"
   android:layout_height="match_parent"
   android:orientation="vertical"
   android:padding="16dp"
   tools:context=".MainActivity">

   <EditText
       android:id="@+id/editText"
       android:layout_width="match_parent"
       android:layout_height="wrap_content"
       android:layout_marginBottom="16dp"
       android:hint="0"
       android:background="@color/teal_200"
       android:inputType="text"
       android:textSize="24dp" />

   <GridLayout
       android:layout_width="match_parent"
       android:layout_height="wrap_content"
       android:background="#808080"
       android:columnCount="4"
       android:rowCount="5">

       <!-- Buttons -->
       <Button
           style="?android:attr/borderlessButtonStyle"
           android:onClick="onClearButtonClick"
           android:text="C" />

       <Button
           style="?android:attr/borderlessButtonStyle"
           android:onClick="onOperatorClick"
           android:text="/" />

       <Button
           style="?android:attr/borderlessButtonStyle"
           android:onClick="onNumberClick"
           android:text="7" />

       <Button
           style="?android:attr/borderlessButtonStyle"
           android:onClick="onNumberClick"
           android:text="8" />

       <Button
           style="?android:attr/borderlessButtonStyle"
           android:onClick="onEqualButtonClick"
           android:text="=" />

       <Button
           style="?android:attr/borderlessButtonStyle"
           android:onClick="onNumberClick"
           android:text="9" />

       <Button
           style="?android:attr/borderlessButtonStyle"
           android:onClick="onOperatorClick"
           android:text="*" />

       <Button
           style="?android:attr/borderlessButtonStyle"
           android:onClick="onNumberClick"
           android:text="4" />

       <Button
           style="?android:attr/borderlessButtonStyle"
           android:onClick="onNumberClick"
           android:text="5" />

       <Button
           style="?android:attr/borderlessButtonStyle"
           android:onClick="onNumberClick"
           android:text="6" />

       <Button
           style="?android:attr/borderlessButtonStyle"
           android:onClick="onOperatorClick"
           android:text="-" />

       <Button
           style="?android:attr/borderlessButtonStyle"
           android:onClick="onNumberClick"
           android:text="1" />

       <Button
           style="?android:attr/borderlessButtonStyle"
           android:onClick="onNumberClick"
           android:text="2" />

       <Button
           style="?android:attr/borderlessButtonStyle"
           android:onClick="onNumberClick"
           android:text="3" />

       <Button
           style="?android:attr/borderlessButtonStyle"
           android:onClick="onOperatorClick"
           android:text="+" />

       <Button
           style="?android:attr/borderlessButtonStyle"
           android:onClick="onNumberClick"
           android:text="0" />

       <Button
           style="?android:attr/borderlessButtonStyle"
           android:onClick="onNumberClick"
           android:text="." />

       <Button
           style="?android:attr/borderlessButtonStyle"
           android:layout_columnSpan="2"
           android:onClick="onEqualButtonClick"
           android:text="=" />

   </GridLayout>
</LinearLayout>


    





 


 


Gradle :
plugins {
   id 'com.android.application'
}

android {
   namespace 'com.example.myapplicationcalculator'
   compileSdk 34

   defaultConfig {
       applicationId "com.example.myapplicationcalculator"
       minSdk 27
       targetSdk 34
       versionCode 1
       versionName "1.0"

       testInstrumentationRunner "androidx.test.runner.AndroidJUnitRunner"
   }

   buildTypes {
       release {
           minifyEnabled false
           proguardFiles getDefaultProguardFile('proguard-android-optimize.txt'), 'proguard-rules.pro'
       }
   }
   compileOptions {
       sourceCompatibility JavaVersion.VERSION_1_8
       targetCompatibility JavaVersion.VERSION_1_8
   }
   buildFeatures {
       viewBinding true
   }
}

dependencies {

   implementation 'androidx.appcompat:appcompat:1.6.1'
   implementation 'com.google.android.material:material:1.11.0'
   implementation 'androidx.constraintlayout:constraintlayout:2.1.4'
   implementation 'androidx.navigation:navigation-fragment:2.7.6'
   implementation 'androidx.navigation:navigation-ui:2.7.6'
   testImplementation 'junit:junit:4.13.2'
   androidTestImplementation 'androidx.test.ext:junit:1.1.5'
   androidTestImplementation 'androidx.test.espresso:espresso-core:3.5.1'
   implementation 'org.mariuszgromada.math:MathParser.org-mXparser:4.4.2'
}

  

Output:
 
 

sqlitedatabaseactivity.java

package com.example.sqlitedatabaseactivity;

import static android.widget.Toast.makeText;

import android.annotation.SuppressLint;
import android.database.Cursor;
import android.os.Bundle;

import com.google.android.material.snackbar.Snackbar;

import androidx.appcompat.app.AppCompatActivity;

import android.text.Editable;
import android.view.View;

import androidx.navigation.NavController;
import androidx.navigation.Navigation;
import androidx.navigation.ui.AppBarConfiguration;
import androidx.navigation.ui.NavigationUI;

import com.example.sqlitedatabaseactivity.databinding.ActivityMainBinding;

import android.view.Menu;
import android.view.MenuItem;
import android.widget.Button;
import android.widget.EditText;
import android.widget.TextView;
import android.widget.Toast;

public class SQLiteDatabaseActivity extends AppCompatActivity {

   private DbAdapter dbAdapter;

   @Override
   protected void onCreate(Bundle savedInstanceState) {
       super.onCreate(savedInstanceState);
       setContentView(R.layout.activity_sqlite);

       dbAdapter = new DbAdapter(this);
       dbAdapter.open();

       EditText eTName=findViewById(R.id.edtTextName);
       EditText eTAge=findViewById(R.id.edtTextAge);
       Button btnInsert = findViewById(R.id.btnInsert);
       Button btnRetrieve = findViewById(R.id.btnRetrieve);
       Button btnUpdate = findViewById(R.id.btnUpdate);
       Button btnDelete = findViewById(R.id.btnDelete);
       Button btnRetrieveParticularRecord=findViewById(R.id.btnRetrieveRecord);
       EditText eTrowId=findViewById(R.id.edtTextRowId);
       TextView tvRecordResult=findViewById(R.id.tvRecordResult);

       btnInsert.setOnClickListener(new View.OnClickListener() {
           @Override
           public void onClick(View v) {
               String name=eTName.getText().toString();
               String ageString=eTAge.getText().toString();
               int age=Integer.valueOf(ageString);
               // Example: Insert a record
               long rowId = dbAdapter.insertRecord(name,age);
               if (rowId != -1) {
                   showToast("Record inserted with ID: " + rowId);
               } else {
                   showToast("Failed to insert record");
               }
           }
       });

       btnRetrieve.setOnClickListener(new View.OnClickListener() {
           @Override
           public void onClick(View v) {
               // Example: Retrieve all records
               Cursor cursor = dbAdapter.getAllRecords();
               if (cursor != null && cursor.getCount() > 0) {
                   // Handle retrieved records
                   showToast("Number of records: " + cursor.getCount());
               } else {
                   showToast("No records found");
               }
           }
       });

       btnUpdate.setOnClickListener(new View.OnClickListener() {
           @Override
           public void onClick(View v) {
               Editable editTextRowId=eTrowId.getText();

               String idString = editTextRowId.toString();

               // Example: Update a record
               if(!idString.isEmpty()) {
                   long id = Long.parseLong(idString);

                   boolean success = dbAdapter.updateRecord(id, "Updated Name", 30);
                   if (success) {
                       showToast("Record updated successfully");
                   } else {
                       showToast("Failed to update record");
                   }
               }else {
                   showToast("Id is Empty");
               }
           }
       });

       btnDelete.setOnClickListener(new View.OnClickListener() {
           @Override
           public void onClick(View v) {
               Editable editTextRowId=eTrowId.getText();

               String idString = editTextRowId.toString();

               // Example: Delete a record
               if(!idString.isEmpty()) {
                   long id = Long.parseLong(idString);

                   boolean success = dbAdapter.deleteRecord(id);
                   if (success) {
                       showToast("Record deleted successfully");
                   } else {
                       showToast("Failed to delete record");
                   }
               }else {
                   showToast("Id is Empty");
               }
           }
       });

       btnRetrieveParticularRecord.setOnClickListener(new View.OnClickListener() {
           @Override
           public void onClick(View v) {
               Editable editTextRowId=eTrowId.getText();

               String idString = editTextRowId.toString();
               if (!idString.isEmpty()) {
                   try {
                       // Parse the string to a long
                       long recordId = Long.parseLong(idString);

                       // Call getRecord to retrieve the record
                       Cursor cursor = dbAdapter.getRecord(recordId);

                       if (cursor != null && cursor.moveToFirst()) {
                           // Retrieve data from the cursor
                           @SuppressLint("Range") String name = cursor.getString(cursor.getColumnIndex(DbAdapter.KEY_NAME));
                           @SuppressLint("Range") int age = cursor.getInt(cursor.getColumnIndex(DbAdapter.KEY_AGE));

                           // Display the result in the TextView
                           String resultText = "Name: " + name + ", Age: " + age;
                           tvRecordResult.setText(resultText);
                       } else {
                           showToast("Record not found");
                       }
                   } catch (NumberFormatException e) {
                       showToast("Invalid ID format");
                   }
               } else {
                   showToast("Please enter a Record ID");
               }
           }
       });

   }

   private void showToast(String message) {
       Toast.makeText(this, message, Toast.LENGTH_SHORT).show();
   }

   @Override
   protected void onDestroy() {
       super.onDestroy();
       dbAdapter.close();
   }
}



    

Activity_sqlite.xml:

<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
   xmlns:tools="http://schemas.android.com/tools"
   android:layout_width="match_parent"
   android:layout_height="match_parent"
   android:orientation="vertical"
   android:padding="16dp"
   android:gravity="center"
   tools:context=".SQLiteDatabaseActivity">

   <TextView
       android:layout_width="match_parent"
       android:layout_height="wrap_content"
       android:text="Enter Name:"
       android:textSize="20dp"/>

   <EditText
       android:id="@+id/edtTextName"
       android:layout_width="match_parent"
       android:textSize="20dp"
       android:layout_height="wrap_content"/>

   <TextView
       android:layout_width="match_parent"
       android:layout_height="wrap_content"
       android:text="Enter Age:"
       android:textSize="20dp"/>

   <EditText
       android:id="@+id/edtTextAge"
       android:layout_width="match_parent"
       android:textSize="20dp"
       android:layout_height="wrap_content"/>

   <Button
       android:id="@+id/btnInsert"
       android:layout_width="match_parent"
       android:layout_height="wrap_content"
       android:text="Insert Record" />

   <Button
       android:id="@+id/btnRetrieve"
       android:layout_width="match_parent"
       android:layout_height="wrap_content"
       android:text="Total Records Count" />

   <TextView
       android:layout_width="match_parent"
       android:layout_height="wrap_content"
       android:text="Enter rowId:"
       android:textSize="20dp"/>

   <EditText
       android:id="@+id/edtTextRowId"
       android:layout_width="match_parent"
       android:textSize="20dp"
       android:layout_height="wrap_content"/>

   <Button
       android:id="@+id/btnUpdate"
       android:layout_width="match_parent"
       android:layout_height="wrap_content"
       android:text="Update Record" />

   <Button
       android:id="@+id/btnDelete"
       android:layout_width="match_parent"
       android:layout_height="wrap_content"
       android:text="Delete Record" />

   <Button
       android:id="@+id/btnRetrieveRecord"
       android:layout_width="match_parent"
       android:layout_height="wrap_content"
       android:text="Retrieve Particular Record" />

   <TextView
       android:id="@+id/tvRecordResult"
       android:layout_width="match_parent"
       android:layout_height="wrap_content"
       android:text="" />


</LinearLayout>
   

DbAdapter:
package com.example.sqlitedatabaseactivity;

import android.content.ContentValues;
import android.content.Context;
import android.database.Cursor;
import android.database.SQLException;
import android.database.sqlite.SQLiteDatabase;
import android.database.sqlite.SQLiteOpenHelper;

public class DbAdapter {
   // Database constants
   private static final String DATABASE_NAME = "your_database";
   private static final int DATABASE_VERSION = 1;

   // Table constants
   private static final String TABLE_NAME = "your_table";
   public static final String KEY_ID = "_id";
   public static final String KEY_NAME = "name";
   public static final String KEY_AGE = "age";

   // Database creation SQL statement
   private static final String DATABASE_CREATE =
           "create table " + TABLE_NAME + " ("
                   + KEY_ID + " integer primary key autoincrement, "
                   + KEY_NAME + " text not null, "
                   + KEY_AGE + " integer not null);";

   private final Context context;
   private DatabaseHelper DBHelper;
   private SQLiteDatabase db;

   public DbAdapter(Context ctx) {
       this.context = ctx;
       DBHelper = new DatabaseHelper(context);
   }

   // Helper class to manage database creation and version management.
   private static class DatabaseHelper extends SQLiteOpenHelper {
       DatabaseHelper(Context context) {
           super(context, DATABASE_NAME, null, DATABASE_VERSION);
       }

       @Override
       public void onCreate(SQLiteDatabase db) {
           try {
               db.execSQL(DATABASE_CREATE);
           } catch (SQLException e) {
               e.printStackTrace();
           }
       }

       @Override
       public void onUpgrade(SQLiteDatabase db, int oldVersion, int newVersion) {
           // Implement if you need to handle database upgrades
       }
   }

   // Open the database
   public DbAdapter open() throws SQLException {
       db = DBHelper.getWritableDatabase();
       return this;
   }

   // Close the database
   public void close() {
       DBHelper.close();
   }

   // Insert a record into the database
   public long insertRecord(String name, int age) {
       ContentValues initialValues = new ContentValues();
       initialValues.put(KEY_NAME, name);
       initialValues.put(KEY_AGE, age);
       return db.insert(TABLE_NAME, null, initialValues);
   }

   // Retrieve all records from the database
   public Cursor getAllRecords() {
       return db.query(TABLE_NAME, new String[]{KEY_ID, KEY_NAME, KEY_AGE},
               null, null, null, null, null);
   }

   // Retrieve a specific record based on ID
   public Cursor getRecord(long rowId) throws SQLException {
       Cursor cursor = db.query(true, TABLE_NAME,
               new String[]{KEY_ID, KEY_NAME, KEY_AGE},
               KEY_ID + "=" + rowId,
               null, null, null, null, null);
       if (cursor != null) {
           cursor.moveToFirst();
       }
       return cursor;
   }

   // Update a record in the database
   public boolean updateRecord(long rowId, String name, int age) {
       ContentValues args = new ContentValues();
       args.put(KEY_NAME, name);
       args.put(KEY_AGE, age);
       return db.update(TABLE_NAME, args, KEY_ID + "=" + rowId, null) > 0;
   }

   // Delete a record from the database
   public boolean deleteRecord(long rowId) {
       return db.delete(TABLE_NAME, KEY_ID + "=" + rowId, null) > 0;
   }
}

    
OUTPUT:
 
 
 


STOPWATCH:
StopwatchActivity.java
package com.example.stopwatch;

import android.os.Bundle;
import android.os.Handler;
import android.view.View;
import android.widget.TextView;

import androidx.appcompat.app.AppCompatActivity;

import org.jetbrains.annotations.Nullable;

import java.util.Locale;

public class StopwatchActivity extends AppCompatActivity {
   private int seconds = 0;

   // Is the stopwatch running?
   private boolean running;

   private boolean wasRunning;

   @Override
   protected void onCreate(@Nullable Bundle savedInstanceState) {
       super.onCreate(savedInstanceState);
       setContentView(R.layout.activity_stopwatch);
       if (savedInstanceState != null) {

           // Get the previous state of the stopwatch
           // if the activity has been
           // destroyed and recreated.
           seconds = savedInstanceState.getInt("seconds");
           running = savedInstanceState.getBoolean("running");
           wasRunning = savedInstanceState.getBoolean("wasRunning");

       }
       runTimer();

   }

   private void runTimer() {

       final TextView timeView = (TextView) findViewById(R.id.time_view);
       Handler handler = new Handler();
       handler.post(new Runnable() {
           @Override
           public void run() {
               int hours = seconds / 3600; //3600=1 hr
               int minutes = (seconds % 3600) / 60;
               int secs = seconds % 60;
               String time = String.format(Locale.getDefault(), "%d:%02d:%02d", hours,
                       minutes, secs);
               timeView.setText(time);
               if (running) {
                   seconds++;
               }

               // Post the code again
               // with a delay of 1 second.
               handler.postDelayed(this, 1000);
           }
       });
   }

   @Override
   public void onSaveInstanceState(Bundle savedInstanceState) {
       super.onSaveInstanceState(savedInstanceState);
       savedInstanceState.putInt("seconds", seconds);
       savedInstanceState.putBoolean("running", running);
       savedInstanceState.putBoolean("wasRunning", wasRunning);
   }

   @Override
   protected void onPause() {
       super.onPause();
       wasRunning = running;
       running = false;
   }

   // If the activity is resumed,
   // start the stopwatch
   // again if it was running previously.
   @Override
   protected void onResume() {
       super.onResume();
       if (wasRunning) {
           running = true;
       }
   }

   // Start the stopwatch running
   // when the Start button is clicked.
   // Below method gets called
   // when the Start button is clicked.
   public void onClickStart(View view) {
       running = true;
   }

   // Stop the stopwatch running
   // when the Stop button is clicked.
   // Below method gets called
   // when the Stop button is clicked.
   public void onClickStop(View view) {
       running = false;
   }

   // Reset the stopwatch when
   // the Reset button is clicked.
   // Below method gets called
   // when the Reset button is clicked.
   public void onClickReset(View view) {
       running = false;
       seconds = 0;
   }


}
    
Activity_stopwatch.xml:
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
   android:layout_width="match_parent"
   android:layout_height="match_parent"
   android:background="#0F9D58"
   android:layout_gravity="center"
   android:gravity="center"
   android:orientation="vertical"
   android:padding="16dp">

   <TextView
       android:id="@+id/time_view"
       android:layout_width="wrap_content"
       android:layout_height="wrap_content"
       android:layout_gravity="center_horizontal"
       android:textAppearance="@android:style/TextAppearance.Large"
       android:textSize="56sp" />

   <Button
       android:id="@+id/start_button"
       android:layout_width="wrap_content"
       android:layout_height="wrap_content"
       android:layout_gravity="center_horizontal"
       android:layout_marginTop="20dp"
       android:onClick="onClickStart"
       android:text="Start" />

   <Button
       android:id="@+id/stop_button"
       android:layout_width="wrap_content"
       android:layout_height="wrap_content"
       android:layout_gravity="center_horizontal"
       android:layout_marginTop="8dp"
       android:onClick="onClickStop"
       android:text="Stop" />

   <Button
       android:id="@+id/reset_button"
       android:layout_width="wrap_content"
       android:layout_height="wrap_content"
       android:layout_gravity="center_horizontal"
       android:layout_marginTop="8dp"
       android:onClick="onClickReset"
       android:text="Reset" />
</LinearLayout>
  
MultiTaskActivity.java:
package com.example.stopwatch;

import android.app.WallpaperManager;
import android.content.Intent;
import android.graphics.Bitmap;
import android.graphics.BitmapFactory;
import android.os.Bundle;
import android.telephony.SmsManager;
import android.view.View;
import android.widget.ImageView;
import android.widget.Toast;

import androidx.appcompat.app.AppCompatActivity;

import java.io.IOException;public class MultiTaskActivity extends AppCompatActivity {
   //bptnjgyjzc
   @Override
   protected void onCreate(Bundle savedInstanceState) {
       super.onCreate(savedInstanceState);
       setContentView(R.layout.activity_multi_task);
       ImageView imagePreview = findViewById(R.id.imagePreview);
       imagePreview.setImageResource(R.drawable.wallpaper);

       findViewById(R.id.apiCall).setOnClickListener(new View.OnClickListener() {
           @Override
           public void onClick(View view) {
             //  startActivity(new Intent(getApplicationContext(), APICall.class));
           }
       });

       findViewById(R.id.txtStopWatch).setOnClickListener(new View.OnClickListener() {
           @Override
           public void onClick(View view) {
               startActivity(new Intent(getApplicationContext(), StopwatchActivity.class));
           }
       });

       findViewById(R.id.txtSetWallpaper).setOnClickListener(new View.OnClickListener() {
           @Override
           public void onClick(View view) {
               WallpaperManager myWallpaperManager = WallpaperManager.getInstance(getApplicationContext());
               Bitmap bitmap = BitmapFactory.decodeResource(getResources(), R.drawable.wallpaper);
               try {
                   //myWallpaperManager.setResource(R.drawable.motorcycle);
                   myWallpaperManager.setBitmap(bitmap);
                   Toast.makeText(MultiTaskActivity.this, "Wallet set success", Toast.LENGTH_SHORT).show();
               } catch (IOException e) {
                   e.printStackTrace();
               }
           }
       });

       findViewById(R.id.txtSMSSend).setOnClickListener(new View.OnClickListener() {
           @Override


           public void onClick(View view) {

               String mobile = "9788686374";
               sendSMS(mobile, "Testing Message");
           }
       });

       findViewById(R.id.txtEmail).setOnClickListener(new View.OnClickListener() {
           @Override
           public void onClick(View view) {
               Intent email = new Intent(Intent.ACTION_SEND);
               email.putExtra(Intent.EXTRA_EMAIL, new String[]{"nsubbu9788@gmail.com"});
               email.putExtra(Intent.EXTRA_SUBJECT, "Subject");
               email.putExtra(Intent.EXTRA_TEXT, "message to send email");

               //need this to prompts email client only
               email.setType("message/rfc822");

               startActivity(Intent.createChooser(email, "Choose an Email client :"));
           }
       });
   }
 public void sendSMS(String phoneNo, String msg) {
       try {
           SmsManager smsManager = SmsManager.getDefault();
           smsManager.sendTextMessage(phoneNo, null, msg, null, null);
           Toast.makeText(getApplicationContext(), "Message Sent ", Toast.LENGTH_LONG).show();
       } catch (Exception ex) {
           Toast.makeText(getApplicationContext(), ex.getMessage().toString(),
                   Toast.LENGTH_LONG).show();
           ex.printStackTrace();
       }
   }
}
   

Activity_multi_task.xml:
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
   xmlns:app="http://schemas.android.com/apk/res-auto"
   xmlns:tools="http://schemas.android.com/tools"
   android:layout_width="match_parent"
   android:layout_height="match_parent"
   android:layout_gravity="center"
   android:gravity="center"
   android:orientation="vertical"
   tools:context=".MultiTaskActivity">

   <Button
       android:id="@+id/txtStopWatch"
       android:layout_width="wrap_content"
       android:layout_height="wrap_content"
       android:layout_marginTop="?actionBarSize"
       android:text="Stop Watch"
       app:layout_constraintEnd_toEndOf="parent"
       app:layout_constraintStart_toStartOf="parent"
       app:layout_constraintTop_toTopOf="parent" />

   <ImageView
       android:id="@+id/imagePreview"
       android:layout_width="100dp"
       android:layout_height="100dp"
       android:src="@drawable/wallpaper"
       app:layout_constraintEnd_toEndOf="parent"
       app:layout_constraintStart_toStartOf="parent"
       app:layout_constraintTop_toBottomOf="@id/txtStopWatch" />

   <Button
       android:id="@+id/txtSetWallpaper"
       android:layout_width="wrap_content"
       android:layout_height="wrap_content"
       android:text="Set Wallpaper"
       app:layout_constraintEnd_toEndOf="parent"
       app:layout_constraintStart_toStartOf="parent"
       app:layout_constraintTop_toBottomOf="@id/imagePreview" />

   <Button
       android:id="@+id/txtSMSSend"
       android:layout_width="wrap_content"
       android:layout_height="wrap_content"
       android:text="Send SMS"
       app:layout_constraintEnd_toEndOf="parent"
       app:layout_constraintStart_toStartOf="parent"
       app:layout_constraintTop_toBottomOf="@id/imagePreview" />


   <Button
       android:id="@+id/txtEmail"
       android:layout_width="wrap_content"
       android:layout_height="wrap_content"
       android:text="Send Email"
       app:layout_constraintEnd_toEndOf="parent"
       app:layout_constraintStart_toStartOf="parent"
       app:layout_constraintTop_toBottomOf="@id/imagePreview" />

   <Button
       android:id="@+id/apiCall"
       android:layout_width="wrap_content"
       android:layout_height="wrap_content"
       android:text="API Calling (Web Services)"
       app:layout_constraintEnd_toEndOf="parent"
       app:layout_constraintStart_toStartOf="parent"
       app:layout_constraintTop_toBottomOf="@id/imagePreview" />

</LinearLayout>
  


AndroidManifests.xml:
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
   xmlns:tools="http://schemas.android.com/tools">

   <uses-permission android:name="android.permission.SET_WALLPAPER" />
   <application
       android:allowBackup="true"
       android:dataExtractionRules="@xml/data_extraction_rules"
       android:fullBackupContent="@xml/backup_rules"
       android:icon="@mipmap/ic_launcher"
       android:label="@string/app_name"
       android:supportsRtl="true"
       android:theme="@style/Theme.Stopwatch"
       tools:targetApi="31">
       <activity
           android:name=".MultiTaskActivity"
           android:exported="true"
           android:label="@string/app_name"
           android:theme="@style/Theme.Stopwatch.NoActionBar">
           <intent-filter>
               <action android:name="android.intent.action.MAIN" />

               <category android:name="android.intent.category.LAUNCHER" />
           </intent-filter>
       </activity>
       <activity android:name=".StopwatchActivity"></activity>
   </application>

</manifest>
 


OUTPUT:


1. Implementing Activities using Intents. 
 activity_main.xml:
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout
   xmlns:android="http://schemas.android.com/apk/res/android"
   xmlns:app="http://schemas.android.com/apk/res-auto"
   xmlns:tools="http://schemas.android.com/tools"
   android:layout_width="match_parent"
   android:layout_height="match_parent"
   tools:context=".MainActivity">
   <EditText
       android:id="@+id/name"
       android:layout_width="wrap_content"
       android:layout_height="wrap_content"
       android:ems="10"
       android:hint="Name"
       android:inputType="textPersonName"
       android:minHeight="48dp"
       app:layout_constraintBottom_toBottomOf="parent"
       app:layout_constraintEnd_toEndOf="parent"
       app:layout_constraintHorizontal_bias="0.497"
       app:layout_constraintStart_toStartOf="parent"
       app:layout_constraintTop_toTopOf="parent"
       app:layout_constraintVertical_bias="0.179"
       android:importantForAutofill="no"
       tools:ignore="HardcodedText" />
 <Button
       android:id="@+id/login"
       android:layout_width="wrap_content"
       android:layout_height="wrap_content"
       android:text="LOGIN"
       app:layout_constraintBottom_toBottomOf="parent"
       app:layout_constraintEnd_toEndOf="parent"
       app:layout_constraintHorizontal_bias="0.498"
       app:layout_constraintStart_toStartOf="parent"
       app:layout_constraintTop_toBottomOf="@+id/name"
       app:layout_constraintVertical_bias="0.413"
       tools:ignore="HardcodedText" />
   <EditText
       android:id="@+id/pwd"
       android:layout_width="wrap_content"
       android:layout_height="wrap_content"
       android:ems="10"
       android:hint="Password"
       android:inputType="textPassword"
       app:layout_constraintBottom_toBottomOf="parent"
       app:layout_constraintEnd_toEndOf="parent"
       app:layout_constraintHorizontal_bias="0.497"
       app:layout_constraintStart_toStartOf="parent"
       app:layout_constraintTop_toTopOf="parent"
 app:layout_constraintVertical_bias="0.37"
       tools:ignore="Autofill,HardcodedText,TouchTargetSizeCheck" />
</androidx.constraintlayout.widget.ConstraintLayout>

activity_sndpg.xml:
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout
   xmlns:android="http://schemas.android.com/apk/res/android"
   xmlns:app="http://schemas.android.com/apk/res-auto"
   xmlns:tools="http://schemas.android.com/tools"
   android:layout_width="match_parent"
   android:layout_height="match_parent"
   tools:context=".secondpg">
   <TextView
       android:id="@+id/result"
       android:layout_width="wrap_content"
       android:layout_height="wrap_content"
       android:text="@string/textview1"
       android:textSize="30sp"
       app:layout_constraintBottom_toBottomOf="parent"
       app:layout_constraintEnd_toEndOf="parent"
       app:layout_constraintHorizontal_bias="0.494"
       app:layout_constraintStart_toStartOf="parent"
       app:layout_constraintTop_toTopOf="parent"
       app:layout_constraintVertical_bias="0.224"
       android:textColor="@color/black"/>
   <TextView
       android:id="@+id/textView2"
       android:layout_width="wrap_content"
       android:layout_height="wrap_content"
       android:text="Welcome!"
       app:layout_constraintBottom_toBottomOf="parent"
       app:layout_constraintEnd_toEndOf="parent"
       app:layout_constraintHorizontal_bias="0.498"
       app:layout_constraintStart_toStartOf="parent"
       app:layout_constraintTop_toTopOf="parent"
       app:layout_constraintVertical_bias="0.141"
       android:textSize="30sp"
       android:textColor="@color/black"
       tools:ignore="HardcodedText" />
</androidx.constraintlayout.widget.ConstraintLayout>

MainActivity.java:
package com.example.login;
import android.content.Intent;
import android.os.Bundle;
import android.widget.Button;
import android.widget.EditText;
import androidx.appcompat.app.AppCompatActivity;
public class MainActivity extends AppCompatActivity {
   public static final String EXTRA_TEXT =
           "com.example.application.example.EXTRA_TEXT";
   Button but;
   @Override
   protected void onCreate(Bundle savedInstanceState) {
       super.onCreate(savedInstanceState);
       setContentView(R.layout.activity_main);
       but = findViewById(R.id.login);
       but.setOnClickListener(v -> activity2());
   }
   public void activity2(){
       EditText editTextName= findViewById(R.id.name);
       String text =editTextName.getText().toString();
       Intent intent = new Intent(this, secondpg.class);
       intent.putExtra(EXTRA_TEXT,text);
       startActivity(intent);
   }
}

Secondpage.java:
package com.example.login;
import android.content.Intent;
import android.os.Bundle;
import android.widget.TextView;
import androidx.appcompat.app.AppCompatActivity;
public class secondpg extends AppCompatActivity {
   @Override
   protected void onCreate(Bundle savedInstanceState) {
       super.onCreate(savedInstanceState);
       setContentView(R.layout.activity_secondpg);
       Intent intent= getIntent();
       String text= intent.getStringExtra(com.example.login.MainActivity.EXTRA_TEXT);
       TextView res= findViewById(R.id.result);
       res.setText(text);
   }
}

Input screen:
 
















Output screen:
 


2.Develop an Application to set an image as wallpaper and on click of a button the image should start to change randomly


Activity_main.xml
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
   xmlns:tools="http://schemas.android.com/tools"
   android:layout_width="match_parent"
   android:layout_height="match_parent"
   tools:context=".MainActivity">
   <ImageView
       android:id="@+id/imageView"
       android:layout_width="match_parent"
       android:layout_height="match_parent"
       android:scaleType="centerCrop" />
   <Button
       android:id="@+id/changeWallpaperButton"
       android:layout_width="wrap_content"
       android:layout_height="wrap_content"
       android:layout_centerHorizontal="true"
       android:layout_alignParentBottom="true"
       android:layout_marginBottom="16dp"
       android:text="Change Wallpaper" />
</RelativeLayout>

MainActivity.java:
package com.example.activity.wallpaperchange;
import android.Manifest;
import android.annotation.SuppressLint;
import android.app.WallpaperManager;
import android.content.pm.PackageManager;
import android.os.Build;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.ImageView;
import androidx.annotation.NonNull;
import androidx.appcompat.app.AppCompatActivity;
import androidx.core.app.ActivityCompat;
import androidx.core.content.ContextCompat;
import com.example.activity.wallpaperchange.R;
import java.io.IOException;
import java.util.Random;
public class MainActivity extends AppCompatActivity {
   private static final int REQUEST_CODE_PERMISSION = 123;
   private ImageView imageView;
   private Button changeWallpaperButton;
   private int[] wallpaperImages = {
           R.drawable.wallpaper1,
           R.drawable.wallpaper2,
           R.drawable.wallpaper3
           // Add more wallpaper images as needed
   };
   @Override
   protected void onCreate(Bundle savedInstanceState) {
       super.onCreate(savedInstanceState);
       setContentView(R.layout.activity_main);
       imageView = findViewById(R.id.imageView);
       changeWallpaperButton = findViewById(R.id.changeWallpaperButton);
       // Set initial wallpaper
       setRandomWallpaper();
       // Set click listener for the button
       changeWallpaperButton.setOnClickListener(new View.OnClickListener() {
           @Override
           public void onClick(View v) {
               // Change wallpaper on button click
               setRandomWallpaper();
           }
       });
       // Request permission if not granted
       requestPermission();
   }
   private void requestPermission() {
       if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.M &&
               ContextCompat.checkSelfPermission(this, Manifest.permission.SET_WALLPAPER)
                       != PackageManager.PERMISSION_GRANTED) {
           ActivityCompat.requestPermissions(
                   this,
                   new String[]{Manifest.permission.SET_WALLPAPER},
                   REQUEST_CODE_PERMISSION
           );
       }
   }
   @SuppressLint("MissingSuperCall")
   @Override
   public void onRequestPermissionsResult(int requestCode, @NonNull String[] permissions, @NonNull int[] grantResults) {
       if (requestCode == REQUEST_CODE_PERMISSION && grantResults.length > 0
               && grantResults[0] == PackageManager.PERMISSION_GRANTED) {
           // Permission granted
       }
   }
   private void setRandomWallpaper() {
       // Choose a random wallpaper image
       int randomIndex = new Random().nextInt(wallpaperImages.length);
       int resourceId = wallpaperImages[randomIndex];
       // Set the chosen image as wallpaper
       try {
           WallpaperManager.getInstance(this).setResource(resourceId);
       } catch (IOException e) {
           e.printStackTrace();
       }
       // Set the chosen image in the ImageView
       imageView.setImageResource(resourceId);
   }
}














Input screen:
 




B 


 







Output screen:



 


 

 





3.Implementing UI component using various view layout

activity_main.xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout
   xmlns:android="http://schemas.android.com/apk/res/android"
   xmlns:tools="http://schemas.android.com/tools"
   android:layout_width="match_parent"
   android:layout_height="match_parent"
   android:orientation="vertical"
   android:padding="16dp">
   <ImageView
       android:id="@+id/profileImage"
       android:layout_width="150dp"
       android:layout_height="150dp"
       android:layout_gravity="center"
       android:layout_marginBottom="16dp"
       android:src="@drawable/ic_launcher_foreground"
       tools:ignore="ContentDescription,ImageContrastCheck" />
   <EditText
       android:id="@+id/editTextName"
       android:layout_width="375dp"
       android:layout_height="63dp"
       android:layout_marginBottom="8dp"
       android:hint="@string/name"
       tools:ignore="TextFields"
       android:importantForAutofill="no" />
   <EditText
       android:id="@+id/editTextEmail"
       android:layout_width="379dp"
       android:layout_height="59dp"
       android:layout_marginBottom="16dp"
       android:hint="Email"
       android:inputType="textEmailAddress"
       android:importantForAutofill="no"
       tools:ignore="HardcodedText" />
   <Button
       android:id="@+id/buttonSave"
       android:layout_width="289dp"
       android:layout_height="wrap_content"
       android:text="@string/save_changes" />
</LinearLayout>

MainActivity.java:
package com.example.myapplication;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.EditText;
import android.widget.ImageView;
import android.widget.Toast;
import android.appcompat.app.AppCompatActivity;
public class MainActivity extends AppCompatActivity {
   @Override
   protected void onCreate(Bundle savedInstanceState) {
       super.onCreate(savedInstanceState);
       setContentView(R.layout.ttt);
       ImageView profileImage = findViewById(R.id.profileImage);
       EditText editTextName = findViewById(R.id.editTextName);
       EditText editTextEmail = findViewById(R.id.editTextEmail);
       Button buttonSave = findViewById(R.id.buttonSave);
       buttonSave.setOnClickListener(new View.OnClickListener() {
           @Override
           public void onClick(View view) {
               String name = editTextName.getText().toString();
               String email = editTextEmail.getText().toString();
               // Save logic here (you can replace this with your actual implementation)
               // Display a toast message for demonstration purposes
               String message = "Name: " + name + "\nEmail: " + email;
               Toast.makeText(MainActivity.this, message, Toast.LENGTH_SHORT).show();
           }
       });
   }
}
























Input screen:
 


Output screen:
 

4.Develop an android application using controls like button, textview, edittext for designing a calculator having basic functionality like addition, subtraction, multiplication and division.
activity_main.xml:
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
   xmlns:tools="http://schemas.android.com/tools"
   android:layout_width="match_parent"
   android:layout_height="match_parent"
   android:orientation="vertical"
   android:padding="16dp"
   tools:context=".MainActivity">
   <EditText
       android:id="@+id/editText"
       android:layout_width="match_parent"
       android:layout_height="wrap_content"
       android:layout_marginBottom="16dp"
       android:hint="0"
       android:inputType="text"
       android:textSize="24sp"
       tools:ignore="Autofill,DuplicateSpeakableTextCheck,HardcodedText,VisualLintTextFieldSize" />
   <GridLayout
       android:layout_width="match_parent"
       android:layout_height="wrap_content"
       android:background="@color/design_default_color_primary"
       android:columnCount="4"
       android:rowCount="5">
       <!-- Buttons -->
       <Button
           style="?android:attr/borderlessButtonStyle"
           android:onClick="onClearButtonClick"
           android:text="C"
           tools:ignore="HardcodedText" />
       <Button
           style="?android:attr/borderlessButtonStyle"
           android:onClick="onOperatorClick"
           android:text="+"
           tools:ignore="HardcodedText" />
       <Button
           style="?android:attr/borderlessButtonStyle"
           android:onClick="onOperatorClick"
           android:text="-"
           tools:ignore="HardcodedText" />
       <Button
           style="?android:attr/borderlessButtonStyle"
           android:onClick="onOperatorClick"
           android:text="*"
           tools:ignore="HardcodedText" />
       <Button
           style="?android:attr/borderlessButtonStyle"
           android:onClick="onNumberClick"
           android:text="1"
           tools:ignore="HardcodedText" />
       <Button
           style="?android:attr/borderlessButtonStyle"
           android:onClick="onNumberClick"
           android:text="2"
           tools:ignore="HardcodedText" />
       <Button
           style="?android:attr/borderlessButtonStyle"
           android:onClick="onNumberClick"
           android:text="3"
           tools:ignore="HardcodedText" />
       <Button
           style="?android:attr/borderlessButtonStyle"
           android:onClick="onOperatorClick"
           android:text="/"
           tools:ignore="HardcodedText" />
       <Button
           style="?android:attr/borderlessButtonStyle"
           android:onClick="onNumberClick"
           android:text="4"
           tools:ignore="HardcodedText" />
       <Button
           style="?android:attr/borderlessButtonStyle"
           android:onClick="onNumberClick"
           android:text="5"
           tools:ignore="HardcodedText" />
       <Button
           style="?android:attr/borderlessButtonStyle"
           android:onClick="onNumberClick"
           android:text="6"
           tools:ignore="HardcodedText" />
       <Button
           style="?android:attr/borderlessButtonStyle"
           android:onClick="onNumberClick"
           android:text="."
           tools:ignore="HardcodedText" />
       <Button
           style="?android:attr/borderlessButtonStyle"
           android:onClick="onNumberClick"
           android:text="7"
           tools:ignore="HardcodedText" />
       <Button
           style="?android:attr/borderlessButtonStyle"
           android:onClick="onNumberClick"
           android:text="8"
           tools:ignore="HardcodedText" />
       <Button
           style="?android:attr/borderlessButtonStyle"
           android:onClick="onNumberClick"
           android:text="9"
           tools:ignore="HardcodedText" />
       <Button
           style="?android:attr/borderlessButtonStyle"
           android:onClick="onEqualButtonClick"
           android:text="="
           tools:ignore="DuplicateSpeakableTextCheck,HardcodedText" />
       <Button
           style="?android:attr/borderlessButtonStyle"
           android:onClick="onNumberClick"
           android:text="0"
           tools:ignore="HardcodedText" />
       <Button
           style="?android:attr/borderlessButtonStyle"
           android:layout_columnSpan="2"
           android:onClick="onEqualButtonClick"
           android:text="="
           tools:ignore="HardcodedText" />
   </GridLayout>
</LinearLayout>

MainActivity.java:
package com.example.activity.myapplicationcalc;
import android.annotation.SuppressLint;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.EditText;
import androidx.appcompat.app.AppCompatActivity;
import org.mariuszgromada.math.mxparser.Expression;
public class MainActivity extends AppCompatActivity {
   private EditText editText;
   @Override
   protected void onCreate(Bundle savedInstanceState) {
       super.onCreate(savedInstanceState);
       setContentView(R.layout.activity_main);
       editText = findViewById(R.id.editText);
   }
   public void onNumberClick(View view) {
       Button button = (Button) view;
       editText.append(button.getText());
   }
   public void onOperatorClick(View view) {
       Button button = (Button) view;
       editText.append(" " + button.getText() + " ");
   }
   public void onClearButtonClick(View view) {
       editText.setText("");
   }
   @SuppressLint("SetTextI18n")
   public void onEqualButtonClick(View view) {
       String expression = editText.getText().toString();
       try {
           Expression expr = new Expression(expression);
           double result = expr.calculate();
           editText.setText(Double.toString(result));
       } catch (Exception e) {
           editText.setText("Error");
       }
   }
}

implementation 'org.mariuszgromada.math:MathParser.org-mXparser:4.4.2'
Add this line in build.gradle (module: app)

































Input screen:

 










Output screen:
 












5.Exercise using controls like Radiogroup,Button and Checkbox.

 Layout.xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
   xmlns:tools="http://schemas.android.com/tools"
   android:orientation="vertical"
   android:layout_width="match_parent"
   android:layout_height="match_parent">
   <TextView
       android:layout_width="match_parent"
       android:layout_height="wrap_content"
       android:text="select your subject"
       android:textStyle="bold"
       android:textSize="30dp"
       tools:ignore="HardcodedText,SpUsage" />
   <CheckBox
       android:layout_width="match_parent"
       android:layout_height="wrap_content"
       android:id="@+id/tam"
       android:text="Tamil"
       android:textSize="25dp"
       tools:ignore="HardcodedText,SpUsage">
   </CheckBox>
   <CheckBox
       android:layout_width="match_parent"
       android:layout_height="wrap_content"
       android:id="@+id/eng"
       android:text="English"
       android:textSize="25dp"
       tools:ignore="HardcodedText,SpUsage">
   </CheckBox>
   <CheckBox
       android:id="@+id/social"
       android:layout_width="match_parent"
       android:layout_height="wrap_content"
       android:text="Social"
       android:textSize="25dp"
       tools:ignore="HardcodedText,SpUsage,TextSizeCheck">
   </CheckBox>
   <CheckBox
       android:layout_width="match_parent"
       android:layout_height="wrap_content"
       android:id="@+id/sci"
       android:text="Science"
       android:textSize="25dp"
       tools:ignore="HardcodedText,SpUsage">
   </CheckBox>
   <TextView
       android:id="@+id/gender"
       android:layout_width="match_parent"
       android:layout_height="wrap_content"
       android:text="Select your Gender"
       android:textSize="30dp"
       android:textStyle="bold"
       tools:ignore="HardcodedText,SpUsage" />
   <RadioGroup
       android:id="@+id/rgGender"
       android:layout_width="match_parent"
       android:layout_height="wrap_content"
       android:orientation="horizontal">
       <RadioButton
           android:id="@+id/male"
           android:layout_width="match_parent"
           android:layout_height="wrap_content"
           android:layout_weight="1"
           android:text="Male"
           android:textSize="25dp"
           tools:ignore="HardcodedText,SpUsage,TextSizeCheck" />
       <RadioButton
           android:layout_width="match_parent"
           android:layout_height="wrap_content"
           android:layout_weight="1"
           android:id="@+id/female"
           android:text="Female"
           android:textSize="25dp"
           tools:ignore="HardcodedText,SpUsage" />
   </RadioGroup>
   <Button
       android:layout_width="100dp"
       android:layout_height="50dp"
       android:id="@+id/subBtn"
       android:text="Submit"
       android:gravity="center"
       android:layout_gravity="center"
       tools:ignore="HardcodedText" />
</LinearLayout>

MainActivity.java:
package com.example.exercise5;
import androidx.appcompat.app.AppCompatActivity;
import android.annotation.SuppressLint;
import android.os.Bundle;
import android.util.Log;
import android.widget.CheckBox;
import android.widget.CompoundButton;
import android.widget.RadioButton;
import android.widget.RadioGroup;
import android.widget.Toast;
public class MainActivity extends AppCompatActivity {
   String TAG=MainActivity.class.getName();
   private CheckBox tam,eng,social,sci;
   private RadioGroup gender;
   @SuppressLint({"MissingSuperCall", "MissingInflatedId"})
   @Override
   protected void onCreate(Bundle savedInstanceState) {
       super.onCreate(savedInstanceState);
       setContentView(R.layout.layout);
           tam=findViewById(R.id.tam);
           eng=findViewById(R.id.eng);
           social=findViewById(R.id.social);
           sci=findViewById(R.id.sci);
           tam.setOnCheckedChangeListener(new CompoundButton.OnCheckedChangeListener() {
               @Override
               public void onCheckedChanged(CompoundButton compoundButton, boolean b) {
                   Log.d(TAG,tam.getText().toString()+"status"+b);
                   Toast.makeText(getApplicationContext(),tam.getText().toString()+" "+b,Toast.LENGTH_LONG).show();
               }
           });
           eng.setOnCheckedChangeListener(new CompoundButton.OnCheckedChangeListener() {
               @Override
               public void onCheckedChanged(CompoundButton compoundButton, boolean b) {
                   Log.d(TAG,eng.getText().toString()+"status"+b);
                   Toast.makeText(getApplicationContext(),eng.getText().toString()+" "+b,Toast.LENGTH_LONG).show();
               }
           });
           gender=findViewById(R.id.rgGender);
           gender.setOnCheckedChangeListener((radioGroup, i) -> {
               RadioButton radioButton=gender.findViewById(i);
               String selectedstr=radioButton.getText().toString();
               Toast.makeText(MainActivity.this, "Yourselection is"+selectedstr,Toast.LENGTH_LONG).show();});
       }
   }















Input screen:
 









Output screen:
 











6.Exercise using ProgressBar view and spinner View

activity_main.xml:
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
   xmlns:tools="http://schemas.android.com/tools"
   android:layout_width="match_parent"
   android:layout_height="match_parent"
   android:paddingLeft="16dp"
   android:paddingTop="16dp"
   android:paddingRight="16dp"
   android:paddingBottom="16dp"
   tools:context=".MainActivity">

   <ProgressBar
       android:id="@+id/progressBar"
       style="?android:attr/progressBarStyleHorizontal"
       android:layout_width="match_parent"
       android:layout_height="wrap_content"
       android:layout_centerVertical="true"
       android:layout_marginTop="20dp"/>

   <Spinner
       android:id="@+id/spinner"
       android:layout_width="match_parent"
       android:layout_height="wrap_content"
       android:layout_below="@id/progressBar"
       android:layout_marginTop="20dp"/>
</RelativeLayout>

MainActivity.java:
package com.example.record6;

import android.os.Bundle;
import android.view.View;
import android.widget.AdapterView;
import android.widget.ArrayAdapter;
import android.widget.ProgressBar;
import android.widget.Spinner;

import androidx.appcompat.app.AppCompatActivity;

import com.example.record6.R;

public class MainActivity extends AppCompatActivity {

   private ProgressBar progressBar;
   private Spinner spinner;
   @Override
   protected void onCreate(Bundle savedInstanceState) {
       super.onCreate(savedInstanceState);
       setContentView(R.layout.activity_main);

       // Initialize views
       progressBar = findViewById(R.id.progressBar);
       spinner = findViewById(R.id.spinner);

       // Set up spinner with sample data
       String[] spinnerItems = {"Level 1", "Level 2", "Level 3", "Level 4", "Level 5"};
       ArrayAdapter<String> adapter = new ArrayAdapter<>(this, android.R.layout.simple_spinner_dropdown_item, spinnerItems);
       spinner.setAdapter(adapter);

       // Set a listener for spinner item selection
       spinner.setOnItemSelectedListener(new AdapterView.OnItemSelectedListener() {
           @Override
           public void onItemSelected(AdapterView<?> parentView, View selectedItemView, int position, long id) {
               // Update progress bar based on the selected item
               int progress = (position + 1) * 20;
               progressBar.setProgress(progress);
           }

           @Override
           public void onNothingSelected(AdapterView<?> parentView) {
               // Do nothing here
           }
       });
   }
}
















Input screen:

 
Output screen:
 
7. Exercise using ImageView and TextView.

activity_main.xml:
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
   xmlns:tools="http://schemas.android.com/tools"
   android:layout_width="match_parent"
   android:layout_height="match_parent"
   android:background="@color/teal_200"
   tools:context=".MainActivity">
   <!-- ImageView to display an image -->
   <ImageView
       android:id="@+id/myImageView"
       android:layout_width="200dp"
       android:layout_height="200dp"
       android:layout_alignParentTop="true"
       android:layout_centerHorizontal="true"
       android:layout_marginTop="50dp"
       android:src="@drawable/img1" />
   <!-- TextView to display text -->
   <TextView
       android:id="@+id/myTextView"
       android:layout_width="wrap_content"
       android:layout_height="wrap_content"
       android:layout_below="@id/myImageView"
       android:layout_alignParentStart="true"
       android:layout_alignParentEnd="true"
       android:layout_alignParentBottom="true"
       android:layout_marginStart="20dp"
       android:layout_marginTop="103dp"
       android:layout_marginEnd="15dp"
       android:layout_marginBottom="342dp"
       android:text="WELCOME TO ANDROID STUDIO !"
       android:textColor="@color/black"
       android:textSize="25sp" />
</RelativeLayout>

MainActivity.java:
package com.example.textviewandimage;
import androidx.appcompat.app.AppCompatActivity;
import android.os.Bundle;
import com.example.textviewandimage.R;
public class MainActivity extends AppCompatActivity {
   @Override
   protected void onCreate(Bundle savedInstanceState) {
       super.onCreate(savedInstanceState);
       setContentView(R.layout.activity_main);
   }

OUTPUT SCREEN::


 












8. Develop an application in android that makes use of notification manager.
Activity_main.xml:
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
   xmlns:tools="http://schemas.android.com/tools"
   android:layout_width="match_parent"
   android:layout_height="match_parent"
   android:padding="16dp"
   tools:context=".MainActivity">
    <Button
       android:layout_width="wrap_content"
       android:layout_height="wrap_content"
       android:layout_centerInParent="true"
       android:text="Send Notification"
       android:onClick="sendNotification"/>
</RelativeLayout>
MainActivity.java:
package com.example.program8;
import android.app.NotificationChannel;
import android.app.NotificationManager;
import android.content.Context;
import android.os.Build;
import android.os.Bundle;
import android.view.View;
import androidx.appcompat.app.AppCompatActivity;
import androidx.core.app.NotificationCompat;
import com.example.program8.R;

public class MainActivity extends AppCompatActivity {

   private static final String CHANNEL_ID = "my_channel";
   private static final CharSequence CHANNEL_NAME = "My Channel";
   private static final String CHANNEL_DESCRIPTION = "This is my notification channel";

   @Override
   protected void onCreate(Bundle savedInstanceState) {
       super.onCreate(savedInstanceState);
       setContentView(R.layout.activity_main);

       createNotificationChannel();
   }

   private void createNotificationChannel() {
       if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.O) {
           NotificationChannel channel = new NotificationChannel(
                   CHANNEL_ID,
                   CHANNEL_NAME,
                   NotificationManager.IMPORTANCE_DEFAULT);
           channel.setDescription(CHANNEL_DESCRIPTION);
           NotificationManager notificationManager = getSystemService(NotificationManager.class);
           notificationManager.createNotificationChannel(channel);
       }
   }

   public void sendNotification(View view) {
       NotificationCompat.Builder builder = new NotificationCompat.Builder(this, CHANNEL_ID)
               .setSmallIcon(R.drawable.ic_notification)
               .setContentTitle("My Notification")
               .setContentText("This is a notification from my app")
               .setPriority(NotificationCompat.PRIORITY_DEFAULT);

       NotificationManager notificationManager = (NotificationManager) getSystemService(Context.NOTIFICATION_SERVICE);
       notificationManager.notify(1, builder.build());
   }
}
































Output:
 

 
9. Create a Stopwatch application using android studio.
Activity_main.xml:
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
   xmlns:app="http://schemas.android.com/apk/res-auto"
   xmlns:tools="http://schemas.android.com/tools"
   android:layout_width="match_parent"
   android:layout_height="match_parent"
   android:layout_gravity="center"
   android:gravity="center"
   android:orientation="vertical"
   tools:context=".MultiTaskActivity">
   <Button
       android:id="@+id/txtStopWatch"
       android:layout_width="wrap_content"
       android:layout_height="wrap_content"
       android:layout_marginTop="?actionBarSize"
       android:text="Stop Watch"
       app:layout_constraintEnd_toEndOf="parent"
       app:layout_constraintStart_toStartOf="parent"
       app:layout_constraintTop_toTopOf="parent" />
</LinearLayout>
Activity_stopwatch.xml:
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
   android:layout_width="match_parent"
   android:layout_height="match_parent"
   android:background="#0F9D58"
   android:layout_gravity="center"
   android:gravity="center"
   android:orientation="vertical"
   android:padding="16dp">
   <TextView
       android:id="@+id/time_view"
       android:layout_width="wrap_content"
       android:layout_height="wrap_content"
       android:layout_gravity="center_horizontal"
       android:textAppearance="@android:style/TextAppearance.Large"
       android:textSize="56sp" />
   <Button
       android:id="@+id/start_button"
       android:layout_width="wrap_content"
       android:layout_height="wrap_content"
       android:layout_gravity="center_horizontal"
       android:layout_marginTop="20dp"
       android:onClick="onClickStart"
       android:text="Start" />
  <Button
       android:id="@+id/stop_button"
       android:layout_width="wrap_content"
       android:layout_height="wrap_content"
       android:layout_gravity="center_horizontal"
       android:layout_marginTop="8dp"
       android:onClick="onClickStop"
       android:text="Stop" />
   <Button
       android:id="@+id/reset_button"
       android:layout_width="wrap_content"
       android:layout_height="wrap_content"
       android:layout_gravity="center_horizontal"
       android:layout_marginTop="8dp"
       android:onClick="onClickReset"
       android:text="Reset" />
</LinearLayout>
StopWatchActivity.java:
package com.example.activity.myapplication;
import android.content.Intent;
import android.os.Bundle;
import android.os.Handler;
import android.view.View;
import android.widget.Button;
import android.widget.TextView;
import androidx.annotation.Nullable;
import androidx.appcompat.app.AppCompatActivity;
import java.util.Locale;
public class StopwatchActivity extends AppCompatActivity {
   private int seconds = 0;
   // Is the stopwatch running?
   private boolean running;
   private boolean wasRunning;
   @Override
   protected void onCreate(@Nullable Bundle savedInstanceState) {
       super.onCreate(savedInstanceState);
       setContentView(R.layout.activity_stopwatch);
       if (savedInstanceState != null) {
           // Get the previous state of the stopwatch
           // if the activity has been
           // destroyed and recreated.
           seconds = savedInstanceState.getInt("seconds");
           running = savedInstanceState.getBoolean("running");
           wasRunning = savedInstanceState.getBoolean("wasRunning");
       }
       runTimer();
   }
   private void runTimer() {

       final TextView timeView = (TextView) findViewById(R.id.time_view);
       Handler handler = new Handler();
       handler.post(new Runnable() {
           @Override
           public void run() {
               int hours = seconds / 3600; //3600=1 hr
               int minutes = (seconds % 3600) / 60;
               int secs = seconds % 60;
               String time = String.format(Locale.getDefault(), "%d:%02d:%02d", hours,
                       minutes, secs);
               timeView.setText(time);
               if (running) {
                   seconds++;
               }
               // Post the code again
               // with a delay of 1 second.
               handler.postDelayed(this, 1000);
           }
       });
   }
   @Override
   public void onSaveInstanceState(Bundle savedInstanceState) {
       super.onSaveInstanceState(savedInstanceState);
       savedInstanceState.putInt("seconds", seconds);
       savedInstanceState.putBoolean("running", running);
       savedInstanceState.putBoolean("wasRunning", wasRunning);
   }
   @Override
   protected void onPause() {
       super.onPause();
       wasRunning = running;
       running = false;
   }
   // If the activity is resumed,
   // start the stopwatch
   // again if it was running previously.
   @Override
   protected void onResume() {
       super.onResume();
       if (wasRunning) {
           running = true;
       }
   }
   // Start the stopwatch running
   // when the Start button is clicked.
   // Below method gets called
   // when the Start button is clicked.
   public void onClickStart(View view) {
       running = true;
   }
   // Stop the stopwatch running
   // when the Stop button is clicked.
   // Below method gets called
   // when the Stop button is clicked.
   public void onClickStop(View view) {
       running = false;
   }
   // Reset the stopwatch when
   // the Reset button is clicked.
   // Below method gets called
   // when the Reset button is clicked.
   public void onClickReset(View view) {
       running = false;
       seconds = 0;
   }
}
MainActivity.java:
package com.example.activity.myapplication;
import android.content.Intent;
import android.os.Bundle;
import android.os.Handler;
import android.view.View;
import android.widget.Button;
import android.widget.TextView;
import androidx.annotation.Nullable;
import androidx.appcompat.app.AppCompatActivity;
import java.util.Locale;
public class StopwatchActivity extends AppCompatActivity {
   private int seconds = 0;
   // Is the stopwatch running?
   private boolean running;
   private boolean wasRunning;
   @Override
   protected void onCreate(@Nullable Bundle savedInstanceState) {
       super.onCreate(savedInstanceState);
       setContentView(R.layout.activity_stopwatch);
       if (savedInstanceState != null) {
           // Get the previous state of the stopwatch
           // if the activity has been
           // destroyed and recreated.
           seconds = savedInstanceState.getInt("seconds");
           running = savedInstanceState.getBoolean("running");
           wasRunning = savedInstanceState.getBoolean("wasRunning");
       }
       runTimer();
   }
   private void runTimer() {

       final TextView timeView = (TextView) findViewById(R.id.time_view);
       Handler handler = new Handler();
       handler.post(new Runnable() {
           @Override
           public void run() {
               int hours = seconds / 3600; //3600=1 hr
               int minutes = (seconds % 3600) / 60;
               int secs = seconds % 60;
               String time = String.format(Locale.getDefault(), "%d:%02d:%02d", hours,
                       minutes, secs);
               timeView.setText(time);
               if (running) {
                   seconds++;
               }
               // Post the code again
               // with a delay of 1 second.
               handler.postDelayed(this, 1000);
           }
       });
   }
   @Override
   public void onSaveInstanceState(Bundle savedInstanceState) {
       super.onSaveInstanceState(savedInstanceState);
       savedInstanceState.putInt("seconds", seconds);
       savedInstanceState.putBoolean("running", running);
       savedInstanceState.putBoolean("wasRunning", wasRunning);
   }
   @Override
   protected void onPause() {
       super.onPause();
       wasRunning = running;
       running = false;
   }
   // If the activity is resumed,
   // start the stopwatch
   // again if it was running previously.
   @Override
   protected void onResume() {
       super.onResume();
       if (wasRunning) {
           running = true;
       }
   }
   // Start the stopwatch running
   // when the Start button is clicked.
   // Below method gets called
   // when the Start button is clicked.
   public void onClickStart(View view) {
       running = true;
   }
   // Stop the stopwatch running
   // when the Stop button is clicked.
   // Below method gets called
   // when the Stop button is clicked.
   public void onClickStop(View view) {
       running = false;
   }
   // Reset the stopwatch when
   // the Reset button is clicked.
   // Below method gets called
   // when the Reset button is clicked.
   public void onClickReset(View view) {
       running = false;
       seconds = 0;
   }
}


Output:
 
 
 
 

10. Exercise using Action bar, menus and adding menu items. 
Activity_main.xml:
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
   xmlns:app="http://schemas.android.com/apk/res-auto"
   xmlns:tools="http://schemas.android.com/tools"
   android:layout_width="match_parent"
   android:layout_height="match_parent"
   tools:context=".MainActivity">
   <androidx.appcompat.widget.Toolbar
       android:id="@+id/toolbar"
       android:layout_width="match_parent"
       android:layout_height="?attr/actionBarSize"
       android:background="?attr/colorPrimary"/>
   <androidx.constraintlayout.widget.ConstraintLayout
       android:layout_width="match_parent"
       android:layout_height="match_parent">
       <TextView
           android:id="@+id/textView2"
           android:layout_width="wrap_content"
           android:layout_height="wrap_content"
           android:layout_marginBottom="348dp"
           android:foregroundTint="#E33C3C"
           android:text="ACTION BAR AND MENU ITEMS"
           android:textColor="#14ACF1"
           android:textSize="24sp"
           app:layout_constraintBottom_toBottomOf="parent"
           app:layout_constraintEnd_toEndOf="parent"
           app:layout_constraintHorizontal_bias="0.492"
           app:layout_constraintStart_toStartOf="parent" />
   </androidx.constraintlayout.widget.ConstraintLayout>
</RelativeLayout>
main_menu.xml:
<?xml version="1.0" encoding="utf-8"?>
<menu xmlns:android="http://schemas.android.com/apk/res/android"
   xmlns:app="http://schemas.android.com/apk/res-auto">
   <item
       android:id="@+id/action_devicecare"
       android:title="Device care"
       app:showAsAction="never"/>
   <item
       android:id="@+id/action_themes"
       android:title="Themes"
       app:showAsAction="never"/>
   <item
       android:id="@+id/action_settings"
       android:title="Settings"
       app:showAsAction="never"/>
</menu>

MainActivity.java:
package com.example.activity.ex10;
import android.os.Bundle;
import android.view.Menu;
import android.view.MenuInflater;
import android.view.MenuItem;
import android.widget.Toast;
import androidx.appcompat.app.AppCompatActivity;
import androidx.appcompat.widget.Toolbar;
public class MainActivity extends AppCompatActivity {
   @Override
   protected void onCreate(Bundle savedInstanceState) {
       super.onCreate(savedInstanceState);
       setContentView(R.layout.activity_main);

       Toolbar toolbar = findViewById(R.id.toolbar);
       setSupportActionBar(toolbar);
   }
   @Override
   public boolean onCreateOptionsMenu(Menu menu) {
       MenuInflater inflater = getMenuInflater();
       inflater.inflate(R.menu.main_menu, menu);
       return true;
   }
   @Override
   public boolean onOptionsItemSelected(MenuItem item) {
       // Handle item selection
       switch (item.getItemId()) {
           case R.id.action_devicecare:
               showToast("Device care selected");
               return true;
           case R.id.action_themes:
               showToast("Themes selected");
               return true;
           case R.id.action_settings:
               showToast("Settings selected");
               return true;
           default:
               return super.onOptionsItemSelected(item);
       }
   }
   private void showToast(String message) {
       Toast.makeText(this, message, Toast.LENGTH_SHORT).show();
   }
}



Output:
 
 

 

























11.Exercise using saving and loading user preferences.
Activity_main.xml:
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
   xmlns:tools="http://schemas.android.com/tools"
   android:layout_width="match_parent"
   android:layout_height="match_parent"
   android:padding="16dp"
   tools:context=".MainActivity">
   <TextView
       android:id="@+id/tv_language"
       android:layout_width="wrap_content"
       android:layout_height="wrap_content"
       android:text="Preferred Language:"
       android:textSize="18sp"
       android:layout_marginTop="16dp" />
   <Spinner
       android:id="@+id/spinner_language"
       android:layout_width="wrap_content"
       android:layout_height="wrap_content"
       android:layout_below="@id/tv_language"
       android:layout_marginTop="8dp" />
   <TextView
       android:id="@+id/tv_font_size"
       android:layout_width="wrap_content"
       android:layout_height="wrap_content"
       android:text="Preferred Font Size:"
       android:textSize="18sp"
       android:layout_below="@id/spinner_language"
       android:layout_marginTop="16dp" />
   <SeekBar
       android:id="@+id/seekBar_font_size"
       android:layout_width="match_parent"
       android:layout_height="wrap_content"
       android:layout_below="@id/tv_font_size"
       android:layout_marginTop="8dp"
       android:max="30"
       android:progress="18" />
   <Button
       android:id="@+id/btn_save"
       android:layout_width="wrap_content"
       android:layout_height="wrap_content"
       android:text="Save Preferences"
       android:layout_below="@id/seekBar_font_size"
       android:layout_centerHorizontal="true"
       android:layout_marginTop="24dp" />

</RelativeLayout>


arrays.xml:
<resources>
   <string-array name="languages_array">
       <item>English</item>
       <item>Spanish</item>
       <item>French</item>
       <item>German</item>
       <item>Chinese</item>
   </string-array>
</resources>
MainActivity.java:
package com.example.activity.program10;
import android.content.SharedPreferences;
import android.os.Bundle;
import android.widget.ArrayAdapter;
import android.widget.Button;
import android.widget.SeekBar;
import android.widget.Spinner;
import android.widget.Toast;
import androidx.appcompat.app.AppCompatActivity;
public class MainActivity extends AppCompatActivity {
   private Spinner spinnerLanguage;
   private SeekBar seekBarFontSize;
   private Button btnSave;
   private SharedPreferences preferences;
   private static final String PREF_NAME = "user_preferences";
   private static final String KEY_LANGUAGE = "preferred_language";
   private static final String KEY_FONT_SIZE = "preferred_font_size";
   @Override
   protected void onCreate(Bundle savedInstanceState) {
       super.onCreate(savedInstanceState);
       setContentView(R.layout.activity_main);
       spinnerLanguage = findViewById(R.id.spinner_language);
       seekBarFontSize = findViewById(R.id.seekBar_font_size);
       btnSave = findViewById(R.id.btn_save);
       // Set up spinner with language options
       ArrayAdapter<CharSequence> adapter = ArrayAdapter.createFromResource(this,
               R.array.languages_array, android.R.layout.simple_spinner_item);
       adapter.setDropDownViewResource(android.R.layout.simple_spinner_dropdown_item);
       spinnerLanguage.setAdapter(adapter);
       preferences = getSharedPreferences(PREF_NAME, MODE_PRIVATE);
       // Load preferences
       loadPreferences();
       btnSave.setOnClickListener(v -> savePreferences());
   }
   private void loadPreferences() {
       String language = preferences.getString(KEY_LANGUAGE, "");
       int fontSize = preferences.getInt(KEY_FONT_SIZE, 18);

       // Set saved preferences
       spinnerLanguage.setSelection(getIndex(spinnerLanguage, language));
       seekBarFontSize.setProgress(fontSize);
   }
   private void savePreferences() {
       String selectedLanguage = spinnerLanguage.getSelectedItem().toString();
       int selectedFontSize = seekBarFontSize.getProgress();
       // Save preferences
       SharedPreferences.Editor editor = preferences.edit();
       editor.putString(KEY_LANGUAGE, selectedLanguage);
       editor.putInt(KEY_FONT_SIZE, selectedFontSize);
       editor.apply();
       Toast.makeText(this, "Preferences saved successfully", Toast.LENGTH_SHORT).show();
   }
   private int getIndex(Spinner spinner, String value) {
       for (int i = 0; i < spinner.getCount(); i++) {
           if (spinner.getItemAtPosition(i).toString().equalsIgnoreCase(value)) {
               return i;
           }
       }
       return 0;
   }
}


























Output:
 

 


12. Create SQLite database using dbadapter helper
Code:
Activity_main.xml:
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
xmlns:app="http://schemas.android.com/apk/res-auto"
xmlns:tools="http://schemas.android.com/tools"
android:layout_width="match_parent"
android:layout_height="match_parent"
android:orientation="vertical"
tools:context=".MainActivity">
<TextView
android:layout_width="match_parent"
android:layout_height="wrap_content"
android:text="Enter Name"
android:textSize="30dp"/>
<EditText
android:id="@+id/edttxtname"
android:layout_width="match_parent"
android:layout_height="wrap_content"
android:textSize="30dp"
tools:ignore="SpeakableTextPresentCheck" />
<TextView
android:layout_width="match_parent"
android:layout_height="wrap_content"
android:text="Enter Age"
android:textSize="30dp"/>
<EditText
android:id="@+id/edttxtage"
android:layout_width="match_parent"
android:layout_height="wrap_content"
android:textSize="30dp"
tools:ignore="SpeakableTextPresentCheck" />
<Button
android:layout_width="match_parent"
android:layout_height="wrap_content"
android:id="@+id/btnsave"
android:text="Save"/>
</LinearLayout>

MainActivity.java:
package com.example.database;
import androidx.appcompat.app.AppCompatActivity;
import android.content.Context;
import android.database.sqlite.SQLiteDatabase;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.EditText;
import android.widget.Toast;
import com.example.database.R;
public class MainActivity extends AppCompatActivity {
SQLiteDatabase db;
Button btnsave;
@Override
protected void onCreate(Bundle savedInstanceState) {
super.onCreate(savedInstanceState);
setContentView(R.layout.activity_main);
btnsave=(Button)findViewById(R.id.btnsave);
EditText edttxtname = (EditText) findViewById(R.id.edttxtname);
EditText edttxtage = (EditText) findViewById(R.id.edttxtage);
db=openOrCreateDatabase("StudentDB", Context.MODE_PRIVATE,null);
db.execSQL("CREATE TABLE IF NOT EXISTS Student1(Name VARCHAR,Age
VARCHAR);");
btnsave.setOnClickListener(new View.OnClickListener() {
@Override
public void onClick(View view) {
//Toast.makeText(getApplicationContext(),"Database Created",Toast.LENGTH_LONG).show();
db.execSQL("INSERT INTO Student1 VALUES( '"+edttxtname.getText()+"','"+
edttxtage.getText()+"');");
Toast.makeText(getApplicationContext(),"Record Inserted",Toast.LENGTH_LONG).show();
}});
}}

13. Perform CURD (create, update, read, delete) operations
Activity_main.xml:
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
   xmlns:app="http://schemas.android.com/apk/res-auto"
   xmlns:tools="http://schemas.android.com/tools"
   android:layout_width="match_parent"
   android:layout_height="match_parent"
   android:orientation="vertical"
   tools:context=".MainActivity">

   <TextView
       android:layout_width="match_parent"
       android:layout_height="wrap_content"
       android:text="Enter Roll.No"
       android:textSize="30dp"
       />
   <EditText
       android:layout_width="match_parent"
       android:layout_height="wrap_content"
       android:id="@+id/edttxtrollno"
       android:textSize="30dp"
       />

   <TextView
       android:layout_width="match_parent"
       android:layout_height="wrap_content"
       android:text="Enter Name"
       android:textSize="30dp"
       />
   <EditText
       android:layout_width="match_parent"
       android:layout_height="wrap_content"
       android:id="@+id/edttxtname"
       android:textSize="30dp"
       />

   <TextView
       android:layout_width="match_parent"
       android:layout_height="wrap_content"
       android:text="Enter Age"
       android:textSize="30dp"
       />
   <EditText
       android:layout_width="match_parent"
       android:layout_height="wrap_content"
       android:id="@+id/edttxtage"
       android:textSize="30dp"
       />
   <Button
       android:layout_width="match_parent"
       android:layout_height="wrap_content"
       android:id="@+id/btnsave"
       android:text="Save"
       />

   <Button
       android:layout_width="match_parent"
       android:layout_height="wrap_content"
       android:id="@+id/btnDelete"
       android:text="Delete"
       />
   <Button
       android:layout_width="match_parent"
       android:layout_height="wrap_content"
       android:id="@+id/btnView"
       android:text="View"
       />

   <Button
       android:layout_width="match_parent"
       android:layout_height="wrap_content"
       android:id="@+id/btnModify"
       android:text="Modify"
       />
</LinearLayout>

MainActivity.java:
package com.example.myapplication1;
import androidx.appcompat.app.AppCompatActivity;
import android.content.Context;
import android.database.Cursor;
import android.database.sqlite.SQLiteDatabase;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.EditText;
import android.widget.Toast;
public class MainActivity extends AppCompatActivity {
   SQLiteDatabase db;
   Button btnsave,btnDelete,btnModify,btnView,btnViewAll;
   @Override
   protected void onCreate(Bundle savedInstanceState) {
       super.onCreate(savedInstanceState);
       setContentView(R.layout.activity_main);
       btnsave=(Button)findViewById(R.id.btnsave);
       btnDelete=(Button) findViewById(R.id.btnDelete) ;
       btnModify=(Button) findViewById(R.id.btnModify) ;
       btnView=(Button) findViewById(R.id.btnView) ;
       EditText edttxtrollno = (EditText) findViewById(R.id.edttxtrollno);
       EditText edttxtname = (EditText) findViewById(R.id.edttxtname);
       EditText edttxtage = (EditText) findViewById(R.id.edttxtage);
       db=openOrCreateDatabase("StudentDB", Context.MODE_PRIVATE,null);
       btnsave.setOnClickListener(new View.OnClickListener() {
           @Override
           public void onClick(View view) {
               //Toast.makeText(getApplicationContext(),"Database Created",Toast.LENGTH_LONG).show();
               db.execSQL("CREATE TABLE IF NOT EXISTS Studentnew(Rollno VARCHAR, Name VARCHAR,Age VARCHAR);");
               //db.execSQL("INSERT INTO Student1 VALUES( '"+edttxtname.getText()+"','"+ edttxtage.getText()+"');");     db.execSQL("INSERT INTO Studentnew VALUES( '" + edttxtrollno.getText()+"', '"+edttxtname.getText()+"','"+ edttxtage.getText()+"');");
               showToast("Record Inserted");
               edttxtrollno.setText("");
               edttxtname.setText("");
               edttxtage.setText("");
           }});
btnDelete.setOnClickListener(new View.OnClickListener() {
           @Override
           public void onClick(View view) {
db.execSQL("Delete from Studentnew where Rollno='"+ edttxtrollno.getText()+"'");
               showToast("Record Deleted");
               edttxtrollno.setText("");
               edttxtname.setText("");
               edttxtage.setText("");
           }
       });
       btnView.setOnClickListener(new View.OnClickListener() {
           @Override
           public void onClick(View view) {
               if(edttxtrollno.getText().toString().trim().length()==0){
                   showToast("Please enter Rollno"); }
               Cursor c=db.rawQuery("SELECT * FROM Studentnew WHERE Rollno='"+edttxtrollno.getText()+"'", null);
               if(c.moveToFirst())
               { if(c.getCount()==0)
                   {
                       showToast("No Record Found");
                   } else{
                       edttxtname.setText(c.getString(1));
                       edttxtage.setText(c.getString(2));
                   }  } else {
                   showToast("No Record Found ");
               } }
       });
 btnModify.setOnClickListener(new View.OnClickListener() {
           @Override
           public void onClick(View view) {

               if(edttxtrollno.getText().toString().trim().length()==0)
               {
                   showToast("Please enter Rollno");
               }
               Cursor c=db.rawQuery("SELECT * FROM Studentnew WHERE Rollno='"+edttxtrollno.getText()+"'", null);
               if(c.moveToFirst(){
                   db.execSQL("UPDATE Studentnew SET Name='"+edttxtname.getText()+"',Age='"+edttxtage.getText()+
                           "' WHERE Rollno='"+edttxtrollno.getText()+"'");
                   showToast("Record Updated");
                   edttxtrollno.setText("");
                   edttxtname.setText("");
                   edttxtage.setText("");
               }}
       });}
   private void showToast(String message) {
       Toast.makeText(this, message, Toast.LENGTH_SHORT).show();
   }}



Output:
 

 
 

 


13.CURD:
activity_main.xml:
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
   xmlns:tools="http://schemas.android.com/tools"
   android:layout_width="match_parent"
   android:layout_height="match_parent"
   android:padding="16dp"
   tools:context=".MainActivity">

   <EditText
       android:id="@+id/edttxtname"
       android:layout_width="match_parent"
       android:layout_height="wrap_content"
       android:hint="Name"
       android:layout_marginBottom="16dp"/>

   <EditText
       android:id="@+id/edttxtage"
       android:layout_width="match_parent"
       android:layout_height="wrap_content"
       android:hint="Age"
       android:layout_below="@id/edttxtname"
       android:layout_marginBottom="16dp"/>

   <Button
       android:id="@+id/btnsave"
       android:layout_width="match_parent"
       android:layout_height="wrap_content"
       android:text="Save"
       android:layout_below="@id/edttxtage"
       android:layout_marginBottom="16dp"/>

   <Button
       android:id="@+id/btnupdate"
       android:layout_width="match_parent"
       android:layout_height="wrap_content"
       android:text="Update"
       android:layout_below="@id/btnsave"
       android:layout_marginBottom="16dp"/>

   <Button
       android:id="@+id/btndelete"
       android:layout_width="match_parent"
       android:layout_height="wrap_content"
       android:text="Delete"
       android:layout_below="@id/btnupdate"
       android:layout_marginBottom="16dp"/>

   <Button
       android:id="@+id/btnread"
       android:layout_width="match_parent"
       android:layout_height="wrap_content"
       android:text="Read"
       android:layout_below="@id/btndelete"
       android:layout_marginBottom="16dp"/>

</RelativeLayout>

MainActivity.java:
package com.example.curd;

import android.annotation.SuppressLint;
import android.content.Context;
import android.database.Cursor;
import android.database.sqlite.SQLiteDatabase;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.EditText;
import android.widget.Toast;

import androidx.appcompat.app.AppCompatActivity;

public class MainActivity extends AppCompatActivity {

   SQLiteDatabase db;
   Button btnsave, btnupdate, btndelete, btnread;
   EditText edttxtname, edttxtage;

   @SuppressLint("MissingInflatedId")
   @Override
   protected void onCreate(Bundle savedInstanceState) {
       super.onCreate(savedInstanceState);
       setContentView(R.layout.activity_main);

       btnsave = findViewById(R.id.btnsave);
       btnupdate = findViewById(R.id.btnupdate);
       btndelete = findViewById(R.id.btndelete);
       btnread = findViewById(R.id.btnread);
       edttxtname = findViewById(R.id.edttxtname);
       edttxtage = findViewById(R.id.edttxtage);

       db = openOrCreateDatabase("StudentDB", Context.MODE_PRIVATE, null);
       db.execSQL("CREATE TABLE IF NOT EXISTS Student1(Name VARCHAR,Age VARCHAR);");

       btnsave.setOnClickListener(new View.OnClickListener() {
           @Override
           public void onClick(View view) {
               insertRecord();
           }
       });

       btnupdate.setOnClickListener(new View.OnClickListener() {
           @Override
           public void onClick(View view) {
               updateRecord();
           }
       });

       btndelete.setOnClickListener(new View.OnClickListener() {
           @Override
           public void onClick(View view) {
               deleteRecord();
           }
       });

       btnread.setOnClickListener(new View.OnClickListener() {
           @Override
           public void onClick(View view) {
               readRecords();
           }
       });
   }

   private void insertRecord() {
       db.execSQL("INSERT INTO Student1 VALUES('"+edttxtname.getText()+"','"+ edttxtage.getText()+"');");
       Toast.makeText(getApplicationContext(),"Record Inserted",Toast.LENGTH_LONG).show();
   }

   private void updateRecord() {
       db.execSQL("UPDATE Student1 SET Age='"+edttxtage.getText()+"' WHERE Name='"+edttxtname.getText()+"';");
       Toast.makeText(getApplicationContext(),"Record Updated",Toast.LENGTH_LONG).show();
   }

   private void deleteRecord() {
       db.execSQL("DELETE FROM Student1 WHERE Name='"+edttxtname.getText()+"';");
       Toast.makeText(getApplicationContext(),"Record Deleted",Toast.LENGTH_LONG).show();
   }

   private void readRecords() {
       Cursor cursor = db.rawQuery("SELECT * FROM Student1", null);
       StringBuilder stringBuilder = new StringBuilder();
       if (cursor.moveToFirst()) {
           do {
               String name = cursor.getString(0);
               String age = cursor.getString(1);
               stringBuilder.append("Name: ").append(name).append(", Age: ").append(age).append("\n");
           } while (cursor.moveToNext());
       }
       cursor.close();
       Toast.makeText(getApplicationContext(), stringBuilder.toString(), Toast.LENGTH_LONG).show();
   }
}

14.SMS
activity_main.xml:
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
   xmlns:app="http://schemas.android.com/apk/res-auto"
   xmlns:tools="http://schemas.android.com/tools"
   android:layout_width="match_parent"
   android:layout_height="match_parent"
   tools:context=".MainActivity2">

   <EditText
       android:id="@+id/editTextPhoneNo"
       android:layout_width="wrap_content"
       android:layout_height="wrap_content"
       android:ems="10"
       android:inputType="textPersonName"
       android:text="Name"
       app:layout_constraintBottom_toBottomOf="parent"
       app:layout_constraintEnd_toEndOf="parent"
       app:layout_constraintHorizontal_bias="0.502"
       app:layout_constraintStart_toStartOf="parent"
       app:layout_constraintTop_toTopOf="parent"
       app:layout_constraintVertical_bias="0.115"
       tools:ignore="MissingConstraints" />

   <EditText
       android:id="@+id/editTextSMS"
       android:layout_width="wrap_content"
       android:layout_height="wrap_content"
       android:ems="10"
       android:inputType="textPersonName"
       android:text="Name"
       app:layout_constraintBottom_toBottomOf="parent"
       app:layout_constraintEnd_toEndOf="parent"
       app:layout_constraintHorizontal_bias="0.497"
       app:layout_constraintStart_toStartOf="parent"
       app:layout_constraintTop_toTopOf="parent"
       app:layout_constraintVertical_bias="0.225"
       tools:ignore="MissingConstraints" />

   <Button
       android:id="@+id/buttonSend"
       android:layout_width="wrap_content"
       android:layout_height="wrap_content"
       android:text="Send"
       app:layout_constraintBottom_toBottomOf="parent"
       app:layout_constraintEnd_toEndOf="parent"
       app:layout_constraintHorizontal_bias="0.349"
       app:layout_constraintStart_toStartOf="parent"
       app:layout_constraintTop_toTopOf="parent"
       app:layout_constraintVertical_bias="0.383"
       tools:ignore="MissingConstraints" />

   <Button
       android:id="@+id/btnback"
       android:layout_width="wrap_content"
       android:layout_height="wrap_content"
       android:text="Back"
       app:layout_constraintBottom_toBottomOf="parent"
       app:layout_constraintEnd_toEndOf="parent"
       app:layout_constraintHorizontal_bias="0.727"
       app:layout_constraintStart_toStartOf="parent"
       app:layout_constraintTop_toTopOf="parent"
       app:layout_constraintVertical_bias="0.383"
       tools:ignore="MissingConstraints" />
</androidx.constraintlayout.widget.ConstraintLayout>


MainActivity.java:
package com.example.myapplication1;

import androidx.appcompat.app.AppCompatActivity;
import android.os.Bundle;
import android.content.Intent;
import android.net.Uri;
import android.view.View;
import android.widget.Button;
import android.widget.EditText;
import android.widget.Toast;
public class MainActivity2 extends AppCompatActivity {
   Button buttonSend,btnback;
   EditText textPhoneNo,textSMS;

   @Override
   protected void onCreate(Bundle savedInstanceState) {
       super.onCreate(savedInstanceState);
       setContentView(R.layout.activity_main2);

       buttonSend = (Button) findViewById(R.id.buttonSend);
       textPhoneNo = (EditText) findViewById(R.id.editTextPhoneNo);
       textSMS = (EditText) findViewById(R.id.editTextSMS);
       buttonSend.setOnClickListener(new View.OnClickListener() {

           @Override
           public void onClick(View v) {

               String phoneNo = textPhoneNo.getText().toString();
               String sms = textSMS.getText().toString();

               try {
                   // SmsManager smsManager = SmsManager.getDefault();
                   // smsManager.sendTextMessage(phoneNo, null, sms, null, null);
                   Intent in = new Intent(Intent.ACTION_VIEW, Uri.parse( "sms:" + phoneNo ) );
                   in.putExtra( "sms_body", sms );
                   startActivity(in);

                   Toast.makeText(getApplicationContext(), "SMS Sent!", Toast.LENGTH_LONG).show();
               } catch (Exception e) {
                   Toast.makeText(getApplicationContext(),e.getMessage(),Toast.LENGTH_LONG).show();
               }
           }
       });

       btnback=(Button)findViewById(R.id.btnback);
       btnback.setOnClickListener(new View.OnClickListener() {
           @Override
           public void onClick(View v) {
               Intent  i1=new Intent(MainActivity2.this,MainActivity.class);
               startActivity(i1);
           }
       });
   }
}


Androidmanifest.xml
before  the application tag opening
<uses-permission android:name="android.permission.SEND_SMS"/>
<uses-permission android:name="android.permission.RECEIVE_SMS"/>



 
 
 

 








