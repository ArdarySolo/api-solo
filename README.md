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
```        
