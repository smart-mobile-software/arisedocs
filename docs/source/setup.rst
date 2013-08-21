.. meta::
   :description: First A/B test setup

Setup your first A/B test
*************************


Overview
===============

What is A/B testing?
---------------------
Testing is a way of showing users different variations of your app, and then measuring how each variation affects your goals.  For example, if you're interested in having your users make more in-app purchases, you might test the phrase "buy more coins now!" versus "save time by buying coins".  Arise's A/B testing tools can tell you which one will make you more money. You can also use Arise to test new in app-features, evaluate performance and roll out changes without resubmitting your app.

What is a conversion?
----------------------
Tests are only good when they can measure some metric and show you which path is performing better.  To help out our system, that metric should be a "conversion". Good examples of goals are things like an in-app purchase, a new account created, or even a tap on an advertisement. We can then calculate the `conversion rate`_ (Number of conversion/ Number of views).

.. _`conversion rate`: http://en.wikipedia.org/wiki/Conversion_rate


Getting Started
===============

1. Create an account
--------------------

If you do not have an account yet, register on the dashboard_. The dashboard is your tool to configure your experiments.

.. _dashboard: http://beta.arise.io/


2. Create and configure your variation
---------------------------------------

Click on "Create a new experiment" to create your first experiment.

Two variations are created by default: variation A (original) and variation B (test).

Variation values
+++++++++++++++++

Variation values will be transmitted to your app. You can experiment:

* call to actions
* headline, product descriptions (words, style, number of words)
* in-app purchases (prices, multiple contents)
* forms (types of fields, length, layout, error handling)
* layout and design (position and grouping of content)
* images

You need to set different values for each variation. We will consider the variation A as the default variation (original).
You will be able to create up to 8 variations. You can create a new variation by clicking on the blue '+' button. However, you will get more reliable and faster results by testing as few variations as possible.

Distribution
++++++++++++

You can set the distribution of your variations. The total of all the variations must always be 100%. You can for example set 70% on the variation A (original) and 30% on the variation B (test). Once your app is deployed, you will be able to view the conversion rate for each variation.

3. Start your experiment
---------------------------

Once you have configured your experiment, you will need to click on the "Start experiment" button. Once an experiment is started, experiment values are not allowed to be modified. You will also not be able to add or remove a variation. However, the distribution can still be modified. Requests from new devices will use the new distribution. Devices that have already an experiment assigned won't change.

4. Install the Arise SDK in your app
-------------------------------------

We currently support iOS and Android. Please read the following documentation to install the Arise SDK in your app:

* :doc:`ios`
* :doc:`android`


5. End your experiment
-----------------------

Once you have significant results for an experiment, you have the choice between keeping the variation A (original) or using a test variation (B,C,etc.). All the devices will display the selected variation when you validate your choice.
