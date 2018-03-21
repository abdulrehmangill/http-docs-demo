# 

**`API Version:`** `2.2.4`




The Telstra SMS Messaging API allows your applications to send and receive
SMS text messages from Australia's leading network operator.


It also allows your application to track the delivery status of both sent
and received SMS messages.




## Base URL

The base URL for this API is `https://tapi.telstra.com/v2`



## Authentication
This API uses `OAuth v2.0` with `Client Credentials` grant type.

**Access Token URL:** `/oauth/token` 



### Scopes

The API makes use of the following OAuth scopes: 

| Name | Value | Description |
| ---- | ----- | ----------- |
| NSMS | `NSMS` | NSMS |





# <a name="api_reference"></a>API Reference

* [Provisioning](#provisioning)
* [Messaging](#messaging)
* [authentication](#authentication)

## <a name="provisioning"></a>![Endpoint Group: ](https://apidocs.io/img/class.png "Provisioning") Provisioning


### <a name="delete_subscription"></a>![Endpoint: ](https://apidocs.io/img/method.png "Delete Subscription") Delete Subscription


**`DELETE`** `/messages/provisioning/subscriptions`

> Delete a mobile number subscription from an account



#### Scopes
The list of required scopes for this endpoint are:

- [`NSMS`](#scopes)



#### Request Headers
>Accept=application/json;
>Content-Type=application/json;

#### Request Body
Raw 

|  Type | Tags | Description |
| ------| ---- |-------------| 
| [DeleteNumberRequest](#delete_number_request) |  ``` Required ```  | EmptyArr | 

 *Example Request Body* 
``` 
{
  "emptyArr": 0
}
``` 

#### Responses
**204** 

> No Content



**400** 

> Invalid or missing request parameters

**401** 

> Invalid access token. Please try with a valid token

**403** 

> 
Authorization credentials passed and accepted but account does not have permission . SpikeArrest-The API call rate limit has been exceeded

**404** 

> 
The requested URI does not exist . RESOURCE-NOT-FOUND

**500** 

> 
Technical error : Unable to route the message to a Target Endpoint :
An error has occurred while processing your request, please refer to
API Docs for summary on the issue

**Default** 

> An internal error occurred when processing the request


### <a name="get_subscription"></a>![Endpoint: ](https://apidocs.io/img/method.png "Get Subscription") Get Subscription


**`GET`** `/messages/provisioning/subscriptions`

> Get mobile number subscription for an account



#### Scopes
The list of required scopes for this endpoint are:

- [`NSMS`](#scopes)



#### Responses
**200** 

> Success


 *Example Body* (**[GetSubscriptionResponse](#get_subscription_response)**) 

```
{
  "activeDays": "3",
  "notifyURL": "http://notifyurl.com",
  "destinationAddress": "+19995550123"
}
```


**400** 

> Invalid or missing request parameters

**401** 

> Invalid access token. Please try with a valid token

**403** 

> 
Authorization credentials passed and accepted but account does not
have permission. SpikeArrest-The API call rate limit has been exceeded

**404** 

> 
The requested URI does not exist . RESOURCE-NOT-FOUND

**500** 

> 
Technical error : Unable to route the message to a Target Endpoint :
An error has occurred while processing your request, please refer to
API Docs for summary on the issue

**Default** 

> An internal error occurred when processing the request


### <a name="create_subscription"></a>![Endpoint: ](https://apidocs.io/img/method.png "Create Subscription") Create Subscription


**`POST`** `/messages/provisioning/subscriptions`

> Provision a mobile number



#### Scopes
The list of required scopes for this endpoint are:

- [`NSMS`](#scopes)



#### Request Headers
>Accept=application/json;
>Content-Type=application/json;

#### Request Body
Raw 

|  Type | Tags | Description |
| ------| ---- |-------------| 
| [ProvisionNumberRequest](#provision_number_request) |  ``` Required ```  | A JSON payload containing the required attributes | 

 *Example Request Body* 
``` 
{
  "activeDays": 20,
  "notifyURL": "http://notifyurl.com"
}
``` 

#### Responses
**201** 

> Created


 *Example Body* (**[ProvisionNumberResponse](#provision_number_response)**) 

```
{
  "destinationAddress": "+19995550123"
}
```


**400** 

> Invalid or missing request parameters

**401** 

> Invalid access token. Please try with a valid token

**403** 

> 
Authorization credentials passed and accepted but account does not
have permission. SpikeArrest-The API call rate limit has been exceeded

**404** 

> 
The requested URI does not exist . RESOURCE-NOT-FOUND

**500** 

> 
Technical error : Unable to route the message to a Target Endpoint :
An error has occurred while processing your request, please refer to
API Docs for summary on the issue

**Default** 

> An internal error occurred when processing the request


[Back to API Reference](#api_reference)

## <a name="messaging"></a>![Endpoint Group: ](https://apidocs.io/img/class.png "Messaging") Messaging


### <a name="send_mms"></a>![Endpoint: ](https://apidocs.io/img/method.png "Send MMS") Send MMS


**`POST`** `/messages/mms`

> Send MMS



#### Scopes
The list of required scopes for this endpoint are:

- [`NSMS`](#scopes)



#### Request Headers
>Accept=application/json;
>Content-Type=application/json;

#### Request Body
Raw 

|  Type | Tags | Description |
| ------| ---- |-------------| 
| [Send MMS Request](#send_mms_request) |  ``` Required ```  | A JSON or XML payload containing the recipient's phone number<br><br><br>and MMS message.The recipient number should be in the format<br>'04xxxxxxxx'<br><br><br>where x is a digit | 

 *Example Request Body* 
``` 
{
  "from": "+19995554443",
  "to": "+19995550123",
  "subject": "This is a test MMS",
  "replyRequest": true,
  "MMSContent": [
    {
      "type": "amr",
      "filename": "hello",
      "payload": "payload"
    }
  ]
}
``` 

#### Responses
**201** 

> Created


 *Example Body* (**[MessageSentResponse](#message_sent_response)**) 

```
{
  "messages": [
    {
      "to": "Bob",
      "deliveryStatus": "success",
      "messageId": "88",
      "messageStatusURL": "http://thisisdummy.com"
    }
  ],
  "messageType": "SMS",
  "numberSegments": 4,
  "NumberNationalDestinations": 22
}
```


**400** 

> 
Invalid or missing request parameters. MMS-TYPE-MISSING . MMS-PAYLOAD-MISSING . MMS-FILENAME-MISSING . DELIVERY-IMPOSSIBLE . TO-MSISDN-NOT-VALID . SENDER-MISSING . DELIVERY-IMPOSSIBLE . SUBJECT-TOO-LONG . FROM-MSISDN-TOO-LONG . TO-MSISDN-TOO-LONG . NOT-PROVISIONED . Request flagged as containing suspicious content

**401** 

> Invalid access token. Please try with a valid token

**403** 

> 
Authorization credentials passed and accepted but account does not have permission. SpikeArrest-The API call rate limit has been exceeded

**404** 

> 
The requested URI does not exist . RESOURCE-NOT-FOUND

**405** 

> The requested resource does not support the supplied verb

**415** 

> API does not support the requested content type

**422** 

> 
The request is formed correctly, but due to some condition the request cannot be processed e.g. email is required and it is not provided in the request

**500** 

> 
Technical error : Unable to route the message to a Target Endpoint :
An error has occurred while processing your request, please refer to
API Docs for summary on the issue

**501** 

> 
The HTTP method being used has not yet been implemented for the requested resource

**503** 

> The service requested is currently unavailable

**Default** 

> An internal error occurred when processing the request


### <a name="get_mms_status"></a>![Endpoint: ](https://apidocs.io/img/method.png "Get MMS Status") Get MMS Status


**`GET`** `/messages/mms/{messageid}/status`

> Get MMS Status



#### Scopes
The list of required scopes for this endpoint are:

- [`NSMS`](#scopes)



#### Path Parameters
| Parameter | Type | Tags | Description | Example |
|-----------|------| ---- |-------------| ----------------------------------- |
| messageid | string |  ``` Required ```  | Unique identifier of a message - it is the value returned from<br><br>a previous POST call to https://api.telstra.com/v2/messages/mms | `123` | 

#### Responses
**200** 

> Outbound poll response


 *Example Body* (**[[OutboundPollResponse](#outbound_poll_response)]**) 

```
[
  {
    "to": "+19995550123",
    "receivedTimestamp": "2002-10-03T15:00:00+00:00",
    "sentTimestamp": "2002-10-02T15:00:00+00:00",
    "deliveryStatus": "PEND"
  }
]
```


**400** 

> 
Invalid or missing request parameters . NOT-PROVISIONED . Request flagged as containing suspicious content

**401** 

> Invalid access token. Please try with a valid token

**403** 

> 
Authorization credentials passed and accepted but account does not have permission . SpikeArrest-The API call rate limit has been exceeded

**404** 

> 
The requested URI does not exist . OLD-NONEXISTANT-MESSAGE-ID . RESOURCE-NOT-FOUND

**405** 

> The requested resource does not support the supplied verb

**415** 

> API does not support the requested content type

**422** 

> 
The request is formed correctly, but due to some condition the request cannot be processed e.g. email is required and it is not provided in the request

**500** 

> 
Technical error : Unable to route the message to a Target Endpoint :
An error has occurred while processing your request, please refer to
API Docs for summary on the issue

**501** 

> 
The HTTP method being used has not yet been implemented for the requested resource

**503** 

> The service requested is currently unavailable

**Default** 

> An internal error occurred when processing the request


### <a name="send_sms"></a>![Endpoint: ](https://apidocs.io/img/method.png "Send SMS") Send SMS


**`POST`** `/messages/sms`

> Send Message



#### Scopes
The list of required scopes for this endpoint are:

- [`NSMS`](#scopes)



#### Request Headers
>Accept=application/json;
>Content-Type=application/json;

#### Request Body
Raw 

|  Type | Tags | Description |
| ------| ---- |-------------| 
| [SendSMSRequest](#send_sms_request) |  ``` Required ```  | A JSON or XML payload containing the recipient's phone number and<br>text message.<br>The recipient number should be in the format '04xxxxxxxx' where x is<br>a digit | 

 *Example Request Body* 
``` 
{
  "to": "+19995550123",
  "from": "+19995552223",
  "body": "This is a test message",
  "validity": 20,
  "scheduledDelivery": 20,
  "notifyURL": "http://notifyurl.com",
  "replyRequest": true
}
``` 

#### Responses
**201** 

> Created


 *Example Body* (**[MessageSentResponse](#message_sent_response)**) 

```
{
  "messages": [
    {
      "to": "Bob",
      "deliveryStatus": "success",
      "messageId": "88",
      "messageStatusURL": "http://thisisdummy.com"
    }
  ],
  "messageType": "SMS",
  "numberSegments": 4,
  "NumberNationalDestinations": 22
}
```


**400** 

> 
Invalid or missing request parameters . TO-MSISDN-NOT-VALID . SENDER-MISSING . DELIVERY-IMPOSSIBLE . FROM-MSISDN-TOO-LONG . BODY-TOO-LONG . BODY-MISSING . TO-MSISDN-TOO-LONG . TECH-ERR . BODY-NOT-VALID . NOT-PROVISIONED . Request flagged as containing suspicious content

**401** 

> Invalid access token. Please try with a valid token

**403** 

> 
Authorization credentials passed and accepted but account does not have permission . SpikeArrest-The API call rate limit has been exceeded

**404** 

> 
The requested URI does not exist . RESOURCE-NOT-FOUND

**405** 

> The requested resource does not support the supplied verb

**415** 

> API does not support the requested content type

**422** 

> 
The request is formed correctly, but due to some condition the request cannot be processed e.g. email is required and it is not provided in the request

**500** 

> 
Technical error : Unable to route the message to a Target Endpoint :
An error has occurred while processing your request, please refer to
API Docs for summary on the issue

**501** 

> 
The HTTP method being used has not yet been implemented for the requested resource

**503** 

> The service requested is currently unavailable

**Default** 

> An internal error occurred when processing the request


### <a name="retrieve_sms_responses"></a>![Endpoint: ](https://apidocs.io/img/method.png "Retrieve SMS Responses") Retrieve SMS Responses


**`GET`** `/messages/sms`

> Retrieve Messages



#### Scopes
The list of required scopes for this endpoint are:

- [`NSMS`](#scopes)



#### Responses
**200** 

> Success


 *Example Body* (**[InboundPollResponse](#inbound_poll_response)**) 

```
{
  "status": "success",
  "destinationAddress": "+19995550123",
  "senderAddress": "+19995550123",
  "message": "Hello this is a test message",
  "messageId": "121",
  "sentTimestamp": "2002-10-03T15:00:00+00:00"
}
```


**400** 

> 
Invalid or missing request parameters . NOT-PROVISIONED . Request flagged as containing suspicious content

**401** 

> Invalid access token. Please try with a valid token

**403** 

> 
Authorization credentials passed and accepted but account does not have permission . SpikeArrest-The API call rate limit has been exceeded

**404** 

> 
The requested URI does not exist . RESOURCE-NOT-FOUND

**405** 

> The requested resource does not support the supplied verb

**415** 

> API does not support the requested content type

**422** 

> 
The request is formed correctly, but due to some condition the request cannot be processed e.g. email is required and it is not provided in the request

**500** 

> 
Technical error : Unable to route the message to a Target Endpoint :
An error has occurred while processing your request, please refer to
API Docs for summary on the issue

**501** 

> 
The HTTP method being used has not yet been implemented for the requested resource

**503** 

> The service requested is currently unavailable

**Default** 

> An internal error occurred when processing the request


### <a name="get_sms_status"></a>![Endpoint: ](https://apidocs.io/img/method.png "Get SMS Status") Get SMS Status


**`GET`** `/messages/sms/{messageId}/status`

> Get Message Status



#### Scopes
The list of required scopes for this endpoint are:

- [`NSMS`](#scopes)



#### Path Parameters
| Parameter | Type | Tags | Description | Example |
|-----------|------| ---- |-------------| ----------------------------------- |
| messageId | string |  ``` Required ```  | Unique identifier of a message - it is the value returned from a previous POST call to https://api.telstra.com/v2/messages/sms | `123` | 

#### Responses
**200** 

> Success


 *Example Body* (**[[OutboundPollResponse](#outbound_poll_response)]**) 

```
[
  {
    "to": "+19995550123",
    "receivedTimestamp": "2002-10-03T15:00:00+00:00",
    "sentTimestamp": "2002-10-02T15:00:00+00:00",
    "deliveryStatus": "PEND"
  }
]
```


**400** 

> 
Invalid or missing request parameters .  NOT-PROVISIONED . Request flagged as containing suspicious content

**401** 

> Invalid access token. Please try with a valid token

**403** 

> 
Authorization credentials passed and accepted but account does not have permission . SpikeArrest-The API call rate limit has been exceeded

**404** 

> 
The requested URI does not exist. OLD-NONEXISTANT-MESSAGE-ID. RESOURCE-NOT-FOUND

**405** 

> The requested resource does not support the supplied verb

**415** 

> API does not support the requested content type

**422** 

> 
The request is formed correctly, but due to some condition the request cannot be processed e.g. email is required and it is not provided in the request

**500** 

> 
Technical error : Unable to route the message to a Target Endpoint :
An error has occurred while processing your request, please refer to
API Docs for summary on the issue

**501** 

> 
The HTTP method being used has not yet been implemented for the requested resource

**503** 

> The service requested is currently unavailable

**Default** 

> An internal error occurred when processing the request


[Back to API Reference](#api_reference)

## <a name="authentication"></a>![Endpoint Group: ](https://apidocs.io/img/class.png "authentication") authentication


### <a name="auth_token"></a>![Endpoint: ](https://apidocs.io/img/method.png "auth token") auth token


**`POST`** `/oauth/token`

> *Tags:*  ``` Skips Authentication ``` 

> Generate authentication token




#### Request Headers
>Content-Type=application/x-www-form-urlencoded;

#### Request Body
Url Encoded

| Parameter | Type | Tags | Description | Default Value |
|-----------|------| ---- |-------------| ------------- | 
| client_id | string |  ``` Required ```  | Client identifier to identify the application |  | 
| client_secret | string |  ``` Required ```  | Helps authenticate the identity of the application |  | 
| grant_type | string |  ``` Required ```  | The OAuth grant type used | `"client_credentials"` | 

*Example Request Body*
```
 client_id = 123 
 client_secret = abc123 
 grant_type = client_credentials 
```

#### Responses
**200** 

> Success


 *Example Body* (**[OAuthResponse](#o_auth_response)**) 

```
{
  "access_token": "access token string",
  "token_type": "token type",
  "expires_in": "3600"
}
```


**400** 

> unsupported_grant_type

**401** 

> invalid_client

**404** 

> The requested URI does not exist

**503** 

> The service requested is currently unavailable

**Default** 

> An internal error occurred when processing the request


[Back to API Reference](#api_reference)

# <a name="models"></a> Models

### List of Models

* [MessageSentResponse](#message_sent_response)
* [MMSContent](#mms_content)
* [OAuthResponse](#o_auth_response)
* [OAuthRequest](#o_auth_request)
* [MessageType](#message_type)
* [Error_Error_Error](#error_error_error)
* [OutboundPollResponse](#outbound_poll_response)
* [Message](#message)
* [GetSubscriptionResponse](#get_subscription_response)
* [ProvisionNumberRequest](#provision_number_request)
* [InboundPollResponse](#inbound_poll_response)
* [Send MMS Request](#send_mms_request)
* [SendSMSRequest](#send_sms_request)
* [Status](#status)
* [Error_Error](#error_error)
* [ProvisionNumberResponse](#provision_number_response)
* [DeleteNumberRequest](#delete_number_request)
## <a name="message_sent_response"></a>![Type: ](https://apidocs.io/img/method.png "MessageSentResponse") MessageSentResponse



> Model for response received on sending an SMS/MMS





| Name | Type | Tags | Description |
|-----------|------| ---- |-------------| 
| messages | [Message](#message) |  ``` Required ```  ``` Collection ```  | List of messages | 
| messageType | string |  ``` Required ```  | Type of message | 
| numberSegments | number |  ``` Required ```  | Number of segments | 
| NumberNationalDestinations | number |  ``` Optional ```  | Number of national destinations | 
| NumberInternationalDestinations | number |  ``` Optional ```  | Number of international destinations | 



#### Example
```
{
  "messages": [
    {
      "to": "Bob",
      "deliveryStatus": "success",
      "messageId": "88",
      "messageStatusURL": "http://thisisdummy.com"
    }
  ],
  "messageType": "SMS",
  "numberSegments": 4,
  "NumberNationalDestinations": 22
}
```



## <a name="mms_content"></a>![Type: ](https://apidocs.io/img/method.png "MMSContent") MMSContent



> Model definining MMS content





| Name | Type | Tags | Description |
|-----------|------| ---- |-------------| 
| type | string |  ``` Required ```  | The following types are supported audio/amr 	audio/aac 	audio/mp3<br>	audio/mpeg3 	audio/mpeg 	audio/mpg 	audio/wav 	audio/3gpp 	audio/mp4<br>	image/gif 	image/jpeg 	image/jpg 	image/png 	image/bmp 	video/mpeg4<br>	video/mp4 	video/mpeg 	video/3gpp 	video/3gp 	video/h263 	text/plain<br>	text/x-vCard 	text/x-vCalendar | 
| filename | string |  ``` Required ```  | The file name to be associated with the content. Some devices<br><br>will display this file name with a placeholder for the content. | 
| payload | string |  ``` Required ```  | The actual payload of the message | 



#### Example
```
{
  "type": "amr",
  "filename": "hello",
  "payload": "payload"
}
```



## <a name="o_auth_response"></a>![Type: ](https://apidocs.io/img/method.png "OAuthResponse") OAuthResponse



> Response model for OAuth





| Name | Type | Tags | Description |
|-----------|------| ---- |-------------| 
| access_token | string |  ``` Optional ```  | OAuth access token | 
| token_type | string |  ``` Optional ```  | OAuth token type | 
| expires_in | string |  ``` Optional ```  | OAuth expiry time | 



#### Example
```
{
  "access_token": "access token string",
  "token_type": "token type",
  "expires_in": "3600"
}
```



## <a name="o_auth_request"></a>![Type: ](https://apidocs.io/img/method.png "OAuthRequest") OAuthRequest



> Request model for OAuth





| Name | Type | Tags | Description |
|-----------|------| ---- |-------------| 
| client_id | string |  ``` Required ```  | Client id | 
| client_secret | string |  ``` Required ```  | Client secret | 
| grant_type | string |  ``` Required ```  | OAuth grant type | 
| scopes | string |  ``` Required ```  | OAuth scope | 



#### Example
```
{
  "client_id": "123",
  "client_secret": "abc",
  "grant_type": "client_credentials",
  "scopes": "NSMS"
}
```



## <a name="message_type"></a>![Type: ](https://apidocs.io/img/method.png "MessageType") MessageType



> Types of messages possible





This type must take a value from the following `string` enumeration of values:

| Name | Value | Description |
| ---- | ----- | ----------- |
| SMS | `SMS` | Sms type | 
| MMS | `MMS` | Mms type | 
| RCS | `RCS` | Rcs type | 



#### Example
```
SMS
```



## <a name="error_error_error"></a>![Type: ](https://apidocs.io/img/method.png "Error_Error_Error") Error_Error_Error



> Returns error status code and message





| Name | Type | Tags | Description |
|-----------|------| ---- |-------------| 
| status | number |  ``` Optional ```  | The status code. | 
| message | string |  ``` Optional ```  | Message describing the error. | 



#### Example
```
{
  "status": 404,
  "message": "Not found"
}
```



## <a name="outbound_poll_response"></a>![Type: ](https://apidocs.io/img/method.png "OutboundPollResponse") OutboundPollResponse



> Model for response containing message status





| Name | Type | Tags | Description |
|-----------|------| ---- |-------------| 
| to | string |  ``` Optional ```  | The phone number (recipient) the message was sent to (in E.164<br><br>format). | 
| receivedTimestamp | string |  ``` Optional ```  | The date and time when the message was recieved by recipient. | 
| sentTimestamp | string |  ``` Optional ```  | The date and time when the message was sent. | 
| deliveryStatus | [Status](#status) |  ``` Optional ```  | Current status of message | 



#### Example
```
{
  "to": "+19995550123",
  "receivedTimestamp": "2002-10-03T15:00:00+00:00",
  "sentTimestamp": "2002-10-02T15:00:00+00:00",
  "deliveryStatus": "PEND"
}
```



## <a name="message"></a>![Type: ](https://apidocs.io/img/method.png "Message") Message



> Model defining a message





| Name | Type | Tags | Description |
|-----------|------| ---- |-------------| 
| to | string |  ``` Required ```  | To whom you are sending the message | 
| deliveryStatus | string |  ``` Required ```  | Whether the message was successfully delivered or not | 
| messageId | string |  ``` Required ```  | Identifier of the message | 
| messageStatusURL | string |  ``` Optional ```  | URL at which you can view status of message | 



#### Example
```
{
  "to": "Bob",
  "deliveryStatus": "success",
  "messageId": "88",
  "messageStatusURL": "http://thisisdummy.com"
}
```



## <a name="get_subscription_response"></a>![Type: ](https://apidocs.io/img/method.png "GetSubscriptionResponse") GetSubscriptionResponse



> Response model for getting mobile number subscription for an account





| Name | Type | Tags | Description |
|-----------|------| ---- |-------------| 
| activeDays | string |  ``` Optional ```  | Number of active days | 
| notifyURL | string |  ``` Optional ```  | Notify url configured | 
| destinationAddress | string |  ``` Optional ```  | The mobile phone number that was allocated | 



#### Example
```
{
  "activeDays": "3",
  "notifyURL": "http://notifyurl.com",
  "destinationAddress": "+19995550123"
}
```



## <a name="provision_number_request"></a>![Type: ](https://apidocs.io/img/method.png "ProvisionNumberRequest") ProvisionNumberRequest



> Request model for provision of mobile number





| Name | Type | Tags | Description |
|-----------|------| ---- |-------------| 
| activeDays | number |  ``` Optional ```  | Number of active days | 
| notifyURL | string |  ``` Optional ```  | Notify url | 



#### Example
```
{
  "activeDays": 20,
  "notifyURL": "http://notifyurl.com"
}
```



## <a name="inbound_poll_response"></a>![Type: ](https://apidocs.io/img/method.png "InboundPollResponse") InboundPollResponse



> 
> Poll for incoming messages returning the latest. Only works if no
> 
> callback url was specified when provisioning a number.





| Name | Type | Tags | Description |
|-----------|------| ---- |-------------| 
| status | string |  ``` Optional ```  | message status | 
| destinationAddress | string |  ``` Optional ```  | The phone number (recipient) that the message was sent to(in<br><br>E.164 format). | 
| senderAddress | string |  ``` Optional ```  | The phone number (sender) that the message was sent from (in<br><br>E.164 format). | 
| message | string |  ``` Optional ```  | Text of the message that was sent | 
| messageId | string |  ``` Optional ```  | Message Id | 
| sentTimestamp | string |  ``` Optional ```  | The date and time when the message was sent by recipient. | 



#### Example
```
{
  "status": "success",
  "destinationAddress": "+19995550123",
  "senderAddress": "+19995550123",
  "message": "Hello this is a test message",
  "messageId": "121",
  "sentTimestamp": "2002-10-03T15:00:00+00:00"
}
```



## <a name="send_mms_request"></a>![Type: ](https://apidocs.io/img/method.png "Send MMS Request") Send MMS Request



> Model defining an MMS request





| Name | Type | Tags | Description |
|-----------|------| ---- |-------------| 
| from | string |  ``` Required ```  | This will be the source address that will be displayed on the<br><br><br>receiving device. If it is not present then it will default to the<br>MSISDN<br><br><br>assigned to the app. If replyRequest is set to true, then this field<br>will<br><br><br>be ignored. | 
| to | string |  ``` Required ```  | This is the destination address. | 
| subject | string |  ``` Required ```  | The subject that will be used in an MMS message. | 
| replyRequest | boolean |  ``` Required ```  | If set to true, the reply message functionality will be implemented<br><br>and the to address will be ignored if present. | 
| MMSContent | [MMSContent](#mms_content) |  ``` Required ```  ``` Collection ```  | An Array of content that will be sent in an MMS message. If this<br><br><br>array is present it will cause the “body” element to be ignored, and<br>the<br><br><br>message will be sent as an MMS. | 



#### Example
```
{
  "from": "+19995554443",
  "to": "+19995550123",
  "subject": "This is a test MMS",
  "replyRequest": true,
  "MMSContent": [
    {
      "type": "amr",
      "filename": "hello",
      "payload": "payload"
    }
  ]
}
```



## <a name="send_sms_request"></a>![Type: ](https://apidocs.io/img/method.png "SendSMSRequest") SendSMSRequest



> Model defining a SMS request





| Name | Type | Tags | Description |
|-----------|------| ---- |-------------| 
| to | string |  ``` Required ```  | Phone number (in E.164 format) to send the SMS to. This number<br><br><br>can be in international format if preceeded by a ‘+’, or in national<br>format. | 
| body | string |  ``` Required ```  | The text body of the message. Messages longer than 160 characters<br><br>will be counted as multiple messages. | 
| from | string |  ``` Optional ```  | Phone number (in E.164 format) the SMS was sent from. If not<br><br><br>present, the serverice will use the mobile number associated with the<br>application,<br><br><br>or it be an Alphanumeric address of up to 11 characters. | 
| validity | number |  ``` Optional ```  | How long the platform should attempt to deliver the message for.<br><br>This period is specified in minutes from the message | 
| scheduledDelivery | number |  ``` Optional ```  | How long the platform should wait before attempting to send the<br><br>message - specified in minutes. | 
| notifyURL | string |  ``` Optional ```  | Contains a URL that will be called once your message has been<br><br>processed. The status may be delivered, expired, deleted, etc. | 
| replyRequest | boolean |  ``` Optional ```  | If set to true, the reply message functionality will be implemented<br><br><br>and the to address will be ignored if present. If false or not<br>present,<br><br><br>then normal message handling is implemented. | 



#### Example
```
{
  "to": "+19995550123",
  "from": "+19995552223",
  "body": "This is a test message",
  "validity": 20,
  "scheduledDelivery": 20,
  "notifyURL": "http://notifyurl.com",
  "replyRequest": true
}
```



## <a name="status"></a>![Type: ](https://apidocs.io/img/method.png "Status") Status



> Current status of message





This type must take a value from the following `string` enumeration of values:

| Name | Value | Description |
| ---- | ----- | ----------- |
| PEND | `PEND` | Pending | 
| SENT | `SENT` | Sent | 
| DELIVRD | `DELIVRD` | Delivered | 
| EXPIRED | `EXPIRED` | Expired | 
| DELETED | `DELETED` | Deleted | 
| UNDVBL | `UNDVBL` | Undeliverable | 
| REJECTED | `REJECTED` | Rejected | 
| READ | `READ` | Read | 



#### Example
```
PEND
```



## <a name="error_error"></a>![Type: ](https://apidocs.io/img/method.png "Error_Error") Error_Error



> Model describing an error message





| Name | Type | Tags | Description |
|-----------|------| ---- |-------------| 
| status | string |  ``` Required ```  | A short error code | 
| message | string |  ``` Optional ```  | Message describing the error. | 



#### Example
```
{
  "status": "404",
  "message": "Not found"
}
```



## <a name="provision_number_response"></a>![Type: ](https://apidocs.io/img/method.png "ProvisionNumberResponse") ProvisionNumberResponse



> Response model for provision of mobile number request





| Name | Type | Tags | Description |
|-----------|------| ---- |-------------| 
| destinationAddress | string |  ``` Optional ```  | The mobile phone number that was allocated | 



#### Example
```
{
  "destinationAddress": "+19995550123"
}
```



## <a name="delete_number_request"></a>![Type: ](https://apidocs.io/img/method.png "DeleteNumberRequest") DeleteNumberRequest



> Request model for deleting a mobile number subscription from an account





| Name | Type | Tags | Description |
|-----------|------| ---- |-------------| 
| emptyArr | number |  ``` Optional ```  | Empty Arr | 



#### Example
```
{
  "emptyArr": 0
}
```




