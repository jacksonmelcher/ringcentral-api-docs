# Toll-Free SMS vs. Local Numbers

Local and toll-free numbers can be used to send and receive SMS under RingCentral's High Volume SMS program.

| Number Type | Description |
|-|-|
| Local | Local Numbers have geographically assigned area codes, e.g. `650-555-0100`. These numbers may be desirable when your firm has a local presence, e.g. texting for a physical local presence to a recipient in the same geographic area. |
| Toll-Free | Toll-Free Numbers have nation-wide area codes, e.g. `800-555-0100`. These are useful for sending nation-wide when there is no need to associate the message with a specific geographic region. Toll-free numbers have one of the following area codes: 800, 888, 877, 866, 855, 844 or 833. |

Both types of numbers can be purchased in the RingCentral [Account Portal](https://service.ringcentral.com) under "Phone Numbers".

### Carrier Approval

Both local and toll-free numbers enrolled in High Volume SMS can be used to send "Non-Consumer (A2P)" SMS as described in the [CTIA Messaging Principles and Best Practices guide](https://www.ctia.org/the-wireless-industry/industry-commitments/messaging-interoperability-sms-mms).

Local numbers are enrolled in a Commercial Long Code / 10DLC program with wireless carriers that allows these number send at high volume.

### Supported Countries

Currently, High Volume SMS is supported for numbers in the United States and Canada.

## Ordering and Provisioning High Volume SMS Numbers

To use High Volume SMS, you must have one or more phone numbers configured for it. RingCentral SMS-enabled phone numbers can be configured for either Enhanced Business SMS (consumer) or High Volume SMS (non-consumer-A2P), and can be switched back and forth, but a number cannot be both at the same time.

If you don't have a number already, log into the [Account Portal](https://service.ringcentral.com) and navigate to the following location to purchase a new number.

["Phone System" > "All Numbers" > "+ Add Number"](https://service.ringcentral.com/application/company/phoneNumbers/allNumbers)

Once you have a number, it will be initially provisioned for standard SMS (Enhanced Business SMS). To configure a number for High Volume (non-consumer-A2P) use, enroll in the [High Volume SMS beta program](https://gamechanging.dev/sms)</a> and indicate which numbers you want to convert. After your number has been provisioned for High Volume SMS, you can verify the configuration with the steps in the next section on listing valid High Volume SMS numbers.

## Listing Valid High Volume SMS Numbers

Send and receive SMS messages using the High Volume SMS API (`a2p-sms`) requires a phone number with the `A2PSmsSender` feature.

To determine which numbers a user can use to send and receive High Volume SMS, retrieve the user's list of phone numbers from the [`extension/phone-number` endpoint](https://developers.ringcentral.com/api-reference/Phone-Numbers/listExtensionPhoneNumbers) and then filter by numbers with the `A2PSmsSender` feature. The `extension/phone-number` is as follows where `{accountId}` and `{extensionId}` can be replaced by actual values or `~` for the current user's account and extension values.

=== "JavaScript"
	```javascript
    {!> code-samples/messaging/high-volume/list.js !} 
	```

=== "Python"
	```python
    {!> code-samples/messaging/high-volume/list.py !} 
	```

=== "PHP"
	```php
    {!> code-samples/messaging/high-volume/list.php !} 
	```

=== "C#"
	```c#
    {!> code-samples/messaging/high-volume/list.cs !} 
	```

=== "Java"
	```java
    {!> code-samples/messaging/high-volume/list.java !} 
	```

=== "Ruby"
	```ruby
    {!> code-samples/messaging/high-volume/list.rb !} 
	```

=== "HTTP"
	```http
	GET /restapi/v1.0/account/{accountId}/extension/{extensionId}/phone-number
	```

### Response

This example response shows the `A2PSmsSender` feature:

```json hl_lines="12"
{
  "uri":"https://platform.ringcentral.com/restapi/v1.0/account/11111111/extension/22222222/phone-number?page=1&perPage=100",
  "records":[
    {
      "id":33333333,
      "phoneNumber":"+16505550100",
      "paymentType":"Local",
      "type":"VoiceFax",
      "usageType":"DirectNumber",
      "features":[
        "CallerId",
        "A2PSmsSender",
      ],
      "status":"Normal",
      "country":{
        "uri":"https://platform.devtest.ringcentral.com/restapi/v1.0/dictionary/country/1",
        "id":"1",
        "name":"United States"
      }
    }
  ]
}
```
