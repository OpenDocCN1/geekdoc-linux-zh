# Design advanced user interfaces for Android
Create complex GUIs with minimal effort
TUTORIAL

method can be unreliable in some parts of the fragment’s lifecycle (Fig. 09)
Finally, the button’s onClick handler is wired to the DetailActivity’s withdrawFragment function. It is responsible for “wiping” the fragment off the screen (Fig. 10).
With that, the application can be tested. Moving the phone to landscape mode will be rewarded with both views being displayed next to one another. The back button will not show up as it is suppressed by the above-shown logic.

# Fragment to fragment
Google’s developer documentation specifies that fragments must not communicate with one another. Instead, data should be exchanged via the activity hosting the elements. If the list hosted in FeedListFragment gets clicked, the activity is notified (Fig. 11). Its implementation can be seen in Fig. 12.
If the handset is in portrait mode, our code limits itself to updating the contents of the text box. If the fragment is not there yet, we must open a new activity. This is done by sending a so-called intent, which can be extended with additional data for the recipient.
This is necessary because of a limitation in the operating system. Fragments declared in an XML file get stripped from their containers during creation. This leads to improved performance, as the object tree becomes more shallow.
Sadly, code such as the one below, will not work as the fragment manager will not be able to find the original framework. This leads to the situation where the two fragments are shown above one another:

```
FragmentTransaction ft = –
getFragmentManager().beginTransaction();
ft.replace(R.id.titles, new •
MessageFragment());
ft.commit();

This problem can be solved by adding a second activity to the project. activity_detail.xml starts out as a carbon copy of activity_main, but is provided with the changes in Fig. 12. The code behind the class is relatively primitive, as you can see in Fig. 13.
During the creation of the activity, we parse the intent in order to retrieve the string which is to be shown in the text box. WithdrawFragment() accomplishes its act by invoking the finish() method. It ends the activity’s lifecycle immediately, thereby exposing the list activity below it. Finally, DetailActivity must be declared inside the manifest file as per following:
```

```
public void onIemCllck(<> AdapterView> argO, View arq1, int arq2, long arq3) {MainActivity act=((MainActivity) getActivity();
act.updateContent(myTask_descVec, get(arq2));
}

public void updateContent(String _toWhat) {
if (myMessageFragment!=null){
TextView myTv=((TextView) findViewById (R id, descView); 
myTv, setText (_toWhat);
} else{//Must launch new activity
Intent intent=new Intent;
intent, setclass(this, DetailActivity, class);
intent, putExtra("toWhat", _toWhat)
startActivity(intent);
}
```

```
<FrameLayout xmlns:android="http://schemas.android.com/apk/res/android"
tools: context="com.example_rsrt ool, Detail Activity"
tools:ignore="MergeRoot Frame" >

<fragment android: name='"com_example_rstool, Message Fragment"
android: id="@id/titles" android:layout_width="match_parent"
android:layout height="match_parent" />
</FrameLayout>
```

```
public class DetailActivity extends Activity
{
public String myToWhat;
protected void onCr eat & Bundle savedInstanceState) {
super.onCreate(savedInstanceState) ;
setContentView(R, layout, activity_detail);

Intent intent=getIntent();
myToWhat=intent, getStringExtra("toW hat") ;
}
public void withdrawFragment(){
finish();
}
```

```
DetailActivity"
android: label = "@string/app name" >
<intent-filter><intent-filter>
</activity>
```

<activity
android:name="com.example.rstool.

you with all the important concepts. Finding solutions to further problems should now be but a question of hitting Stack Overflow.
For now, our journey through the world of Android shall end. Let us conclude this final instalment with a bit of advice: pay attention to reviews and user feedback, rather from the Play Store or from friends and colleagues who have tested your unreleased app, and be sure to adjust your code accordingly if you want to make your app a success. And keep coding – the developer of Flappy Bird had to launch a bunch of other games before they hit the mother lode.

At this point, the Android GUI stack is likely to complain about the invocation of setOnCllck.Listen er for the list. In order to remove the exception, replace the line with:
myView.setOnItemClick. Lister ( this);

# Conclusion
Getting started with fragments, lists and the layout system can be a daunting task. The steps outlined in this tutorial should have familiarised