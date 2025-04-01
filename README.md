# Overview
The hosted page solution allows us to open up a page that is managed by Fiserv.Generally the steps to process a payment are the following:
- Open fiserv hosted page
  - Submit a post action with hidden input parameters to open page
- User enters information into payment page
- User submits payment page and then is either taken to a success or failure result page

# Success / Failure
We can either specify the page that the is navigated to by specifying them in the post parameters or we can allow Fiserv to take the user to a generic page. In addition to this we can enable server to server notifications to update the status of an order.

### Warning
- In order to take the user to a success or failure page we must be able to respond to a post request. I believe in this case we wouldn't be able to use our current static site deployment and would thus need something like nextjs.
- The notifications service does not appear to be available for integration testing. So would need to set something up in this place in order for qa to test our built up solution 
- The notification service is just a dump api location we provide where we receive a post to update the status of an order

# Recommendations and Next Steps
In order to avoid restructuring our static site solution I believe we should leverage the notification service and rely on the default success and failure pages. This is the general outline of what I believe our solution should be:
- Our static site navigates to a checkout page
- We have some sort of checkout entity with an id that we can reference
- User clicks 'pay' on our checkout page which then opens the fiserv payment portal
  - Note: we will pass the checkout id as an order id to the payment portal and include the url for our notification service
- User will enter payment information and complete transaction
- User is taken to a success or failure page provided by fiserv which they can exit out
- Fiserv will post the status update to our notification url. This will allow us to update the order status
- On our checkout page we will pull periodically for the status of our order on our own api
- If we have a failure status we will let the user try to submit payment again
- If we have a success status we will do something else

### Notification Service Setup
Our notification service will just be a couple of dumb api end points to:
- Update the status of an order, this is what fiserv will post to
- Submit an order so that we can generate an id to hand over to fiserv
- Poll order status

For QA testing it might be helpful to provide the following:
- A page that shows pending orders
- Ability to approve a pending order manually 
- Ability to decline a pending order manually
- Periodic job that simulates a post into our update order api in order simulate fiserv request

# Documentation
It looks like there are two main sources of documentation which over the same api. The main difference is that one is regional. I recommend referencing that one but some times we need to use both.
- Original source: https://docs.fiserv.dev/public/docs/introduction
- Regional source: https://developer.fiserv.com/product/IPGNA/docs/?path=/docs/additionalInfo/HostedPaymentPages.md&branch=main&gettingStarted=true


