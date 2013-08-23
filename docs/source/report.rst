.. meta::
   :description: A/B tests reports and conversion rates

Understand your report
*************************


Overview
===============

Your experiment report is your tool to understand which variation was the most effective.

Views and conversions
=====================

A variation is assigned by the server as soon as you run the initialize function.
The system will add one view or one conversion to the report for each event. One user can record more than one view or conversions.

If the Arise client could not reach the server, the client will fallback on the default variation value and no events will be recorded (views or variations).

Examples
----------------

Example 1
+++++++++++++++++

+---------------------+---------------------+---------------------+
|                     |     Variation A     |     Variation B     |
+---------------------+---------------------+---------------------+
|        views        |         1290        |         1300        |
+---------------------+---------------------+---------------------+
|     conversions     |          130        |          340        |
+---------------------+---------------------+---------------------+
|  conversion rate    |          10%        |          26%        |
+---------------------+---------------------+---------------------+

This table means that:

* 1290 view events has been recorded for the the variation A
* 1300 view events has been recorded for the the variation B
* 130 conversion events has been recorded for the the variation A
* 340 conversion events has been recorded for the the variation B

The conversion rate is the total number of conversion events divided by the total number of view events.

Keep in mind that:

* one user might record multiple view events for the variation which has been assigned to him.
* one user might record multiple conversion events for the variation which has been assigned to him.

In this example, variation B was better than variation A.

Example 2
+++++++++++++++++

+---------------------+---------------------+---------------------+
|                     |     Variation A     |     Variation B     |
+---------------------+---------------------+---------------------+
|        views        |         2340        |         2251        |
+---------------------+---------------------+---------------------+
|     conversions     |         2100        |         3450        |
+---------------------+---------------------+---------------------+
|  conversion rate    |          89%        |          153%       |
+---------------------+---------------------+---------------------+

Seems like a bug in our system? No, it's a feature! This experiment could have been implemented in a very addictive game.

A screen is shown to the player when he has no more life (game over):

**Variation A**:

| Game over
| Buy more lives to continue
| [ 1 life ]
| [ 5 lives ]
| [ 25 lives ] 
  
**Variation B**:  
  
| You were soooooo closed to the final boss!
| Wanna refill? Lives are even better than energy drinks.
| [ 1 life ]
| [ 5 lives ]
| [ 25 lives ] 
  
| One view event is recorded when the screen is displayed.
| One conversion event is recorded **for each life** bought.
  
In this example, the results means that a player who loose purchases in average 0.89 life with the variation A and 1.53 lives with the variation B.
The revenue is higher with the variation B than with the variation A!

This is why in some cases we can have more conversion events than views! The goal here was to optimize the number of lives purchased.  
