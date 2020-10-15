## Prerequisite
 1) Public IPs (for IP Whitelisting) 
    Please ensure that the following address names are whitelisted in your firewall

 2) Merchant Store ID

## Summary of flow
![flow](https://user-images.githubusercontent.com/72907629/96084251-bcac8300-0ef9-11eb-951f-bb96589a049c.png)


## API Server Information
Sandbox : https://stg.anyonepay.ph/checkout/api-sev
Production : https://api.anyonepay.ph

## Register API
- Register a new payment transaction

4.1. End point URI
[POST] /registerPayment


4.2. Request Header
![image](https://user-images.githubusercontent.com/72907629/96085708-262d9100-0efc-11eb-8e7f-5c7e059a1d67.png)


4.3. Request Parameters
![image](https://user-images.githubusercontent.com/72907629/96085819-59702000-0efc-11eb-9234-ede673827187.png)


4.4. Request Body Example

    JSON
    {
        "storeId": 2005271259396999814,
        "amount": 100,
        "userName": "Joseph",
        "email": "joseph@sharetreats.com",
        "phoneNumber": "639451901540",
        "product": "Brownie chocolate cake",
        "referenceNo": "YourSideUniqueReferenceNumber",
        "redirectUrl": "https://www.merchant-website.ph/callback_page/",
        "webhookUrl": "https://www.merchant-website.ph/webhook_page/"
    }

4.5. Response Parameters
![image](https://user-images.githubusercontent.com/72907629/96085985-8e7c7280-0efc-11eb-9c96-752daad95506.png)


4.6. Response Body Example

    JSON
    {
        "result_code": "200",
        "result_message": "AOP_PAY_REGISTER_PAYMENT_200_SUCCESS",
        "data": {
            "paymentSeq": 2009141749135764828
            "status": 1
        }
    }

## Verify API
- Verify a result status of payment transaction

5.1. End point URI
[POST] /getPaymentResult

5.2. Request Header
![image](https://user-images.githubusercontent.com/72907629/96086161-d13e4a80-0efc-11eb-9c99-6d6404d2c3b8.png)

## Login recaptcha ignore option 
	If registered host exists then ignore recaptcha when try to login
    System Environment 
        -DENV_RECAPTCHA_IGNORE_HOSTS=127.0.0.1,localhost,10.8.0.10
        
## Qwikcilver API Integration
Path docs > qwikcilver > *.md
