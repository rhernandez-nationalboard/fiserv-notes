### Steps
- Create a checkout form where submitting form should submit an html form to `fiserv gateway`. This is how we open the hosted payment gateway. We will provide a success, failure URL, and notification URL to this page.
	- Note: the notification URL is a server to server notification system to keep our system in sync with the status of a transaction.
- User enters information on hosted payment page and submits payment
- The gateway will use our provided URLs to send us back the results

### Step 1
- Implement html form to post to their gateway URL.
- Store name and shared secret will be required to post html form
	- Test values are: `10123456789` and `sharedsecret`
	- URL for test transactions `https://test.ipg-online.com/connect/gateway/processing`
- Include all required parameters specified here
	- URL: https://developer.fiserv.com/product/IPGNA/docs/?path=/docs/additionalInfo/HostedPaymentPages.md&branch=main&gettingStarted=true
	- `currency`: 840 for US
- Include hidden security has named `hasExtended`
	- URL: https://developer.fiserv.com/product/IPGNA/docs/?path=docs/additionalInfo/HowToGenerateHash.md&branch=main
	- Need to be calculated using all non-empty specified request parameters in ascending order of parameter names.
	- Shared secret key is used as the key to has the value
