### PAYable IPG SDK

Payable IPG SDK helps to integrate the payment gateway of your website.

<hr>

### Integration
First, You need to get the Merchant Key and Merchant Token to integrate with IPG SDK from Payable.

* Merchant Key: 
* Merchant Token:  

## Redirect to the Payable Payment Gateway
You can simply use an HTML Form to submit the below params to Payable Payment Gateway.When your customer click on payment/checkout button, It will be redirect to the Payable Payment Gateway. The Customer can confirm the payment by click on 'continue' button. Then your customer will be securely redirected to the commercial bank Payment Gateway and the customer can then enter the credentials (Card No / Cardholder name / CVV ) and process the payment there. Once the payment is made, The payable payment gateway will show the payment status to your customer and send the reciept to your customer's email. 

Payable Checkout URL:

```
Sandbox: https://sandboxipgsdk.payable.lk/sdk/v2/payable-checkout-sandbox.js
```
Required Form Parameters:

1. ```notify_url```
2. ```return_url```
3. cancel_url
4. merchant_key
5. custom_1
6. custom_2
7. currency_code
8. check_value
9. order_description
