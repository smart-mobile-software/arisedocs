.. meta::
   :description: Phonegap A/B testing client setup

Arise PhoneGap SDK
**********************

This documentation will help you to install the Arise PhoneGap SDK in your html5 application.

Installation steps
==================

1. Add the Arise PhoneGap plugin to your project
--------------------------------------------------

At the root of your project, run:

.. code-block:: bash

    phonegap local plugin add https://github.com/poiuytrez/ArisePhoneGap.git

The plugin will be automatically downloaded and installed in your application.
On an iOS project, you need to drag the ArisePhoneGap/libs/ios/Arise.framework folder inside your project’s Frameworks folder in XCode. Ensure that you select ‘Copy items into the destination group’s folder’ when the dialogue box appears.

2. Initialize the framework
---------------------------

You need to initialize the framework in the deviceReady function of your application:

.. code-block:: javascript

    // Initialize the arise library
    var authKey = "9c51b5e8f06ebd26728f29954365098f052c68c8";
    var appName = "AngryElephants";
    // arise.initialize(success, error, authKey, appName);
    arise.initialize(
        function(){ console.log("successfully initialized"); },
        function(error){ console.log("an error occured:" + error); },
        authKey,
        appName
    );

Replace the value of the key and the app name by your own key and your application name. You can find it on your dashboard. This function will trigger a asynchronous sync with the server (experiments values are retrieved and events are sent).

3. Get the experiment value
----------------------------

When you plan to run the experiment, you will need to call the getVariationWithListener with the experiment tag name (same as the one displayed in your dashboard) to get the experiment data.
You have also to set a default value in case of no connection to the server. "Buy it now" is the default value in the following code snippet.

.. code-block:: javascript

    // arise.getVariationWithListener(success, error, experimentTag, defaultValue);
    arise.getVariationWithListener(
        function(value){
            // print the variation
            console.log(value);
        },
        function(error){
            console.log("an error occured:" + error);
        },
        "ExpTag1",
        "MyDefaultValue"
    );

The default value will only be printed if the application has never succeeded to connect to the server. We recommend to set the default value to the same value as your variation A value.

We also recommend to call this function as late as possible in your app.

4. Record events
----------------

Now that you have setup your application for testing, you will need to record views and conversion events. You need to provide the experiment tag name as a parameter to associate the events with an experiment.

Record a view:

.. code-block:: javascript

	// arise.recordView(success, error, experimentTag);
	arise.recordView(
	    function(){ console.log("success")},
	    function(error){ console.log("an error occured:" + error) },
	    "ExpTag1"
	);

Record a conversion:

.. code-block:: javascript

    // arise.recordConversion(success, error, experimentTag);
    arise.recordConversion(
        function(){ console.log("success")},
        function(error){ console.log("an error occured:" + error) },
        "ExpTag1"
    );

Views and conversions events are stored on the device until an internet connection is available. Our framework does work properly even in case of no connectivity.

Full code example
==================

.. code-block:: html

    <!DOCTYPE html>
    <html>
    <head>
        <script>
            // Click on Initialize button
            function initialize(){
                // Initialize Arise
                // Initialize the arise library
                var authKey = "9c51b5e8f06ebd26728f29954365098f052c68c8";
                var appName = "AngryElephants";
                // arise.initialize(success, error, authKey, appName);
                arise.initialize(
                        function(){ console.log("successfully initialized"); },
                        function(error){ console.log("an error occured:" + error); },
                        authKey,
                        appName
                );
            }

            // Click on GetVariation button
            function getVariation(){
                // arise.getVariationWithListener(success, error, experimentTag, defaultValue);
                arise.getVariationWithListener(
                        function(value){
                            // print the variation
                            alert(value);
                        },
                        function(error){
                            console.log("an error occured:" + error);
                        },
                        "ExpTag1",
                        "MyDefaultValue"
                );
            }

            // Click on Record View button
            function recordView(){
                // arise.recordView(success, error, experimentTag);
                arise.recordView(
                        function(){ console.log("success")},
                        function(error){ console.log("an error occured:" + error) },
                        "ExpTag1"
                );
            }

            // Click on Record Variation button
            function recordConversion(){
                // arise.recordConversion(success, error, experimentTag);
                arise.recordConversion(
                        function(){ console.log("success")},
                        function(error){ console.log("an error occured:" + error) },
                        "ExpTag1"
                );
            }
        </script>
    </head>
    <body>
    <button onclick='initialize()'>Initialize</button>
    <button onclick='getVariation()'>Get variation</button>
    <button onclick='recordView()'>Record view</button>
    <button onclick='recordConversion()'>Record conversion</button>

    <script type="text/javascript" src="phonegap.js"></script>

    </body>
    </html>




Notes
=====

The Arise PhoneGap SDK supports PhoneGap 3.X on Android and iOS.
