.. meta::
   :description: What happens since the previous version of Arise?

Release notes
*****************

Version 2.6.1
==================

Html5
------

* Added compatibility with PhoneGap 3.0.0 for Android.

Version 2.6
==================
August 30th 2013

Backward compatible with iOS and Android Arise SDK version 2.5.

Dashboard
----------

* Adding support experiments tags. Mobile apps will the this tag to refer to the experiment instead of the experiment name. It means that you can run a new experiment with new values without resubmitting your app to the store.
* Other experiments are automatically collapsed when a new one is created
* Fix issue with empty distribution value

iOS
----

* Support for experiment tags
* AFNetworking library renamed to avoid conflicts with an existing library

Android
--------

* Support for experiment tags

Migration notes from 2.5 to 2.6
--------------------------------
SDK 2.5 will still work with experiments names. To use experiment tags:

1. Update your SDK
2. Replace your experiments names with experiments tags names in your source code

Version 2.5
==================
August 27th 2013

Dashboard
----------

* Adding support for multiple applications. Each application will be able to contain an unlimited number of experiments
* Experiments collapsible status are now saved
* One step registration
* Migration of existing Arise version 1.0 users

iOS
----

* Experiment values are now returned instantly if the system has not retrieved any values from the server. We had a 5 seconds waiting time on the previous version
* Support for application names on initialization

Android
--------

* Experiment values are now returned instantly if the system has not retrieved any values from the server. We had a 5 seconds waiting time on the previous version
* Support for application names on initialization

Version 2.4
==================
August 22th 2013

Dashboard
----------

* Adding support up to 8 variations per experiment (A/B/N testing)
* Stunning performances (no page reload)

iOS
----

* A default value can be defined
* Multiple variations support
* Platform support lowered form iOS 6.0 and up to iOS 5.0 and up.

Android
--------

* A default value can be defined
* Multiple variations support

Version 2.3
==================
August 6th 2013

Dashboard
----------

* Multiple experiments support
* Experiment status (draft, active, archived)
* Experiments info and report merged on the same page

iOS
----

* Better getVariation callback handling (works even at the first launch of the app)
* Less http requests (the registration with the server is now cached)
* Multiple experiments support

Android
--------

* Less http requests (the registration with the server is now cached)
* Multiple experiments support

Version 2.2
==================
July 28th 2013

First release of the new Arise platform (2.x). Versions 2.0 and 2.1 were never released to the public.
