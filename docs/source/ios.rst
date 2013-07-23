.. meta::
   :description: iOS A/B testing client setup

Arise iOS SDK
*****************

This documentation will help you to install the Arise iOS client in your application.

Installation steps
==================

1. Add the Arise library to your project
----------------------------------------

First, download the Arise SDK for iOS. Unzip it and drag and drag it inside your project's /libs/ folder. Ensure that you select ‘Copy items into the destination group’s folder’ when the dialogue box appears.

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

    #import <Arise/AriseAB.h>

Add the following line under application:didFinishLaunchingWithOptions of your AppDelegate.m file to initialize the framework:

.. code-block:: obj-c

    [Arise initializeWithKey:@"9c51b5e8f06ebd26728f29954365098f052c68c8"];

Replace the value of the key by your own key. You can find it in your dashboard.

4. Get the experiment value
---------------------------

You can request a variation value using the getVariation method in one of your .m file:

.. code-block:: obj-c

    [ABTest getVariation:^(NSString *experimentValue){
        upgradeButton.title = experimentValue;
    }];

Do not forget to include the Arise SDK in your header file:

.. code-block:: obj-c

    #import <Arise/AriseAB.h>


5. Record events
----------------

Now that you have setup your application for testing, you will need to record views and conversion events.
Record a view:

.. code-block:: obj-c

	[ABTest recordView];

Record a conversion:

.. code-block:: obj-c

	[ABTest recordConversion];


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

        // Create a button with a default value
        UIBarButtonItem *purchaseButton = [[UIBarButtonItem alloc] initWithTitle:@"Buy"
                                                                        style:UIBarButtonItemStyleBordered
                                                                       target:self
                                                                       action:@selector(login:)];

        self.navigationItem.rightBarButtonItem = purchaseButton;

        [ABTest getVariation:^(NSString *experimentValue){
            // Change the title of the purchase button
            purchaseButton.title = experimentValue;
        }];
    }

    - (void)onLoadPurchasePage
    {
        [ABTest recordView];
    }

    - (IBAction)onPurchase:(id)sender
    {
        // User clicked on the purchase button : count a successful experiment, or conversion.
        [ABTest recordConversion];
    }

    - (void)didReceiveMemoryWarning
    {
        [super didReceiveMemoryWarning];
        // Dispose of any resources that can be recreated.
    }

    - (IBAction)login:(id)sender
    {
        /**
         User pressed the button : count a successful experiment, or conversion.
         */
        [ABTest recordConversion];
    }

To run the test in the example you need to embed in the navigation controller to the project.
Select "Mainstoryboard.storyboard" > Editor > Embed In > Navigation Controller.

Notes
=====

The Arise iOS SDK supports iOS 6 and later.