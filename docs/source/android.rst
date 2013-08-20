.. meta::
   :description: Android A/B testing client setup

Arise Android SDK
*****************

This documentation will help you to install the Arise Android client in your application.

Installation steps
==================

1. Add the Arise library to your project
----------------------------------------

First, download the `Arise library jar file`_ and drag it inside your project's /libs/ folder.

.. _`Arise library jar file`: https://s3.amazonaws.com/ariseio/Arise-Android-2.4.jar

2. Add permissions
-------------------

In your project, right click on AndroidManifest.xml Click on Open With/Android Common XML Editor. Add after the <uses-sdk .... /> tag:

.. code-block:: xml

    <uses-permission android:name="android.permission.INTERNET"></uses-permission>

3. Initialize the framework
---------------------------

In the onCreate function of your main activity, you need to initialize the framework:

.. code-block:: java

    // Initialize the arise library
    String authKey = "9c51b5e8f06ebd26728f29954365098f052c68c8";
    Arise.initialize(getApplicationContext(), authKey);

Replace the value of authKey by your own key. You can find it at the top of your dashboard.

4. Get the experiment value
---------------------------

When you plan to run the experiment, you will need to call the getVariationWithListener with the experiment name (same as the one displayed in your dashboard) to get the experiment data.
You have also to set a default value in case of no connection to the server. "Buy it now" is the default value in the following code snippet.

.. code-block:: java

    // Get and setup the variation
    ABTest.getVariationWithListener("Experiment1", "Buy it now", new VariationListener() {
    	@Override
    	public void onVariationAvailable(String value) {
    		final String buyMessage = value;
    	}
    });

The default value will only be printed if the application has never succeeded to connect to the server. We recommend to set the default value to the same value as your variation A value.

5. Record events
----------------

Now that you have setup your application for testing, you will need to record views and conversion events. You need to provide the experiment name as a parameter to associate the events with an experiment.

Record a view:

.. code-block:: java

	ABTest.recordView("Experiment1");

Record a conversion:

.. code-block:: java

	ABTest.recordConversion("Experiment1");

Views and conversions events are stored on the device until an internet connection is available. Our framework does work properly even in case of no connectivity.

Full code example
==================

.. code-block:: java

    package com.example.shoestore;

    import io.arise.ABTest;
    import io.arise.Arise;
    import io.arise.VariationListener;
    import android.os.Bundle;
    import android.app.Activity;

    public class MainActivity extends Activity {

    	@Override
    	protected void onCreate(Bundle savedInstanceState) {
    		super.onCreate(savedInstanceState);
    		setContentView(R.layout.activity_main);

    		// Initialize the arise library
    		String authKey = "9c51b5e8f06ebd26728f29954365098f052c68c8";
    		Arise.initialize(getApplicationContext(), authKey);

    		// Get and setup the variation
    		ABTest.getVariationWithListener("Experiment1", "Buy it now", new VariationListener() {
    			@Override
    			public void onVariationAvailable(String value) {
    				// Change the button label
    				final String buyMessage = value;
    				// Use the buyMessage to customize our application
    				// ...

    			}
    		});

    	}

    	private void onLoadPurchasePage(){
    		// the user is viewing the item purchase page
    		// record a view event
    		ABTest.recordView("Experiment1");
    	}

    	private void onPurchaseCompleted(){
    		// the user has bought the item
    		// record a conversion event
    		ABTest.recordConversion("Experiment1");
    	}
    }

Notes
=====

The Arise Android SDK supports Android 2.3.3 (API level 10) and later.
