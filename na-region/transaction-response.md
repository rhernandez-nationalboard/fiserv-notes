Link:
- https://developer.fiserv.com/product/IPGNA/docs/?path=docs/additionalInfo/TransactionResponse.md&branch=main

Response Fields
- Status:
	- approved
	- declined
	- failed: wrong transaction message content / parameters
	- waiting: asynchronous alternative payment methods
- `ipgTransactionId`: id assigned by gateway to be used in case of void
- `fail_reason`: reason the transaction failed