### PAYable IPG SDK

Payable IPG SDK helps to integrate the payment gateway of your website.

<hr>

### Integration
First, You need to get the Merchant Key and Merchant Token to integrate with IPG SDK from Payable.

* Merchant Key: 
* Merchant Token:  

#### Redirect to the Payable Payment Gateway
You can simply use an HTML Form to submit the below params to Payable Payment Gateway.When your customer click on payment/checkout button, It will be redirect to the Payable Payment Gateway. The Customer can confirm the payment by click on 'continue' button. Then your customer will be securely redirected to the commercial bank Payment Gateway and the customer can then enter the credentials (Card No / Cardholder name / CVV ) and process the payment there. Once the payment is made, The payable payment gateway will show the payment status to your customer and send the reciept to your customer's email. 

Payable Checkout URL:

```
Sandbox: https://sandboxipgsdk.payable.lk/sdk/v2/payable-checkout-sandbox.js
```
Required Form Parameters:

1. ```notify_url```         - URL to callback the status of the payment (Needs to be a URL accessible on a public IP/domain)
2. ```return_url```         - URL to redirect users when success
3. ```cancel_url```         - URL to redirect users when cancelled
4. ```merchant_key```       - Payable Merchant ID [Given by PAYable]
5. ```currency_code```      - Currency Code (LKR/USD)
6. ```check_value```        - Generated hash value to ensure extra security
7. ```order_description```  - Small Description for the Order


5. ```custom_1``` - Merchant specific data, a Custom 1
6. ```custom_2``` - Merchant specific data, a Custom 2
