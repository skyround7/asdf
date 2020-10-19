## 1.Prerequisite
 1) Public IPs (for IP Whitelisting) 
    Please ensure that the following address names are whitelisted in your firewall

 2) Merchant Store ID

## 2.Summary of flow
![flow](https://user-images.githubusercontent.com/72907629/96084251-bcac8300-0ef9-11eb-951f-bb96589a049c.png)


## 3.API Server Information
Sandbox : https://stg.anyonepay.ph/checkout/api-sev
Production : https://api.anyonepay.ph

## 4.Register API
- Register a new payment transaction

### 4.1 End point URI
[POST] /registerPayment

### 4.2 Request Header
![image](https://user-images.githubusercontent.com/72907629/96085708-262d9100-0efc-11eb-8e7f-5c7e059a1d67.png)

### 4.3 Request Parameters
![image](https://user-images.githubusercontent.com/72907629/96085819-59702000-0efc-11eb-9234-ede673827187.png)

### 4.4. Request Body Example

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

### 4.5. Response Parameters
![image](https://user-images.githubusercontent.com/72907629/96085985-8e7c7280-0efc-11eb-9c96-752daad95506.png)


### 4.6. Response Body Example

    JSON
    {
        "result_code": "200",
        "result_message": "AOP_PAY_REGISTER_PAYMENT_200_SUCCESS",
        "data": {
            "paymentSeq": 2009141749135764828
            "status": 1
        }
    }

## 5.Verify API
- Verify a result status of payment transaction

### 5.1. End point URI
[POST] /getPaymentResult

### 5.2. Request Header
![image](https://user-images.githubusercontent.com/72907629/96086161-d13e4a80-0efc-11eb-9c99-6d6404d2c3b8.png)

### 5.3 Request Parameters
![image](https://user-images.githubusercontent.com/72907629/96087087-478f7c80-0efe-11eb-9780-3c2a5ad90ad7.png)

### 5.4. Request Body Example
	JSON
	{
	  "paymentSeq": 200604192149017209
	}

### 5.5. Response Parameters
![image](https://user-images.githubusercontent.com/72907629/96087188-70177680-0efe-11eb-9b8f-cc2168e9b4d7.png)

Subset of paymentResult

![image](https://user-images.githubusercontent.com/72907629/96087242-858ca080-0efe-11eb-9d34-e637cbd9b42b.png)

### 5.6. Response Body Example
	JSON
	{
	"result_code": "200",
	"result_message": "AOP_GET_PAYMENT_RESULT_200_SUCCESS",
	"data": {
	    "paymentResult": {
	      "paymentSeq": 2006041921490172097,
	      "payTotalAmount": 15,
	      "payAmount": 13.64,
	      "payVat": 1.36,
	      "payProduct": "testproduct",
	      "payItems": "[{\"price\": \"10\", \"quantity\": \"1\", \"brandName\": \"testBrand1\", \"itemsName\": \"testitems1\", \"totalAmount\": \"10\"}, {\"price\": \"10\", \"quantity\": \"2\", \"brandName\": \"testBrand2\", \"itemsName\": \"testitems2\", \"totalAmount\": \"20\"}]",
	      "payStatus": "SUCCESS",
	      "payDate": 1597743036000,
	      "merchantReferenceNo": "00000002"
	    }
	  },
	  "status": 1
	}

## 6.SDK for PHP
### 6.1. Compatibility
- PHP 5.6 or higher

### 6.2. SDK source code structure
![image](https://user-images.githubusercontent.com/72907629/96087393-be2c7a00-0efe-11eb-90cd-dfb8609d47c8.png)

### 6.3. Install the SDK library
	- Place the lib directory in your source directory.
	- Include the AnyonePay.php file in your source code.
![image](https://user-images.githubusercontent.com/72907629/96087451-d43a3a80-0efe-11eb-891d-2f7e0036f154.png)
	

### 6.4 Register API example
	RegisterStub.php
	<?php
	//Include SDK library files
	require_once __DIR__ . "/../AnyonePay.php";

	use AnyonePay\AnyonePaySdk;
	use AnyonePay\entity\RegisterReq;

	//Initialize environment
	AnyonePaySdk::getInstance()->initConfig("SANDBOX");
	//Configure the input parameter
	$request = new RegisterReq(2005271259396999814, 100, 'Tester', 'joseph@sharetreats.com', '639451901540', 'test_product', 'YourSideUniqueReferenceNumber', 'https://www.anyonepay.ph/sandbox/merchant_result.html', 'https://www.anyonepay.ph/sandbox/merchant_result.html',
	'https://www.anyonepay.ph/sandbox/merchant_cancel.html');

	//Try to send API transaction
	$response = $request->send();

	//Check the result of response
	echo 'checkoutUrl : ' . $response->checkoutUrl;

### 6.5. Verify API example
	VerifyStub.php
	<?php
	//Include SDK library files
	require_once __DIR__ . "/../AnyonePay.php";

	use AnyonePay\AnyonePaySdk;
	use AnyonePay\entity\VerifyReq;

	//Initialize environment
	AnyonePaySdk::getInstance()->initConfig("SANDBOX");

	//Configure the input parameter
	$request = new VerifyReq(2006041921490172097);

	//Try to send API transaction
	$response = $request->send();

	//Check the result of response
	echo 'paymentSeq : ' . $response->paymentSeq;

## 7. SandBox API
- SandBox product purchase api. 
- prepare the credential for sandbox configuration from Business site of your account.

-Test

![image](https://user-images.githubusercontent.com/72907629/96394075-16fc5b00-11fc-11eb-9fb3-6e1c7f53f25a.png)

### 7.1. End point URI
[POST] /registerPayment

### 7.2. Request Header
![image](https://user-images.githubusercontent.com/72907629/96394169-4ca14400-11fc-11eb-831a-d76b2917db59.png)

### 7.3. Request Parameters
![image](https://user-images.githubusercontent.com/72907629/96404812-cba37600-1216-11eb-95c8-a83825b55b62.png)

### 7.4. Request Body Example
	JSON
	
	{
	  "storeId": "2009230959474681499",
	  "amount": "1.00",
	  "product": "Test-Product",
	  "redirectUrl": "https://example.com/sandbox/merchant_result.html",
	  "webhookUrl": "https://example.com/webhook",
	  "cancelUrl": "https://example.com/cancel",
	  "referenceNo": "123456789"
	}

### 7.5. Response Parameters
![image](https://user-images.githubusercontent.com/72907629/96394362-bde0f700-11fc-11eb-9763-176703b037b1.png)

### 7.6. Response Body Example
	JSON
	{
	 "result_code": 200,
	  "result_message": "AOP_PAY_REGISTER_PAYMENT_200_SUCCESS",
	  "data": {
	    "paymentSeq": "2010151641324683967",
	    "referenceNo": "123456789",
	    "redirectUrl": "http://api-sandbox.anyonepay.ph/checkout/?entry=consent&paymentSeq=2010151641324683967&cancelUrl=https%3A%2F%2Fexample.com%2Fcancel"
	  }
	}





