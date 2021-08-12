### PAYable IPG SDK

Payable IPG SDK helps to integrate the payment gateway of your website.

<hr>

### Integration

First, You need to get the Merchant Key and Merchant Token to integrate with IPG SDK from Payable.

- Merchant Key:
- Merchant Token:

### Version V1.0.2.1
#### The Payable Payment Gateway 

You can simply use an HTML Form to submit the below params to Payable Payment Gateway.When your customer click on payment/checkout button, It will be redirect to the Payable Payment Gateway. The Customer can confirm the payment by click on 'continue' button. Then your customer will be securely redirected to the commercial bank Payment Gateway and the customer can then enter the credentials (Card No / Cardholder name / CVV ) and process the payment there. Once the payment is made, The payable payment gateway will show the payment status to your customer and send the reciept to your customer's email.

Payable Checkout URL:

```
Sandbox: https://sandboxipgsdk.payable.lk/sdk/v2/payable-checkout-sandbox.js
```

Required Form Parameters:

- `notify_url` - URL to callback the status of the payment (Needs to be a URL accessible on a public IP/domain)
- `return_url` - URL to redirect users when success
- `cancel_url` - URL to redirect users when cancelled
- `merchant_key` - Payable Merchant ID [Given by PAYable]
- `currency_code` - Currency Code (LKR)
- `check_value` - Generated hash value to ensure extra security
- `order_description` - Small Description for the Order
- `amount` - Total Payment Amount
- `invoice_id` - Invoice ID generated by the merchant
- `customer_first_name`- Customer’s First Name
- `customer_last_name` - Customer’s Last Name
- `customer_mobile_phone`- Customer’s Mobile No
- `customer_phone` - Customer’s Phone No
- `customer_email` - Customer’s Email
- `billing_address_street` - Billing Address Line1
- `billing_address_city`- Billing City
- `billing_address_province` - Billing Province
- `billing_address_country` - Billing Country (LKA)
- `billing_address_postcode` - Billing Postal Code

Optional Form Parameters:

- `custom_1` - Merchant specific data, a Custom 1
- `custom_2` - Merchant specific data, a Custom 2
- `billing_address_street2` - Billing Address Line2
- `billing_address_company` - Billing Company
- `shipping_contact_first_name` - Shipping Contact First Name
- `shipping_contact_last_name` - Shipping Contact Last Name
- `shipping_contact_mobile` - Shipping Contact Mobile No
- `shipping_contact_phone ` - Shipping Contact Phone No
- `shipping_contact_email` - Shipping Contact Email
- `shipping_address_company` - Shipping Contact Company
- `shipping_address_street` - Shipping Address Line1
- `shipping_address_street2` - Shipping Address Line2
- `shipping_address_city` - Shipping City
- `shipping_address_province` - Shipping Province
- `shipping_address_country` - Shipping Country (LKA)
- `shipping_address_postcode` - Shipping Postal Code

In Request, `check_value` is a combination of merchantKey, invoiceId, amount, currency parameter set in a predefined sequence given by PAYable which then encrypted with merchantToken (a unique Secret value for the Merchant which was shared by PAYable) using SHA-512.

Format:

`UPPERCASE(SHA512[<merchant_key>|<invoice_id>|<amount>|<currency_code>|UPPERCASE(SHA512[<merchant_Token>])])`

##### Sample HTML Form Code

```
   <html>
     <head>
      <title>ABC Fashion</title>
      <script src="https://sandboxipgsdk.payable.lk/sdk/v2/payable-checkout-sandbox.js"></script>
      </head>
    <body>
    <form method="post">
        <input type="hidden" name="notify_url" value="https://yoursite.com/payment/nortify" />
        <input type="hidden" name="return_url" value="https://yoursite.com/payment/return" />
        <input type="hidden" name="cancel_url" value="https://yoursite.com/payment/cancel" />
        <input type="hidden" name="merchant_key" id="merchant_key" value="D75XXXXXXXXX" />
        <input type="hidden" name="check_value" id="check_value" value="A8907A75XXXXXXXXXXXXXXXXXXX" />

        <h3>Payment Details</h3>
        <input type="text" name="invoice_id" id="invoice_id" value="INV0002301">
        <input type="text" name="order_description" id="order_description" value="Payment for abc Fashion">
        <input type="text" name="amount" id="amount" value="999.12" />
        <input type="hidden" name="currency_code" id="currency_code" value="LKR" />

        <h3>Customer Details</h3>
        <input type="text" id="customer_first_name" name="customer_first_name" value="Shakthi" />
        <input type="text" id="customer_last_name" name="customer_last_name" value="Elon" />
        <input type="text" id="customer_mobile_phone" name="customer_mobile_phone" value="94XXXXXXXXX" />
        <input type="text" name="customer_phone" id="customer_phone" value="94XXXXXXXXX"  />
        <input type="email" id="customer_email" name="customer_email" value="test@gmail.com" />
        <input type="text" id="billing_address_street" name="billing_address_street" value="154"/>
        <input type="text" name="billing_address_city" id="billing_address_city" value="Vavuniya">
        <input type="text" name="billing_address_province" id="billing_address_province" value="North Province">
        <input type="hidden" name="billing_address_country" id="billing_address_country" value="LKA">
        <input type="text" name="billing_address_postcode" id="billing_address_postcode" value="43000">
        <input type="submit" value="PAY Now">
       </form>
     </body>
    </html>
```

Submit your form json data into Payable

```
    function returnForm(form_jsondata) {
        payable.startPayment(form_jsondata);
    }

```

##### Listening to Payable Payment Gateway

Once you connect to Payable Payment Gateway, You can listen sdk response.

```
    window.addEventListener('load', function() {

    });

```

As soon as the payment is processed, You can get the payment status.

```
   payable.onCompleted = function onCompleted(data) {
        console.log("Payment completed")
    };

```

If the payment gateway dismissed you can get the connection status.

```
   payable.onDismissed = function onDismissed() {
        log("Payment Cancel");
    };

```

You can get the error details from `onError`. Error will be field validation (3009), Gateway callback error (3008) and timeout error (3007).

```
   payable.onError = function onError(error) {
        if (error.code === 3009) { // field validation error
            error.fields.forEach((field) => {
                console.log(field.error)
            });
        }
        if (error.code === 3008) { // mpgs error callback
            console.log(error)
        }
        if (error.code === 3007) { // timeout error
            console.log(error)
        }
    };

```

##### Sample HTML Code

```
<html>
<head>
    <title>ABC Fashion</title>
    <script src="https://sandboxipgsdk.payable.lk/sdk/v2/payable-checkout-sandbox.js"></script>
    <script>
        window.addEventListener('load', function() {

            payable.onCompleted = function onCompleted(data) {
                console.log("Payment completed");
            };

            payable.onDismissed = function onDismissed() {
                console.log("Payment Cancel");
            };


            payable.onError = function onError(error) {
                if (error.code === 3009) { // field validation error
                    error.fields.forEach((field) => {
                        console.log(field.error)
                    });
                }
                if (error.code === 3008) { // mpgs error callback
                    console.log(error)
                }
                if (error.code === 3007) { // timeout error
                    console.log(error)
                }
            };
        });

        function returnForm() {
            var payment = {
                amount: "59.91",
                billing_address_city: "Vavuniya",
                billing_address_company: "Pay Shop",
                billing_address_country: "LKA",
                billing_address_postcode: "43000",
                billing_address_province: "North Province",
                billing_address_street: "154",
                billing_address_street2: "Koomankulam",
                cancel_url: "https://yoursite.com/payment/cancel",
                check_value: "C6FXXXXXXXXXXXXXXXXXXXXXX",
                currency_code: "LKR",
                custom_1: "customYuDSFk5Z1O",
                custom_2: "test2",
                customer_email: "testmail@gmail.com",
                customer_first_name: "Shakthi",
                customer_last_name: "Laxmy",
                customer_mobile_phone: "07XXXXXXXX",
                customer_phone: "07XXXXXXXX",
                invoice_id: "INVvw5EA0d1pH",
                merchant_key: "D7XXXXXXXXX",
                notify_url: "https://yoursite.com/payment/nortify",
                order_description: "Sandbox payment",
                return_url: "https://yoursite.com/payment/return",
                shipping_address_city: "Colombo",
                shipping_address_company: "Payable",
                shipping_address_country: "LKA",
                shipping_address_postcode: "43000",
                shipping_address_province: "western province",
                shipping_address_street: "Main street",
                shipping_address_street2: "Temple road",
                shipping_contact_email: "testshipmail@gmail.com",
                shipping_contact_first_name: "Kumaran",
                shipping_contact_last_name: "Test Lastname",
                shipping_contact_mobile: "07XXXXXXXX",
                shipping_contact_phone: "07XXXXXXXX",
            };
            payable.startPayment(payment);
        }
    </script>
</head>
<body>
    <button onclick="returnForm()" name="btnpay">PAY Now</button>
</body>
</html>
```

Listening to Payment Notification

Payable Payment Gateway will send back to your website notifies the payment status to the notify_url
