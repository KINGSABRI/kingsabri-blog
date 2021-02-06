# Ruby \| How to Send an email from Microsoft Exchange

If you having a hard time sending an email from and MS-Exchange server, here's the easy way.

```text
gem install viewpoint
```

```ruby
require 'viewpoint'
include Viewpoint
endpoint = 'https://domain.com/ews/Exchange.asmx'
username = AD_Account
password = AD_Acc_Pass
EWS::EWS.endpoint = endpoint
EWS::EWS.set_auth(username, password)
message = EWS::Message
message.send('Hi subject', 'Hola body!', ['to_mail@domain.com'], ['cc1_mail@domain.com', 'cc2_mail@domain.com'])r);" (actually changes the password)
```



