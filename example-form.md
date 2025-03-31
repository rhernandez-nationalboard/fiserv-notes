Form
``` typescript
  <form method="post" action="https://test.ipg-online.com/connect/gateway/processing">
    <input type="hidden" name="chargetotal" value={paymentProcessorRequest.chargeTotal} />
    <input type="hidden" name="checkoutoption" value="combinedpage" />
    <input type="hidden" name="currency" value={paymentProcessorRequest.currency}/>
    <input type="hidden" name="hash_algorithm" value="HMACSHA256" />
    <input type="hidden" name="paymentMethod" value={paymentProcessorRequest.paymentMethod}/>
    <input type="hidden" name="responseFailURL" value={paymentProcessorRequest.responseFailedURL} />
    <input type="hidden" name="responseSuccessURL" value={paymentProcessorRequest.responseSuccessURL} />
    <input type="hidden" name="storename" value={paymentProcessorRequest.storeName} />
    <input type="hidden" name="timezone" value={paymentProcessorRequest.timezone}/>
    <input type="hidden" name="transactionNotificationURL" value={paymentProcessorRequest.transactionNotificationUrl} />
    <input type="hidden" name="txndatetime" value={paymentProcessorRequest.txnDateTime}/>
    <input type="hidden" name="txntype" value={paymentProcessorRequest.txnType}/>
    <input type="hidden" name="hashExtended" value={createExtendedHash(paymentProcessorRequest)} />
    <input type="submit" value="Submit" />
  </form>
```

Hash Function
``` typescript
    const stringToExtendedHash = [
      request.chargeTotal,
      'combinedpage',
      request.currency,
      'HMACSHA256',
      request.paymentMethod,
      request.responseFailedURL,
      request.responseSuccessURL,
      request.storeName,
      request.timezone,
      request.transactionNotificationUrl,
      request.txnDateTime,
      request.txnType,
    ].join('|');
    console.log(stringToExtendedHash);
    const hashString = HmacSHA256(stringToExtendedHash, request.sharedSecret);
    const encodedHashString = CryptoJS.enc.Base64.stringify(hashString);
    console.log(encodedHashString);
    return encodedHashString;
```