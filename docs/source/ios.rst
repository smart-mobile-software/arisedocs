.. meta::
   :description: iOS A/B testing client setup

Arise iOS SDK
*****************

This document will help you to install the Arise iOS client in your application.

Installation steps
==================

1. Add the Arise library to your project
----------------------------------------

First, download the `Arise SDK for iOS`_. Unzip it and drag it inside your project's Frameworks folder in XCode. Ensure that you select ‘Copy items into the destination group’s folder’ when the dialogue box appears.

.. _`Arise SDK for iOS`: https://s3.amazonaws.com/ariseio/Arise-iOS-2.5.zip

2. Add dependencies
-------------------
In XCode:

* select your project in the project navigator
* in the project settings select your target
* click on the Build Phases tab
* Open the Link With Libraries collapsible panel
* Click on '+'
*  Search for libsqlite3.dylib and click on the Add button.


3. Initialize the framework
---------------------------

Add the following line in your AppDelegate.h:

.. code-block:: obj-c

    #import <Arise/Arise.h>

Add the following line under application:didFinishLaunchingWithOptions of your AppDelegate.m file to initialize the framework:

.. code-block:: obj-c

    [Arise initializeWithKey:@"9c51b5e8f06ebd26728f29954365098f052c68c8" appName:@"MyApp"];

Replace the value of the key and the app name by your own key and your application name. You can find it on your dashboard.

4. Get the experiment value
---------------------------

You can request a variation value using the getVariation: method with the experiment name (same as the one displayed in your dashboard).
You have also to set a default value in case of no connection to the server. "Buy it now" is the default value in the following code snippet.

.. code-block:: obj-c

    [ABTest getVariation:@"Experiment1" defaultValue:@"Buy it now" data:^(NSString *value){
        [_purchaseButton setTitle:value forState:UIControlStateNormal];
    }];

Do not forget to import the Arise SDK in your header file:

.. code-block:: obj-c

    #import <Arise/Arise.h>

The default value will only be printed if the application has never succeeded to connect to the server. We recommend to set the default value to the same value as your variation A value.

5. Record events
----------------

Now that you have setup your application for testing, you will need to record views and conversion events. You need to provide the experiment name as a parameter to associate the events with an experiment.

Record a view:

.. code-block:: obj-c

	[ABTest recordView:@"Experiment1"];

Record a conversion:

.. code-block:: obj-c

	[ABTest recordConversion:@"Experiment1"];

Views and conversions events are stored on the device until an internet connection is available. Our framework does work properly even in case of no connectivity.

Full code example
==================

.. code-block:: obj-c

    #import "ViewController.h"

    @interface ViewController ()

    @end

    @implementation ViewController

    - (void)viewDidLoad
    {
        [super viewDidLoad];

        // Get and setup the variation
        [ABTest getVariation:@"Experiment1" defaultValue:@"Buy it now" data:^(NSString *value){
            // Use the variation value to customize our application
            // ...
            
            // For example :
            // Change the title of the purchase button
            [_purchaseButton setTitle:value forState:UIControlStateNormal];
        }];
    }

    - (void)onLoadPurchasePage
    {
    	// the user is viewing the item purchase page
        // record a view event
        [ABTest recordView:@"Experiment1"];
    }

    - (IBAction)onPurchase:(id)sender
    {
        // the user has bought the item
        // record a conversion event
        [ABTest recordConversion:@"Experiment1"];
    }

    - (void)didReceiveMemoryWarning
    {
        [super didReceiveMemoryWarning];
        // Dispose of any resources that can be recreated.
    }

Notes
=====

The Arise iOS SDK supports iOS 5.0 and later.
