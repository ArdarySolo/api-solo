# api-solo
api-solo gives you the opportunity to send  multiple messages at once when you like or add multiple contact
# Installation
$ composer require soloapi/apisolo
# Usage
## Sending an SMS
``` php
<?php
require_once __DIR__ . '/vendor/autoload.php';
use SoloApi\ApiSolo\ApiSolo;
$data='{"header":{"login":"user@gmail.com","accessKey":"xYGt5Dl9wKvz+#RGGU!PjVB+KfiJAYnh%z4&","mode":"prod","priority":2},"messages":[{"phone_number":"+33*****","message":"Hi Cassandra, can you confirm our appointement?","url":"https://www.my-link.com","priorite": 1,"date_to_send":"2022-10-29 10:16:10"},{"phone_number":"+33*****","message":"Dear customer, your package has been sent","url":"","priorite": 1,"date_to_send":"2022-10-29 10:16:10"}]}';
$api = new ApiSolo();
$response=$api->sendSms($data);

?>
```
Result example:
```
[
    {
        "id_sms_api": "Pf7v16XZ38oT02s",
        "sms_per_message": 1,
        "user": "user@gmail.com",
        "sent_time": "2022-10-29T14:12:53.996Z",
        "phone_number": "+336**",
        "message": "Hi Cassandra, can you confirm our appointement https://arsms.co/oloe00F6Vvsa \n \nSent for free from PC via arsms.co/free",
        "sent": 1
    },
    {
        "id_sms_api": "NDztErkiR98DHxB",
        "sms_per_message": 1,
        "user": "user@gmail.com",
        "sent_time": "2022-10-29T14:12:53.996Z",
        "phone_number": "+33******",
        "message": "Dear customer, your package has been sent\n \nSent for free from PC via arsms.co/free",
        "sent": 1
    }
]
```
## Adding contact
``` php
<?php
require_once __DIR__ . '/vendor/autoload.php';
use SoloApi\ApiSolo\ApiSolo;
$data='{"header": [{ "login": "user@gmail.com","password": "YOUR_PASSWORD","api": true}], "contacts": [{ "phone_number": "+1XXXXXXXXXX", "first_name": "Doe","last_name": "Joe", "adress": "contact adress", "email": "contact_email@gmail.com", "country_code":"+XX" // Not in international format },{ "phone_number": "+1XXXXXXXXXX", "first_name": "Smith","last_name": "John","adress": "contact adress","email": "contact_email@gmail.com" }]}';
$api = new ApiSolo();
$response=$api->addContact($data);

?>
```
Result example:
 {  

        "data":{  

        "contact":[  

        {

        "phone_number": "+1XXXXXXXXXX",     // international format

        "first_name": "Doe",

        "last_name": "Joe",

        "adress": "contact adress"

        "email": "contact_email@gmail.com",

        "result":"success"

        },

        {

        "phone_number": "+1XXXXXXXXXX",     // international format

        "first_name": "Smith",

        "last_name": "John",

        "adress": "contact adress"

        "email": "contact_email@gmail.com",

        "result":"success"

        }

        ]

        }

        }
  
## Urls Callback (You do not need to install api solo to use it)
To use urls callbacks in order to get incoming Sms ,Sms delivery status ...You just need to have in your callback url :
### Case Message delivery status :
```php
<?php
$status_message =json_decode($_GET[« status »]);
?>

$status_message is an object like this:
{
  "user":"SENDER_LOGIN",

   "phone_number":"RECIPIENT",

   "status":"received",      // values : "sent" or "received"

   "date_status":"2019-08-09T12:50:54.211Z",

   "id_sms_api":"YOUR_ID_SMS"      // or the one we provide you if empty when sending

 }
 ```
### Case GET INCOMING MESSAGE :
```php
<?php
$message =json_decode($_GET[« message »]);
?>

$message is an object like this:
{
  "title":"incoming sms",

    "from":"+1XXXXXXXXXX",    // phone number (international format)

    "message":"Hello world !",

    "date":"2020-01-21 10:01:38"

 }
 ```
 ### Case GET Clicked link :
```php
<?php
$click =json_decode($_GET[« click »]);
?>

$click is an object like this:
{  

    "title":"clicked link",

    "phonenumber":"+1XXXXXXXXXX",    // phone number (international format)

    "link":"https:\/\/www.my-link.com\/",

    "date":"2019-07-08 15:07:03",

    "id_sms_api":"YOUR_ID_SMS"      // or the one we provide you if empty when sending

 }
 ```
  ### Case GET CALL LOGS :
```php
<?php
$call  =json_decode($_GET[« call  »]);
?>

$call  is an object like this:
{  

    "TITLE":"INCOMING CALL", // or "OUTGOING CALL" or "MISSED"

    "PHONE_NUMBER":"+1XXXXXXXXXX",

    "CALL_TIME":"2019-07-05",

    "DURATION": "15:11:04"

 }
 ```
   ### Case GET CALL QUALIFICATION :
```php
<?php
$qualification  =json_decode($_GET["calls"]);
?>

$qualification is an object like this:
{

"title":"Call qualification From Mobile",// or title can be "Call qualification From Interface"

"from":"+1XXXXXXXXXX", // phone number (international format)

"qualification":"Hello world !",

"date":"2020-01-21 10:01:38"

}
 ```
