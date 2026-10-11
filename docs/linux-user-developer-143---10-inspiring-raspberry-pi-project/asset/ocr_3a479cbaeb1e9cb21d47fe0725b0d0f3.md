# # Design advanced user interfaces for Android
Create complex GUIs with minimal effort
TUTORIAL

```
public class MyArrayAdapter extends
ArrayAdapter<String>
{
public Context myContext;
public Vector<String> myTitles;
int myResource;

public MyArrayAdapter(Context context, int resource, Vector<String> _myTitles) {
super(context, resource);
myContext=context;
myTitles=_myTitles;
myResource=resource;
}

@Override
public int getCount()
{
return myTitles.size();
}
}
```

Android uses widgets in order to display the individual rows of the list. GetView is responsible for the generation of said widget, which gets created from the layout presented above (Fig.04).

With that, our application is ready. The “titles” of the feed in question will be displayed in a visually pleasing list. Sadly, story content is not shown by the current version of our application.

# ## Going landscape

Programs such as Microsoft Outlook and Mozilla Thunderbird have accustomed users to a Master- Slave view. Clicking the title of an email opens its contents in a different pane. Initially, this paradigm could not be implemented on mobile phones as the screen resolution was too low.

As technology evolved, companies like WeblB tried to implement “split views” in their products. In order to make things a little bit more interesting, our application shall use this advanced paradigm only when running in landscape mode. Clicking a feed in portrait mode shall, instead, open a new window showing the feed in its entirety.

The first step involves the creation of a new layout which will be used only in landscape mode. Right-click the folder /res/layout, and select the option New»Android XML Layout. The file name must be “activity_main.xml” – Eclipse’s warning about the existing file can be ignored.

Proceed by clicking Next in order to open the configuration dialog. Android’s resource system can select the correct resource file via a batch of parameters. In our case, select the qualifier “Layout Direction”, which can then be parametrised to select portrait, landscape or

![](bbox=[0.84, 0.15, 0.93, 0.17])

```
public class FeedListFragment extends ListFragment implements OnClickListener
{

HTTPTask myTask;
MyArrayAdapter myAdapter;
Context myContext;

@Override
public void onCreate(Bundle savedInstanceState) {
myTask=new HTTPTask();
super.onCreate(savedInstanceState);
getListView().setOnlickListener(this);
}

@Override
public void onViewCreated(View view, Bundle savedInstanceState) {
myTask.myFragment=this;
myTask.execute(“http://www.rssboard.org/files/sample-rss-2.xml”);
super.onViewCreated(view, savedInstanceState);
}

public void configureMe(){
if (myContext==null)
{
myContext=getActivity();
}
myAdapter=new MyArrayAdapter(myContext, R.layout.listlineLayout, myTask.titleVect);
setListAdapter(myAdapter);
}
}
```

![](bbox=[0.84, 0.5, 0.93, 0.52])

```
protected void onCreate(Bundle savedInstanceState){
super.onCreate(savedInstanceState);
setContentView(R.layout.activity_main);

if (savedInstanceState == null) {
FeedListFragment myFragment=new FeedListFragment();
myFragment.myContext=getApplicationContext();
getFragmentManager().beginTransaction()
.add(R.id.container, myFragment).commit();
}
}
```

![](bbox=[0.84, 0.64, 0.93, 0.66])

```
@Override
public View getView(int position, View convertView, ViewGroup parent) {
LayoutInflater inflater = (LayoutInflater) myContext.
getSystemService(Context.LAYOUT_INFLATER_SERVICE);
View rowView = inflater.inflate(myResource, parent, false);

TextView letterView = (TextView) rowView.findViewById(R.id.textLarge);
TextView textView = (TextView) rowView.findViewById(R.id.textSmall);
letterView.setText(myTitles.get(position).substring(0, 1));
textView.setText(myTitles.get(position).substring(1));
return rowView;
}
```