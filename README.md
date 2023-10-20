# jaago_volunteer

A new Flutter project.

Flutter scalable folder & files structure
=========================================

I built two application in flutter and one application which I am currently working has started 7 months ago and it still growing. If we want to build a single codebase native performance mobile application for Android and iOS then Flutter is the best choice.

In this article, We will be covering how to structure our large scale application which we have decided to build with Flutter.

When we create the Flutter project then by default only this folder and files are present (see below).

![](https://miro.medium.com/max/602/1*pUJ4v5oZlBLwShuqIaUVTQ.jpeg)

Default flutter app folder and files structure

Almost all the code we need to write inside the lib folder and we can see that by default Flutter doesn’t provide any file structure only the main.dart file with one stateful widget is present to run the sample counter.

Now, we will see what folders and files we need to create so that the application will be scalable.

Adding Assets
=============

First, we will create an **assets** folder in the root of the project which we will use to store images, translation files, custom font files, HTML files.

**assets** folder contains the following folders:

1.  **fonts:** This folder should have all the font files i.e custom fonts which are used in the application (.ttf files)
2.  **html:** If our application needs to open some HTML content which we need to add in our mobile app (Generally the licensed content of the application or any .html files which we need to load in the application using the package: [webview_flutter](https://pub.dev/packages/webview_flutter) or [flutter_html](https://pub.dev/packages/flutter_html))  
    _Note: Generally_ [_webview_flutter_](https://pub.dev/packages/webview_flutter) _is used to load the URL of any web content but we can use this plugin for showing the HTML content which is stored locally in the mobile application. I will prepare a separate article explaining how to show local HTML files in flutter and will add the link here when completed._
3.  **i18n:** If our application supports Internationalization then need to add .json files for all the supporting different languages i.e If we need to support English and French then need to add _en.json_ and _fr.json_ in this folder. we can find more information on this link [internationalizing flutter using JSON files](/flutter-community/flutter-internationalization-the-easy-way-using-provider-and-json-c47caa4212b2)
4.  **images:** This is the most important folder where we store all our images.

Here is actually how the **assets** folder looks like:

![assets folder structure](https://miro.medium.com/max/590/1*qKfQOPjmSE2IYbSBlF71zQ.jpeg)

This is how the assets folder looks

After creating the assets folder we need to add all the assets path in _pubspec.yaml_ file so that flutter recognizes where the assets are present.

Here is how the assets path is added to _pubspec.yaml_ file

![Add application assets path in pubspec.yaml file](https://miro.medium.com/max/1400/1*Nlh92HH6vyUKO2Pn4jDYGg.jpeg)

This is how application assets path are added in pubspec.yaml

**Adding the config folder**
============================

Now, we will be adding the **config** folder inside the **lib** folder

**config** folder contains the following folders:

1.  **routes:** The route folder contains all the files which are based on the application screens navigation code. We will be using the package [fluro](https://pub.dev/packages/fluro) to separate our route navigation. This folder contains three files: _routes.dart, routes\_config.dart, routes\_handler.dart. we_ can see the [fluro](https://pub.dev/packages/fluro) package example code to know about each of these files. Later I will create a separate article for explaining how to use [fluro](https://pub.dev/packages/fluro) for route navigation in flutter and will add the link for the same here.
2.  **themes:** If our application supports _light_ and _dark_ theme and these themes are custom themes then need to create two files _light_theme.dart_, _dark_theme.dart_ where we will be adding all the colors which are needed for each widget type. One more file we will be creating _theme_config.dart_ which describes all the constants related to the theme.  
[flutter theam Doc](https://api.flutter.dev/flutter/material/ThemeData-class.html)
[flutter theam vid](https://www.youtube.com/watch?v=9iQiVUmLXyI)

    _Note: As this article is based on folder & files structure we will be describing what actually all the themes files contains and how it works in a separate document which I will prepare soon. For now, you can check this link to_ [_build multiple theme support using Bloc_](https://resocoder.com/2019/08/09/switch-themes-with-flutter-bloc-dynamic-theming-tutorial-dark-light-theme/)

Here is how the **config** folder looks like:

![Config folder and all the files related to config](https://miro.medium.com/max/586/1*Rq_viTks0Nj3fe0mMfhTEQ.jpeg)

config folder & file structure

Adding Constants
================

Here are the following constants which are static throughout the applications

1.  **api_path.dart:** When using REST API service in dart then we can store all the API endpoints in a separate file _api_path.dart_
2.  **assest_path.dart:** Although we have described the assets path in _pubspec.yaml_ but to use that asset in an application we need to give there relative path in any widgets.  
    If we add all the assets relative path in one file then it will be easy for us to get all the paths and update the path if required in the future.
3.  **app_constants.dart:** This is where all our application constants will be present and this is different for each application.

Here is how the **constants** folder looks like:

![App Constants folder & files structure](https://miro.medium.com/max/602/1*2wDOea3DEuEYkSrZVBXNSw.jpeg)

App Constant folder & file structure

Adding Custom Widgets
=====================

In a large scale application, we need to make more customized widgets rather than flutter default widgets. Suppose we need to make use of our own custom RaisedButton, FlatButton, OutlineButton, Divider, CircularLoader, etc which we can use throughout our application then that kind of customization widgets we can add inside the file _widget.dart_ which will be present inside the folder **widgets**

Here is how the **widgets** folder looks like:

![widget folder](https://miro.medium.com/max/576/1*T2KpWRJgxiDM2MRqampW2A.jpeg)

widget folder for adding custom widgets

**Adding Utils**
================

**Utils** folder contains the _helpers, services, UI utils, mixins_ which are used throughout the application

**Exploring Helpers  
**In many scenarios, we need to write code multiple times for the same thing like converting the every word first characters to be uppercase usually used in showing titles for any other widgets, etc. This kind of code can be made common to reduce the redundancy and add that code in helpers files which are present in _lib/utils/helpers/text_helper.dart.  
text_helper.dart_ will contain all the code which are required to convert the String to show in a Text widget.

**Exploring Services  
**We will be creating a different kind of service files in the folder _lib/utils/services  
_**_Note:_** _All the services will be singleton classes._

1.  **local\_storage\_service.dart:** In this file, we write all the code needed to _store_ and _get_ data from the local storage using the plugin [shared_preferences](https://pub.dev/packages/shared_preferences).  
    In this file, there will be getters and setters for each and every data to be stored in the local storage.
2.  **secure\_storage\_service.dart:** We do not store user credentials, API tokens, secret API keys in local storage, for that we make use of [flutter\_secure\_storage](https://pub.dev/packages/flutter_secure_storage) which stores data in the Android Keystore and Apple keychain with platform-specific encryption technique.  
    In this file, there will be getters and setters for each and every data to be stored in platform secure storage.
3.  **rest\_api\_service.dart:** We do call the rest API to get, store data on a remote database for that we need to write the rest API call at a single place and need to return the data if the rest call is a success or need to return custom error exception on the basis of 4xx, 5xx status code. We can make use of [http](https://pub.dev/packages/http) package to make the rest API call in the flutter
4.  **native\_api\_service.dart:** We use multiple packages to access the native services like Camera, Photo Gallery, Location, etc for that we need to write code in a separate file which we can be used from multiple places throughout the application

**Exploring UI Utils  
**All the common UI related things should be present inside _lib/utils/ui_ folder  
Here is the list of folders and files which will be present in the directory _lib/utils/ui_

1.  **animations:** All the custom animations will be present in this file with separate files like _slide\_fade\_transition.dart, impulse_animation.dart,_ etc this all custom animations will be used through the application.
2.  **app_dialogs.dart:** All the custom app dialogs UI will be present in this file.
3.  **ui_utils.dart:** All the custom UI widgets like an input text box with search icon, autocomplete widgets, Error message banners, custom checkbox chips related utils can be present in this file and will be used thoughout the application.

**Exploring Mixins  
Mixin** is a class that contains methods for use by other classes without having to be the parent class of those other classes.” In other words, **mixins** are normal classes from which we can borrow methods(or variables) from without extending the class.  
In the application, we can make different mixins like validation\_mixins.dart, orientation\_mixins.dart

Here is how the **utils** folder looks like:

![utils folder and files](https://miro.medium.com/max/594/1*X3v6ZNBKDpIC1Z-HleL0yw.jpeg)

App utils folder & file structure

**Adding Core Features**
========================

Core features like Login/auth, walkthrough screens (Screens which are only visible at after the install only), application setting features are the core features that should be added in a folder **Core**.

1.  **auth**: Auth folder must contain the features: Register, Login, Forgot password.
2.  **walk_through:** Walkthrough  screens must contain all the screens which will be visible only when the application starts for the first time after the fresh install.
3.  **settings:** This will be the application setting feature

Here is how the **core** folders and files look like:

![core features folders and files structure](https://miro.medium.com/max/556/1*DA5Ov_9r0Sw24FLwQb5ejA.jpeg)

Core features folder and file structure

Adding Application Modules
==========================

Before proceeding with **modules,** I would like to show how each and every module is implemented. i.e each and every module and core features which we discussed above are based on the **Bloc** pattern which we can find more in this package [flutter_bloc](https://pub.dev/packages/flutter_bloc).

**Bloc** design pattern helps to separate _presentation_ from _business logic_. Following the **Bloc** pattern facilitates testability and reusability. This package abstracts reactive aspects of the pattern allowing developers to focus on writing the business logic.

Let's take the example with module **dashboard** in the application which contains the following folders:

1.  **bloc:** This folder contains the three files _dashboard\_bloc.dart, dashboard\_events.dart, dashboard_states.dart._ I will create a separate document describing the bloc pattern and how to incorporate it into the flutter application. For now, you can understand the bloc pattern from [flutter_bloc](https://pub.dev/packages/flutter_bloc).
2.  **models**: This folder contains the data models which need to be shown on the dashboard screen.
3.  **repositories:** This folder contains the repository files which is used to write code for services call and for computation works.
4.  **screens:** This folder consists of all the screens UI widgets that will be visible to the user.

**Note**: All the modules and core features should contain these four folders to separate out the business logic from the UI.

Here is how the module **dashboard** looks like:

![Modules folder and file structures](https://miro.medium.com/max/564/1*UJoIjb9bfP8iQIdOkLPYHg.jpeg)

Modules folders and files structure

Complete Look of all the folder structure for a scalable application
====================================================================

![Complete scalable flutter app folder and file structure](https://miro.medium.com/max/576/1*zDzyL82bMpMMx7lBiDh57Q.jpeg)

Complete Folder and File structure for a scalable application

Hope! you get how to make use of this folder & file architecture for large scale applications.

I will be continually adding more articles regarding managing different custom themes, Bloc Design pattern following the DDD approach, Internationalization in Flutter.

Thank you

# jaago_volunteer
