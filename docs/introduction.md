---
tags: [00. Welcome]
---
<div style="text-align:center;margin:auto;"><img style="float: right;" src="https://i.imgur.com/1ftCIDg.png" width=250px></div>



<h1>Rotender Partner API</h1>

Welcome to the Rotender Partner API. The purpose of this API is to allow Rotender partners to perform a number of functions to serve customers, including:
1. Displaying a menu of Drinks that are in stock and offered by Rotender.
2. Accurately tracking the inventory across Rotender Units so that out of stock Drinks are never sold.
3. After payment is processed, forwarding the Order to Rotender for fulfillment.
4. Directing the Customer to the Rotender when the Order is received.

<h1 style="margin-top:30px">Workflow</h1>

The following describes the workflow and API interactions in the use case where the Rotender Partner has a customer-facing app which handles Menu Display, Ordering and Payment Processing:

1. Customer opens Partner app, which [requests a drink menu](https://rotender.stoplight.io/docs/rotender-partner-docs/reference/Rotender%20Partner%20API/models/openapi.v1.yaml/paths/~1venues~1%7BvenueId%7D/get) from Rotender with a "venue ID".
2. Customer Browses the Rotender's menu as rendered by Partner App (either standalone or in line with drink options from a traditional bar).
3. User selects a Drink, and upon payment, Partner app submits a POST request to Rotender's Orders resource as documented [here](https://rotender.stoplight.io/docs/rotender-partner-docs/reference/Rotender%20Partner%20API/models/openapi.v1.yaml/paths/~1venues~1%7BvenueId%7D~1orders/post).
4. Rotender sends a response confirming the Drink has been added to our system. The Partner App then instructs the user to walk up to the Rotender to get their drink.
5. Customer walks to the Rotender and sees a 4 digit code on the Rotender's screen. Its purpose is to prove that a given customer is physically present and at the device. The 4 digit confirmation is then entered into the Partner's app, and the partner app [updates the Order record](https://rotender.stoplight.io/docs/rotender-partner-docs/reference/Rotender%20Partner%20API/models/openapi.v1.yaml/paths/~1venues~1%7BvenueId%7D~1orders/put) with a "ready" status. The Rotender device then pours the specified Order for the Customer.