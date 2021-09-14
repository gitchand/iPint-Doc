# iPint-Doc
* [Introduction](#introduction_)
* [How it works?](#how_it_works)
* [Development](#development_section)
  * [Integrating with iPint](#integrating_with_ipint)
  * [Checkout Page](#checkout_page)
  * [API Reference](#api_reference)

## <a name="introduction_">Introduction</a>
Wecolme to iPint! For merchants and businesses accepting payments is limited to 'fiat currencies' through traditional means. Traditional method are costly, inefficient and risk prone. They are geographically restrictive.

iPint allows businesses to accept crypto payments by its secure, easy to use and easy to integrate payment service.

## <a name="how_it_works">How it works?</a>
### Step 1
Customer selects cryptocurrency as payment method.
### Step 2
Customer selects specific coin & amount of USD to be deposited. QR code/invoice generated with amount & address. Transfers crypto within time limit.
### Step 3
Payment is confirmed on blockchain. Customer gets deposit in his account. Merchant is informed in realtime. Merchants settlement happens in USDT.

Check <a href="https://ipint.io/demo-checkout/" target="_blank">Demo</a>

## <a name="development_section">Development</a>
### <a name="integrating_with_ipint">Integrating with iPint</a>
  * #### iPint API
     Fully customizable integration into any online shop or website
  * #### Pop-in iFrame
     Displaying within your web page
  * #### Redirect to iPint
     Simple to implement, open in iPint secure page
### <a name="checkout_page">Checkout Page</a>
To open iPint checkout page, redirect to https:ipint.io/invoice?id=fetch-id-from-the-folliwing-step
<br /> To get id to be fetched in the redirect url, call [/checkout](#checkout_endpoint) endpoint.
### <a name="api_reference">API Reference</a>
- All endpoints return either a JSON object or array.
- In case of POST method, request data will be JSON 
- Base URL https://api.ipint.io:8003
##### <a name="checkout_endpoint">Checkout</a>
To get id to be fetched in the redirect url.
* ###### URL
  /checkout
* ###### Method
  POST
* ###### Headers
  apikey
* ###### URL Params
  None
* ###### Data Params
  *Required:* client_email_id, client_preferred_fiat_currency, merchant_website
  
  *Conditional:* merchant_id
  
  *Optional:* amount
  
```
{
    "client_email_id": "client-email-address-for-unique-reference-id",
    "client_preferred_fiat_currency": "local-currency-code",
    "amount": "1000",
    "merchant_id": "ipint-merchant-id",
    "merchant_website": "merchant-website"
}
```
* ###### Success Response
  *Code*: 200
  
  *Content*: {"session_id":"id-to-be-fetched-in-the-url-to-redirect-to-ipint"}
  
  *Note*: Use this id <br />1.To redirect to the iPint checkout page.<br />2. To get status after the payment (call /invoice endpoint)
* ###### Error Response
  *Code*: 400
  *Content*: {"error": true, "message": "error-messsage"}

curl sample code


    curl -H "Content-Type: application/json" -H "apikey: your-api-key" -X POST -d '{"client_email_id":"customer-email-id","client_preferred_fiat_currency":"local-currency-code", "merchant_id": "merchant-id"}' https://api.ipint.io:8003/checkout

`
