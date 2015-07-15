# Android Toolbar

We’ll show you how to replace the ActionBar with the Toolbar.

### Add Support Library

To implement Toolbar, make sure to add the Support Library setup instructions first. (make sure these versions have been updated.)

```gradle
dependencies {
  compile 'com.android.support:appcompat-v7:22.2.0'
}
 ```
 
### Replace the ActionBar
 
 Change the theme to "Theme.AppCompat.Light.NoActionBar" at `style.xml `.
 
```xml
 <resources>

    <style name="AppTheme" parent="Theme.AppCompat.Light.NoActionBar">
        <item name="colorPrimary">@color/ColorPrimary</item>
        <item name="colorPrimaryDark">@color/ColorPrimaryDark</item>
        <item name="android:textColorPrimary">@color/textColorPrimary</item>
    </style>

</resources>
```
 Add your color scheme for our project, you can see from the image below. There are attributes which you can set to get a basic color scheme of your App.
 
 ![show1](http://i.imgur.com/GGhcgXy.png?1)
 
 You need add a file `color.xml` in your values folder and add the color attributes as shown in the below code.
 
```xml
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <color name="ColorPrimary">#FF5722</color>
    <color name="ColorPrimaryDark">#E64A19</color>
    <color name="textColorPrimary">#ffe6dfde</color>
</resources>
```
### Toolbar Widget

Now lets make a Toolbar, it is just like any other layout which can be placed at any place in your UI. We create a file called `tool_bar.xml`.

```xml
<?xml version="1.0" encoding="utf-8"?>
<android.support.v7.widget.Toolbar xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="?attr/actionBarSize"
    android:background="@color/ColorPrimary">

</android.support.v7.widget.Toolbar>

```
Include it in `activity_main.xml`.

```xml
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">

    <include
        android:id="@+id/tool_bar"
        layout="@layout/tool_bar"/>

    <TextView
        android:text="@string/hello_world"
        android:layout_below="@+id/tool_bar"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"/>

</RelativeLayout>
```

### Set up the Toolbar

```java
public class MainActivity extends AppCompatActivity {

    private Toolbar toolbar;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        // Attaching the layout to the toolbar object
        toolbar = (Toolbar) findViewById(R.id.tool_bar);
        // Setting toolbar as the ActionBar with setSupportActionBar() call
        setSupportActionBar(toolbar);
    }
}
```
![show2](http://i.imgur.com/gEMuheJ.png?1)

### Toolbar component

There are some common components to customize the Toolbar.

![show3](http://i.imgur.com/vX4s27L.png?1)

1. setNavigationIcon
2. setLogo
3. setTitle
4. setSubtitle
5. set the `menu_main.xml`

```java
// App Logo
toolbar.setLogo(R.mipmap.ab_android);
// Navigation Icon
toolbar.setNavigationIcon(R.mipmap.ic_launcher);
// Title
toolbar.setTitle("My Title");
// Sub Title
toolbar.setSubtitle("Sub title");
```
Add item in the `menu_main.xml` as shown below

```xml
<menu xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools" tools:context=".MainActivity">

    <item android:id="@+id/action_edit"
        android:title="edit"
        android:orderInCategory="80"
        android:icon="@mipmap/ab_edit"
        app:showAsAction="ifRoom" />

    <item android:id="@+id/action_share"
        android:title="share"
        android:orderInCategory="90"
        android:icon="@mipmap/ab_share"
        app:showAsAction="ifRoom" />

    <item android:id="@+id/action_settings"
        android:title="@string/action_settings"
        android:orderInCategory="100"
        app:showAsAction="never" />
</menu>
```

### Set listener

Implements `Toolbar.OnMenuItemClickListener`

```java
public class MainActivity extends AppCompatActivity implements Toolbar.OnMenuItemClickListener {

    private Toolbar toolbar;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        ...
        
        // Setting toolbar as the ActionBar with setSupportActionBar() call
        setSupportActionBar(toolbar);
        getSupportActionBar().setDisplayShowHomeEnabled(true);
        // Navigation Icon
        toolbar.setNavigationIcon(R.mipmap.ic_launcher);
        toolbar.setNavigationOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                Toast.makeText(MainActivity.this, "Click Navigation Icon", Toast.LENGTH_SHORT).show();
            }
        });

        //set Listener(must below of the setSupportActionBar)
        toolbar.setOnMenuItemClickListener(this);

    }

    @Override
    public boolean onOptionsItemSelected(MenuItem menuItem) {
        if (menuItem.getItemId() == android.R.id.home) {
            Toast.makeText(MainActivity.this, "Click Navigation Icon", Toast.LENGTH_SHORT).show();
        }
        return super.onOptionsItemSelected(menuItem);
    }
...

    @Override
    public boolean onMenuItemClick(MenuItem menuItem) {
        String msg = "";
        switch (menuItem.getItemId()) {
            case R.id.action_edit:
                msg += "Click edit";
                break;
            case R.id.action_share:
                msg += "Click share";
                break;
            case R.id.action_settings:
                msg += "Click setting";
                break;
        }

        if(!msg.equals("")) {
            Toast.makeText(MainActivity.this, msg, Toast.LENGTH_SHORT).show();
        }
        return true;
    }
}
```

## References

* <http://blog.mosil.biz/2014/10/android-toolbar/>
* <http://www.101apps.co.za/index.php/articles/using-toolbars-in-your-apps.html>
* <http://www.android4devs.com/2014/12/how-to-make-material-design-app.html>


