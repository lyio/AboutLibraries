#AboutLibraries  [![Maven Central](https://maven-badges.herokuapp.com/maven-central/com.mikepenz.aboutlibraries/library/badge.svg?style=flat)](https://maven-badges.herokuapp.com/maven-central/com.mikepenz.aboutlibraries/library) [![Android Arsenal](http://img.shields.io/badge/Android%20Arsenal-AboutLibraries-brightgreen.svg?style=flat)](http://android-arsenal.com/details/1/102)

AboutLibraries is a library to offer you all the information you need of your libraries!

Most modern apps feature an "Used Library"-section and for this some information of those libs is required. As it gets annoying to copy those strings always to your app I've developed this small helper library to provide the required information.

######Note:
The description files should be included in the specific libraries (as far as possible) so the AboutLibraries library can take care about which libs to show. If a library contains the description file, the lib will auto-detect this file and will auto-show this library. You can find more details in the *Contribute* section of this README.


#Get started
- [Create new definition files](http://def-builder.mikepenz.com/)
- [Test the library in the sample](https://play.google.com/store/apps/details?id=com.mikepenz.aboutlibraries.sample)
- [Get detailed instructions in the wiki](https://github.com/mikepenz/AboutLibraries/wiki)
- [Want to see some images? Click here](https://github.com/mikepenz/AboutLibraries/wiki/Screenshots)
- [Everything clear. Here's a list of compatible/included libs](https://github.com/mikepenz/AboutLibraries/wiki/Compatible-Libs)


#Screenshots
![Image](https://raw.githubusercontent.com/mikepenz/AboutLibraries/master/DEV/screenshots/screenshot1_small.png)
![Image](https://raw.githubusercontent.com/mikepenz/AboutLibraries/master/DEV/screenshots/screenshot2_small.png)


#Wiki
You can find all required information (in a structured format) in the wiki.

[Bring me to the wiki](https://github.com/mikepenz/AboutLibraries/wiki)

You can also find [Screenshots](https://github.com/mikepenz/AboutLibraries/wiki/Screenshots) if you are interested in the autogenerated activity.

It contains a complete list of all supported libraries. Updated as soon as new libs are added.
Please let me know if you include the definition file in your library. Thanks.

[Here's a complete list](https://github.com/mikepenz/AboutLibraries/wiki/Compatible-Libs)


##Include in your project
###Using Maven
The AboutLibraries Library is pushed to [Maven Central](http://search.maven.org/#search|ga|1|g%3A%22com.mikepenz.aboutlibraries%22), so you just need to add the following dependency to your `build.gradle`. It seems it is also required to add the support dependencies to the application. If it works without, you should be fine too :).

```javascript
compile('com.mikepenz.aboutlibraries:library:4.4.0@aar') {
	transitive = true
}
```

Further information and how to use it if you can't update to the newest v21 support libs can be found in the [wiki](https://github.com/mikepenz/AboutLibraries/wiki/HOWTO:-Include)


##Usage
You can use this library in a few different ways. You can create your own activity, including a custom style and just use the information, or you can use the built-in Activity or Fragment and just pass the libs you would love to include.
###Activity / Fragment
####Fragment
```java
Bundle bundle = new Bundle();
//Pass the fields of your application to the lib so it can find all external lib information
bundle.putStringArray(Libs.BUNDLE_FIELDS, Libs.toStringArray(R.string.class.getFields()));
//Define the libs you want (only those which don't include the information, and are not autoDetected) 
//(OPTIONAL if all used libraries offer the information, or are autoDetected)
bundle.putStringArray(Libs.BUNDLE_LIBS, new String[] {
    "AndroidIconify", "ActiveAndroid", "FButton", "Crouton", "HoloGraphLibrary", 
    "ShowcaseView", "NineOldAndroids", "AndroidViewpagerIndicator"
});

//Display the library version (OPTIONAL)
bundle.putBoolean(Libs.BUNDLE_VERSION, true);
//Display the library license (OPTIONAL
bundle.putBoolean(Libs.BUNDLE_LICENSE, true);

//Create a new Fragment (you can do this where ever you want
Fragment fragment = new LibsFragment();
//Set the arguments
fragment.setArguments(bundle);
```
####Activity
#####Code:
```java
//Create an intent with context and the Activity class
Intent i = new Intent(getApplicationContext(), LibsActivity.class);
//Pass the fields of your application to the lib so it can find all external lib information
i.putExtra(Libs.BUNDLE_FIELDS, Libs.toStringArray(R.string.class.getFields()));
//Define the libs you want (only those which don't include the information, and are not autoDetected) 
//(OPTIONAL if all used libraries offer the information, or are autoDetected)
i.putExtra(Libs.BUNDLE_LIBS, new String[]{"crouton", "actionbarsherlock", "showcaseview"});

//Display the library version (OPTIONAL)
i.putExtra(Libs.BUNDLE_VERSION, true);
//Display the library license (OPTIONAL
i.putExtra(Libs.BUNDLE_LICENSE, true);

//Set a title (OPTIONAL)
i.putExtra(Libs.BUNDLE_TITLE, "Open Source");

//Pass your theme (OPTIONAL)
i.putExtra(Libs.BUNDLE_THEME, R.style.Theme_AppCompat);
//Pass a custom accent color (OPTIONAL)

//start the activity
startActivity(i);
```

###Custom
Use the `Library` class and build your view on your own

The preferred method to get a Libs instance is by passing the string-field-array
```java
Libs libs = new Libs(getActivity(), R.string.class.getFields());
```

Now you can use the instance to get the information
```java
libs.getLibrary("ActionBarSherlock")
```
done.


##Small extra
For those who read the whole README here's one more thing.
You can also use the AboutLibraries activity as an "about this app" screen. You ask how?
Yeah pretty simple just add the following .xml file (or just the strings - the key must be the same) to your project.

```xml
<resources>
    <string name="aboutLibraries_description_showIcon">true</string>
    <string name="aboutLibraries_description_showVersion">true</string>
    <string name="aboutLibraries_description_text">Place your description here :D</string>
</resources>
```
or
```java
i.putExtra(Libs.BUNDLE_APP_ABOUT_ICON, true);
i.putExtra(Libs.BUNDLE_APP_ABOUT_VERSION, true);
i.putExtra(Libs.BUNDLE_APP_ABOUT_DESCRIPTION, "Place your description here :D");

```


##Definition-File-Builder
For the lazy ones, I've created a small and hopefully useful tool to create definition files for new libs.

[Definition-File-Builder](http://def-builder.mikepenz.com/)


##Including in your library
Create a `{yourlib}_strings.xml` in your values folder and define the required information.

You can also find a sample in one of my other open source projects here: [LINK](https://github.com/mikepenz/AnimatedGridView/blob/master/library/src/main/res/values/info_strings.xml)

###Sample *_strings.xml (ActionBarSherlock)
```xml
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <!-- If you include it in your own library use this pattern: define_* -->
    <!-- If it should be included in the AboutLibraries lib use this pattern: define_int_* -->
    <string name="define_ActionBarSherlock"></string>
    <string name="library_ActionBarSherlock_author">Jake Wharton</string>
    <string name="library_ActionBarSherlock_authorWebsite">http://jakewharton.com/</string>
    <string name="library_ActionBarSherlock_libraryName">ActionBarSherlock</string>
    <string name="library_ActionBarSherlock_libraryDescription">ActionBarSherlock is an standalone library designed to facilitate the use of the action bar design pattern across all versions of Android through a single API.</string>
    <string name="library_ActionBarSherlock_libraryVersion">4.3.1</string>
    <string name="library_ActionBarSherlock_libraryWebsite">http://actionbarsherlock.com/</string>
    <!-- Possible values right now: apache_2_0, mit, bsd_2, bsd_3 -->
    <string name="library_ActionBarSherlock_licenseId">apache_2_0</string>
    <!-- you still can define the license within your library definition, but it is recommend to use the id -->
    <!-- possible fields for a custom license: *_licenseVersion, *_licenseLink, *_licenseContent -->
    <string name="library_ActionBarSherlock_isOpenSource">true</string>
    <string name="library_ActionBarSherlock_repositoryLink">https://github.com/JakeWharton/ActionBarSherlock</string>
</resources>
```


##Contribute
You can contribute by creating an information file for a new library, and open a pull-request at the creators Git repository. If he doesn't include the information file in his repo, or if the library isn't maintained anymore you can create a pull-request here.

Please note that if you make a pull-request here, that you have to change the `define_` string to `define_int_`. It is also very important that the `_strings.xml` has an unique filename (it should be named `{libraryidentifier}_strings.xml`.


##Already in use in following apps
(feel free to send me new projects)

* [Numbers](https://play.google.com/store/apps/details?id=com.tundem.numbersreloaded.free)
* [MegaYatzy](https://play.google.com/store/apps/details?id=com.tundem.yatzyTJ)



#Developed By

* Mike Penz - http://mikepenz.com - <mikepenz@gmail.com>


#License

    Copyright 2014 Mike Penz

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

       http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.
