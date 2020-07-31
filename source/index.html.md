---
title: TestSMS client API v1
language_tabs:
  - shell: cURL
  - ruby: Ruby
  - python: Python
  - go: Go
  - java: Java
  - csharp: C#
  - php: PHP
language_clients:
  - shell: ""
  - ruby: ""
  - python: ""
  - go: ""
  - java: ""
  - csharp: ""
  - php: ""
toc_footers: []
includes: []
search: false
highlight_theme: darkula
headingLevel: 2

---

<!-- Generator: Widdershins v4.0.1 -->

<h1 id="testsms-client-api">TestSMS client API v1</h1>

> Scroll down for code samples, example requests and responses. Select a language for code samples from the tabs above or the mobile navigation menu.

TestSMS helps you verifying the quality of your messaging connections by combining a plug and play management interface and an extensive network of end-user devices globally located. Verify SenderID support, MNP accuracy, content changes, UDH and all SMS properties.<br/> <br/> The Test SMS API allows you to integrate directly with your SMS system and use it in your UI.  It is organized around HTTP REST API. Our API has predictable resource-oriented URLs, accepts JSON-encoded request bodies, returns JSON-encoded responses, and uses standard HTTP response codes, authentication, and verbs.  <br /> <br /> **Introduction**  <br /> <br /> First thing is to create your free Test SMS account, its free for testing and integration process. In order to activate your account, we would need further information regarding your business and how our Test SMS Platform will be of help to your services.  <br /> <aside class="notice"> Once your account is activated you are ready to go live and using Test SMS API. </aside> 

Base URLs:

* <a href="https://my.testsms.com/api">https://my.testsms.com/api</a>

<a href="http://testsms.com">Terms of service</a>
Email: <a href="mailto:info@testsms.com">TestSMS</a> Web: <a href="mailto:info@testsms.com">TestSMS</a> 
License: <a href="http://www.apache.org/licenses/LICENSE-2.0">Apache 2.0</a>

<h1 id="testsms-client-api-authentication">Authentication</h1>

Test SMS uses **OAuth2 over https** to manage authentication and authorisation.OAuth2 is a protocol that lets external applications request permission from another Test SMS user to send requests on their behalf without getting their password.<br /><br /> New to OAuth2? See more at [official OAuth2 site](https://oauth.net/2/) and [using barrer token](https://oauth.net/2/bearer-tokens/).<br />All requests to the TestSMS API require a access_token for authentication. You need your own credentials to generate access token.This token expires in 24 hours and you need to request new one when token expired. <br/> <br/>To get access token as simple text use call **v1/token** and your email and password as credentials. <br/> <br/> In most cases you will use your own platform or apps, such as CLIs, daemons, or services running on your back-end, the system authenticates and authorizes the app rather than a user. For this scenario, typical authentication schemes like username/email + password or social logins don't make sense. Instead, your platform or apps use the **Client Credentials Flow**, in which they pass along their **Client ID and Client Secret** to authenticate themselves and get a token.  <br/><br/>**How it works** <br/><ol><li>Your app authenticates with the Auth0 Authorization Server using its Client ID and Client Secret (**/v1/access-token** endpoint).</li><li>Authorization Server validates the Client ID and Client Secret.</li><li>Authorization Server responds with an Access Token.</li><li>Your application can use the Access Token to call an API on behalf of itself.</li><li>The API responds with requested data</li></ol>

## Get access token by email, password

<a id="opIdtoken"></a>

> Code samples

```shell
curl --request POST \
  --url https://my.testsms.com/api/v1/token \
  --header 'accept: application/json' \
  --header 'content-type: application/json' \
  --data '{"email":"name@comapny.com","password":"******"}'
```

```ruby
require 'uri'
require 'net/http'
require 'openssl'

url = URI("https://my.testsms.com/api/v1/token")

http = Net::HTTP.new(url.host, url.port)
http.use_ssl = true
http.verify_mode = OpenSSL::SSL::VERIFY_NONE

request = Net::HTTP::Post.new(url)
request["content-type"] = 'application/json'
request["accept"] = 'application/json'
request.body = "{\"email\":\"name@comapny.com\",\"password\":\"******\"}"

response = http.request(request)
puts response.read_body
```

```python
import http.client

conn = http.client.HTTPSConnection("my.testsms.com")

payload = "{\"email\":\"name@comapny.com\",\"password\":\"******\"}"

headers = {
    'content-type': "application/json",
    'accept': "application/json"
    }

conn.request("POST", "/api/v1/token", payload, headers)

res = conn.getresponse()
data = res.read()

print(data.decode("utf-8"))
```

```go
package main

import (
	"fmt"
	"strings"
	"net/http"
	"io/ioutil"
)

func main() {

	url := "https://my.testsms.com/api/v1/token"

	payload := strings.NewReader("{\"email\":\"name@comapny.com\",\"password\":\"******\"}")

	req, _ := http.NewRequest("POST", url, payload)

	req.Header.Add("content-type", "application/json")
	req.Header.Add("accept", "application/json")

	res, _ := http.DefaultClient.Do(req)

	defer res.Body.Close()
	body, _ := ioutil.ReadAll(res.Body)

	fmt.Println(res)
	fmt.Println(string(body))

}
```

```java
HttpResponse<String> response = Unirest.post("https://my.testsms.com/api/v1/token")
  .header("content-type", "application/json")
  .header("accept", "application/json")
  .body("{\"email\":\"name@comapny.com\",\"password\":\"******\"}")
  .asString();
```

```csharp
var client = new RestClient("https://my.testsms.com/api/v1/token");
var request = new RestRequest(Method.POST);
request.AddHeader("content-type", "application/json");
request.AddHeader("accept", "application/json");
request.AddParameter("application/json", "{\"email\":\"name@comapny.com\",\"password\":\"******\"}", ParameterType.RequestBody);
IRestResponse response = client.Execute(request);
```

```php
<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => "https://my.testsms.com/api/v1/token",
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => "",
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 30,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => "POST",
  CURLOPT_POSTFIELDS => "{\"email\":\"name@comapny.com\",\"password\":\"******\"}",
  CURLOPT_HTTPHEADER => array(
    "accept: application/json",
    "content-type: application/json"
  ),
));

$response = curl_exec($curl);
$err = curl_error($curl);

curl_close($curl);

if ($err) {
  echo "cURL Error #:" . $err;
} else {
  echo $response;
}
```

`POST /v1/token`

You can use your email and password to get Access Token. Now that you have an access_token you can interact with your Test SMS account via the API. <br />To do so, you must simply append the access token to the header of any API request: <br />**Authorization:** `Bearer {access_token}` 

> Body parameter

```json
{
  "email": "name@comapny.com",
  "password": "******"
}
```

<h3 id="get-access-token-by-email,-password-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[LoginRequest](#schemaloginrequest)|true|The email and password for login|

> Example responses

> token

```json
"eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzUxMiJ9.eyJleHAiOjE1NjE4NDc5ODEsImlhdCI6MTU2MTc2MTU4MSwiZW1haWwiOiJtaW1hcmtvQGdtYWlsLmNvbSJ9.wxOmD0rUaK9yONHpcXuWO4VxkWktPB95ea8s_sK7Xe83-oyaP1hK8pjO1lUIPA9iMThgXH8NRCG4_uc0Z72oow"
```

<h3 id="get-access-token-by-email,-password-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|JWT access token as a simple string|string|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|User is not active or bad request|None|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|Email or password not correct|None|
|429|[Too Many Requests](https://tools.ietf.org/html/rfc6585#section-4)|Too many access token attemts|None|
|501|[Not Implemented](https://tools.ietf.org/html/rfc7231#section-6.6.2)|Internal Server Error|None|

<aside class="success">
This operation does not require authentication
</aside>

## Get access token using Client Credentials Flow

<a id="opIdaccessToken"></a>

> Code samples

```shell
curl --request POST \
  --url https://my.testsms.com/api/v1/access-token \
  --header 'accept: application/json' \
  --header 'content-type: application/x-www-form-urlencoded' \
  --data ''
```

```ruby
require 'uri'
require 'net/http'
require 'openssl'

url = URI("https://my.testsms.com/api/v1/access-token")

http = Net::HTTP.new(url.host, url.port)
http.use_ssl = true
http.verify_mode = OpenSSL::SSL::VERIFY_NONE

request = Net::HTTP::Post.new(url)
request["content-type"] = 'application/x-www-form-urlencoded'
request["accept"] = 'application/json'

response = http.request(request)
puts response.read_body
```

```python
import http.client

conn = http.client.HTTPSConnection("my.testsms.com")

payload = ""

headers = {
    'content-type': "application/x-www-form-urlencoded",
    'accept': "application/json"
    }

conn.request("POST", "/api/v1/access-token", payload, headers)

res = conn.getresponse()
data = res.read()

print(data.decode("utf-8"))
```

```go
package main

import (
	"fmt"
	"net/http"
	"io/ioutil"
)

func main() {

	url := "https://my.testsms.com/api/v1/access-token"

	req, _ := http.NewRequest("POST", url, nil)

	req.Header.Add("content-type", "application/x-www-form-urlencoded")
	req.Header.Add("accept", "application/json")

	res, _ := http.DefaultClient.Do(req)

	defer res.Body.Close()
	body, _ := ioutil.ReadAll(res.Body)

	fmt.Println(res)
	fmt.Println(string(body))

}
```

```java
HttpResponse<String> response = Unirest.post("https://my.testsms.com/api/v1/access-token")
  .header("content-type", "application/x-www-form-urlencoded")
  .header("accept", "application/json")
  .asString();
```

```csharp
var client = new RestClient("https://my.testsms.com/api/v1/access-token");
var request = new RestRequest(Method.POST);
request.AddHeader("content-type", "application/x-www-form-urlencoded");
request.AddHeader("accept", "application/json");
IRestResponse response = client.Execute(request);
```

```php
<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => "https://my.testsms.com/api/v1/access-token",
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => "",
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 30,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => "POST",
  CURLOPT_POSTFIELDS => "",
  CURLOPT_HTTPHEADER => array(
    "accept: application/json",
    "content-type: application/x-www-form-urlencoded"
  ),
));

$response = curl_exec($curl);
$err = curl_error($curl);

curl_close($curl);

if ($err) {
  echo "cURL Error #:" . $err;
} else {
  echo $response;
}
```

`POST /v1/access-token`

Send client credentials,client_id and client_secret, into client body to get Access Token. To create and manage API Keys use TestSMS portal. ![Generate API key](generateApiKey.jpg) Each application is assigned a **Client ID** upon creation. This is an alphanumeric string and it's the unique identifier for your application ( such as `q8fij2iug0CmgPLfTfG1tZGdTQyGaTUA` ). It cannot be modified and you will be using it in your application's code when you call Auth0 APIs. <br/>Another important piece of information is the **Client Secret**. Think of it as your application's password which must be kept confidential at all times. If anyone gains access to your Client Secret they can impersonate your application and access protected resources. <br/>Generate your Client Credentials using [TestSMS portal.](https://my.testsms.com)  <br/> <br/> Now that you have an access_token you can interact with your Test SMS account via the API. <br />To do so, you must simply append the access token to the header of any API request: <br />**Authorization:** `Bearer {access_token}` 

> Body parameter

```yaml
client_id: asDa987asdf987asdf098098df
client_secret: asDa987asdf987asdf098098dfoiupoiuyougliuyoqwer876EGSDFGSDFGfsd
grant_type: client_credentials

```

<h3 id="get-access-token-using-client-credentials-flow-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|object|false|none|
|» client_id|body|string|false|Use Client ID generated using TestSMS portal|
|» client_secret|body|string|false|Use Client Secret generated using TestSMS portal|
|» grant_type|body|string|false|Use Client Credentials flow|

> Example responses

> 200 Response

```json
{
  "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzUxMiJ9.eyJleHAiOjE1NjE4NDc5ODEsImlhdCI6MTU2MTc2MTU4MSwiZW1haWwiOiJtaW1hcmtvQGdtYWlsLmNvbSJ9.wxOmD0rUaK9yONHpcXuWO4VxkWktPB95ea8s_sK7Xe83-oyaP1hK8pjO1lUIPA9iMThgXH8NRCG4_uc0Z72oow",
  "expires_in": 86400,
  "token_type": "Bearer",
  "scope": "write read"
}
```

<h3 id="get-access-token-using-client-credentials-flow-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Access token|[TokenResponse](#schematokenresponse)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|User is not active or bad request|None|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|Credentials not correct|None|
|429|[Too Many Requests](https://tools.ietf.org/html/rfc6585#section-4)|Too many access token attempts|None|
|501|[Not Implemented](https://tools.ietf.org/html/rfc7231#section-6.6.2)|Internal Server Error|None|

<aside class="success">
This operation does not require authentication
</aside>

<h1 id="testsms-client-api-api-reference">API Reference</h1>

Business process could be described in 3 simple steps: <br /> <br />  1. Request available networks and test scenarios <br /> 2. Create one or more test. <br /> 3. Get test results with delays, statuses, real received message body, PDU ... <br />

## Get available networks

<a id="opIdnetworks"></a>

> Code samples

```shell
curl --request GET \
  --url https://my.testsms.com/api/v1/mccmnc \
  --header 'accept: application/json'
```

```ruby
require 'uri'
require 'net/http'
require 'openssl'

url = URI("https://my.testsms.com/api/v1/mccmnc")

http = Net::HTTP.new(url.host, url.port)
http.use_ssl = true
http.verify_mode = OpenSSL::SSL::VERIFY_NONE

request = Net::HTTP::Get.new(url)
request["accept"] = 'application/json'

response = http.request(request)
puts response.read_body
```

```python
import http.client

conn = http.client.HTTPSConnection("my.testsms.com")

headers = { 'accept': "application/json" }

conn.request("GET", "/api/v1/mccmnc", headers=headers)

res = conn.getresponse()
data = res.read()

print(data.decode("utf-8"))
```

```go
package main

import (
	"fmt"
	"net/http"
	"io/ioutil"
)

func main() {

	url := "https://my.testsms.com/api/v1/mccmnc"

	req, _ := http.NewRequest("GET", url, nil)

	req.Header.Add("accept", "application/json")

	res, _ := http.DefaultClient.Do(req)

	defer res.Body.Close()
	body, _ := ioutil.ReadAll(res.Body)

	fmt.Println(res)
	fmt.Println(string(body))

}
```

```java
HttpResponse<String> response = Unirest.get("https://my.testsms.com/api/v1/mccmnc")
  .header("accept", "application/json")
  .asString();
```

```csharp
var client = new RestClient("https://my.testsms.com/api/v1/mccmnc");
var request = new RestRequest(Method.GET);
request.AddHeader("accept", "application/json");
IRestResponse response = client.Execute(request);
```

```php
<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => "https://my.testsms.com/api/v1/mccmnc",
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => "",
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 30,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => "GET",
  CURLOPT_HTTPHEADER => array(
    "accept: application/json"
  ),
));

$response = curl_exec($curl);
$err = curl_error($curl);

curl_close($curl);

if ($err) {
  echo "cURL Error #:" . $err;
} else {
  echo $response;
}
```

`GET /v1/mccmnc`

Use to get available networks for test and all test scenarios including MNP (ported numbers).   From returned list, most important attributes are **mccmnc** and **mccmncOriginal** if exists. Param **mccmnc** is required for creating test for specific country and network operator. Param **mccmncOriginal**, if exists, represents that ported number is available for testing.   <br /> <aside class="notice"> **Note** that refreshing period of available operator networks for testing is few minutes. </aside>

> Example responses

> 200 Response

```json
[
  {
    "mccmnc": "20610",
    "country": "string",
    "region": "string",
    "countryCode": "string",
    "isoAlpha2": "string",
    "network": "string",
    "mccmncOriginal": "20603"
  }
]
```

<h3 id="get-available-networks-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Array of available test scenarios|Inline|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|Request Access Token|None|
|501|[Not Implemented](https://tools.ietf.org/html/rfc7231#section-6.6.2)|Internal Server Error|None|

<h3 id="get-available-networks-responseschema">Response Schema</h3>

Status Code **200**

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|[[MccmncResponse](#schemamccmncresponse)]|false|none|[Object contains available test scenario regarding mcc-mnc and mcc-mnc original]|
|» mccmnc|string|true|none|A PLMN is identified by a globally unique PLMN code, which consists of a MCC (Mobile Country Code) and MNC (Mobile Network Code)|
|» country|string|false|none|none|
|» region|string|false|none|none|
|» countryCode|string|false|none|none|
|» isoAlpha2|string|false|none|none|
|» network|string|false|none|none|
|» mccmncOriginal|string|false|none|Represent originally ported from PLNM value|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
None ( Scopes: read:networks )
</aside>

## Create tests

<a id="opIdcreateTest"></a>

> Code samples

```shell
curl --request POST \
  --url https://my.testsms.com/api/v1/createTest \
  --header 'accept: application/json' \
  --header 'content-type: application/json' \
  --data '{"callbackUrl":"https://myserverdomain/api/sms-callback-results","networks":[{"mccmnc":"22201"},{"mccmnc":"22208","messageIdTemplate":"[g-code]"},{"mccmnc":"22201","mccmncOriginal":"22299","messageIdTemplate":"[pass7]"},{"externalMsisdn":"3936622667777"}]}'
```

```ruby
require 'uri'
require 'net/http'
require 'openssl'

url = URI("https://my.testsms.com/api/v1/createTest")

http = Net::HTTP.new(url.host, url.port)
http.use_ssl = true
http.verify_mode = OpenSSL::SSL::VERIFY_NONE

request = Net::HTTP::Post.new(url)
request["content-type"] = 'application/json'
request["accept"] = 'application/json'
request.body = "{\"callbackUrl\":\"https://myserverdomain/api/sms-callback-results\",\"networks\":[{\"mccmnc\":\"22201\"},{\"mccmnc\":\"22208\",\"messageIdTemplate\":\"[g-code]\"},{\"mccmnc\":\"22201\",\"mccmncOriginal\":\"22299\",\"messageIdTemplate\":\"[pass7]\"},{\"externalMsisdn\":\"3936622667777\"}]}"

response = http.request(request)
puts response.read_body
```

```python
import http.client

conn = http.client.HTTPSConnection("my.testsms.com")

payload = "{\"callbackUrl\":\"https://myserverdomain/api/sms-callback-results\",\"networks\":[{\"mccmnc\":\"22201\"},{\"mccmnc\":\"22208\",\"messageIdTemplate\":\"[g-code]\"},{\"mccmnc\":\"22201\",\"mccmncOriginal\":\"22299\",\"messageIdTemplate\":\"[pass7]\"},{\"externalMsisdn\":\"3936622667777\"}]}"

headers = {
    'content-type': "application/json",
    'accept': "application/json"
    }

conn.request("POST", "/api/v1/createTest", payload, headers)

res = conn.getresponse()
data = res.read()

print(data.decode("utf-8"))
```

```go
package main

import (
	"fmt"
	"strings"
	"net/http"
	"io/ioutil"
)

func main() {

	url := "https://my.testsms.com/api/v1/createTest"

	payload := strings.NewReader("{\"callbackUrl\":\"https://myserverdomain/api/sms-callback-results\",\"networks\":[{\"mccmnc\":\"22201\"},{\"mccmnc\":\"22208\",\"messageIdTemplate\":\"[g-code]\"},{\"mccmnc\":\"22201\",\"mccmncOriginal\":\"22299\",\"messageIdTemplate\":\"[pass7]\"},{\"externalMsisdn\":\"3936622667777\"}]}")

	req, _ := http.NewRequest("POST", url, payload)

	req.Header.Add("content-type", "application/json")
	req.Header.Add("accept", "application/json")

	res, _ := http.DefaultClient.Do(req)

	defer res.Body.Close()
	body, _ := ioutil.ReadAll(res.Body)

	fmt.Println(res)
	fmt.Println(string(body))

}
```

```java
HttpResponse<String> response = Unirest.post("https://my.testsms.com/api/v1/createTest")
  .header("content-type", "application/json")
  .header("accept", "application/json")
  .body("{\"callbackUrl\":\"https://myserverdomain/api/sms-callback-results\",\"networks\":[{\"mccmnc\":\"22201\"},{\"mccmnc\":\"22208\",\"messageIdTemplate\":\"[g-code]\"},{\"mccmnc\":\"22201\",\"mccmncOriginal\":\"22299\",\"messageIdTemplate\":\"[pass7]\"},{\"externalMsisdn\":\"3936622667777\"}]}")
  .asString();
```

```csharp
var client = new RestClient("https://my.testsms.com/api/v1/createTest");
var request = new RestRequest(Method.POST);
request.AddHeader("content-type", "application/json");
request.AddHeader("accept", "application/json");
request.AddParameter("application/json", "{\"callbackUrl\":\"https://myserverdomain/api/sms-callback-results\",\"networks\":[{\"mccmnc\":\"22201\"},{\"mccmnc\":\"22208\",\"messageIdTemplate\":\"[g-code]\"},{\"mccmnc\":\"22201\",\"mccmncOriginal\":\"22299\",\"messageIdTemplate\":\"[pass7]\"},{\"externalMsisdn\":\"3936622667777\"}]}", ParameterType.RequestBody);
IRestResponse response = client.Execute(request);
```

```php
<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => "https://my.testsms.com/api/v1/createTest",
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => "",
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 30,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => "POST",
  CURLOPT_POSTFIELDS => "{\"callbackUrl\":\"https://myserverdomain/api/sms-callback-results\",\"networks\":[{\"mccmnc\":\"22201\"},{\"mccmnc\":\"22208\",\"messageIdTemplate\":\"[g-code]\"},{\"mccmnc\":\"22201\",\"mccmncOriginal\":\"22299\",\"messageIdTemplate\":\"[pass7]\"},{\"externalMsisdn\":\"3936622667777\"}]}",
  CURLOPT_HTTPHEADER => array(
    "accept: application/json",
    "content-type: application/json"
  ),
));

$response = curl_exec($curl);
$err = curl_error($curl);

curl_close($curl);

if ($err) {
  echo "cURL Error #:" . $err;
} else {
  echo $response;
}
```

`POST /v1/createTest`

Post networks, array of mccmnc to get phone numbers for test or use external number, your own numbers, to create test. <br /> Be sure that sent networks are from recent call to `/v1/mccmnc` API, so all requested networks have online numbers. Each created test contains **id, messageId, msisdn**. <br/> To test your route send text that contains **messageId** to **msisdn (phone number)**. Get results of each test using **id** in `/v1/smsTest/{id}` API call.  You can also test **UDH (User Data Header)** in your test, e.g if you like to test concatenated message or send message to specific port. <br /> Set **callbackUrl** as your endpoint, so our service can send you immediate response of tested cases.  Results for tests created using API could be forwarded out to your system using **callbackUrl**  that you defined in createTest request. When our system got test results from device that info will  be send immediately as POST request with **JSON payload** to **callbackUrl** and you don't  need to make another request to check test results by ID (`GET /v1/smsTest/{id}`).  Please find more info about JSON payload [here](https://testsms.com/docs/api/index.html#tocSsmstestresponse) <br/> <br/> Use optional parameter **externalMsisdn** if you would like to create test to specific number,  usually your own number. Do not expect results for tests with external numbers, that could be any your number without possibility to send data to our servers. If specify parameter **externalMsisdn** entered, other params ,like `mccmnc` in request body will be ignored. <br/> Format for external number is `[country code][area code][local phone number]`. <br/><br/> **Examples:** 4499274098712, 543513809889. Note that **missing sign** + from phone number format. <br/> <br/> Optional parameter **messageIdTemplate** could be used if you need different type of messageId. Available templates are `[g-code], [code], [code6],[code7]..[code9], [pass], [pass6],[pass7]..[pass20]`. <br/>  <h3>How to use <span style="color: var(--lumo-primary-text-color) ">[code] </span> placeholder in SMS text message</h3><p> Placeholder <code>[code]</code> should be replaced with random 5 digits into your text message. Use it to simulate PIN, OTP or any kind of digit verification code. For longer digit code use <code>[code6], [code7] .. [code9]</code>. For specific Google code, use <code>[g-code]</code> placeholder. <br/> <br/> **Examples:** </p><p>"Hello, your code is <b>[code]</b>." <br/>"Hello, your code is <b>59674</b>".</p><p>"Enter 8 digit code, <b>[code8]</b>, to verify account. "<br/> "Enter 8 digit code, <b>76237802</b>, to verify account.</p><p>"Your google verification is <b>[g-code]</b> number." <br/> "Your google verification is <b>G-448232</b> number."</p><h3>How to use <span style="color: var(--lumo-primary-text-color) ">[pass]</span> placeholder in SMS text message</h3><p> Placeholder <code>[pass]</code> should be replaced with 8 alphanumeric into your text message. Use it to simulate random password or other secret. If you need different lenght of password use <code>[pass5], [pass6] .. [pass20]</code>. <br/> <br/> **Examples:** </p><p>"Hello, your new password is <b>[pass]</b>. Please change password after first login" <br/> "Hello, your new password is <b>jkh54p2s</b>. Please change password after first login".</p><p>"Your verification code is <b>[pass10]</b>. " <br/> "Your verification code is <b>udp9pk40vy</b>." </p><p>"Tap on link https://ig.me/verify/<b>[pass13]</b> to verify your Instagram account. "<br/> "Tap on link https://ig.me/verify/<b>gdimnb67ns5l4e</b> to verify your Instagram account."</p><p>Placeholders <code>[code], [pass]</code> could be combined but only one will be used as MessageId to identify specific test.  With combination you are free to simulate any kind of text message like short link, UUID or some text that usually used by Facebook, Twitter, Instagram etc. </p>

> Body parameter

```json
{
  "callbackUrl": "https://myserverdomain/api/sms-callback-results",
  "networks": [
    {
      "mccmnc": "22201"
    },
    {
      "mccmnc": "22208",
      "messageIdTemplate": "[g-code]"
    },
    {
      "mccmnc": "22201",
      "mccmncOriginal": "22299",
      "messageIdTemplate": "[pass7]"
    },
    {
      "externalMsisdn": "3936622667777"
    }
  ]
}
```

<h3 id="create-tests-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[CreateTestsRequest](#schemacreatetestsrequest)|true|Post networks, array of mccmnc, mccmncOriginal, externalMsisdn callbackUrl to get phone numbers for tests|

> Example responses

> 200 Response

```json
[
  {
    "phoneNumbers": [
      {
        "id": 524232,
        "messageId": "fsdgf3fawcai",
        "msisdn": "4499274098712"
      }
    ]
  }
]
```

<h3 id="create-tests-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|none|Inline|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Check if json format is right <br/>Networks can't be empty <br />Purchase credits in app|None|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|Request Access Token|None|
|501|[Not Implemented](https://tools.ietf.org/html/rfc7231#section-6.6.2)|Internal Server Error|None|

<h3 id="create-tests-responseschema">Response Schema</h3>

Status Code **200**

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|[[CreateTestResponse](#schemacreatetestresponse)]|false|none|none|
|» phoneNumbers|[[CreateTestMsisdn](#schemacreatetestmsisdn)]|false|none|[Contains data of created test. ]|
|»» id|integer(int64)|true|none|Represent ID for test case. Use it to call API to get result for.|
|»» messageId|string|false|none|Alphanumeric code unique for each test case.  Must be included into SMS body. Format of messageId could be different if that specified into createTest request.|
|»» msisdn|string|false|none|Phone number for requested network (MCCMNC) for test.|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
None ( Scopes: write:test )
</aside>

## Get sms test result

<a id="opIdgetSmsTestById"></a>

> Code samples

```shell
curl --request GET \
  --url https://my.testsms.com/api/v1/smsTest/58237 \
  --header 'accept: application/json'
```

```ruby
require 'uri'
require 'net/http'
require 'openssl'

url = URI("https://my.testsms.com/api/v1/smsTest/58237")

http = Net::HTTP.new(url.host, url.port)
http.use_ssl = true
http.verify_mode = OpenSSL::SSL::VERIFY_NONE

request = Net::HTTP::Get.new(url)
request["accept"] = 'application/json'

response = http.request(request)
puts response.read_body
```

```python
import http.client

conn = http.client.HTTPSConnection("my.testsms.com")

headers = { 'accept': "application/json" }

conn.request("GET", "/api/v1/smsTest/58237", headers=headers)

res = conn.getresponse()
data = res.read()

print(data.decode("utf-8"))
```

```go
package main

import (
	"fmt"
	"net/http"
	"io/ioutil"
)

func main() {

	url := "https://my.testsms.com/api/v1/smsTest/58237"

	req, _ := http.NewRequest("GET", url, nil)

	req.Header.Add("accept", "application/json")

	res, _ := http.DefaultClient.Do(req)

	defer res.Body.Close()
	body, _ := ioutil.ReadAll(res.Body)

	fmt.Println(res)
	fmt.Println(string(body))

}
```

```java
HttpResponse<String> response = Unirest.get("https://my.testsms.com/api/v1/smsTest/58237")
  .header("accept", "application/json")
  .asString();
```

```csharp
var client = new RestClient("https://my.testsms.com/api/v1/smsTest/58237");
var request = new RestRequest(Method.GET);
request.AddHeader("accept", "application/json");
IRestResponse response = client.Execute(request);
```

```php
<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => "https://my.testsms.com/api/v1/smsTest/58237",
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => "",
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 30,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => "GET",
  CURLOPT_HTTPHEADER => array(
    "accept: application/json"
  ),
));

$response = curl_exec($curl);
$err = curl_error($curl);

curl_close($curl);

if ($err) {
  echo "cURL Error #:" . $err;
} else {
  echo $response;
}
```

`GET /v1/smsTest/{id}`

Get result to check route quality and network availability. Param **receiptStatus** used to explain how SMS arrived on device. Values for ** receiptStatus** are WAIT(0), POSITIVE(1), NEGATIVE(5). Note that our system is waiting for sms up to 2 hours and than automatically set NEGATIVE status.

<h3 id="get-sms-test-result-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|id|path|integer(int64)|true|Represent test ID|

> Example responses

> default Response

```json
{
  "createdOn": "2019-08-24T14:15:22Z",
  "mccMnc": "20610",
  "mccMncPorted": "20603",
  "deliveredSender": "Verify",
  "deliveredText": "trwvu&sryu4o is your verification code",
  "phone": "1555765435",
  "messageId": "trwvu&sryu4o",
  "callbackUrl": "http://example.com/testSmsCallbackUrl",
  "receiptTime": "2019-08-24T14:15:22Z",
  "receiptStatus": "POSITIVE",
  "pdu": "07917283010010F5040BC87238880900F100009930925161958003C16010",
  "scts": "2019-08-24T14:15:22Z",
  "scn": "Orange Belgium",
  "arrivalTs": "2019-08-24T14:15:22Z"
}
```

<h3 id="get-sms-test-result-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|default|Default|Result of single test|[SmsTestResponse](#schemasmstestresponse)|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
None ( Scopes: read:test )
</aside>

# Schemas

<h2 id="tocS_CreateTest">CreateTest</h2>
<!-- backwards compatibility -->
<a id="schemacreatetest"></a>
<a id="schema_CreateTest"></a>
<a id="tocScreatetest"></a>
<a id="tocscreatetest"></a>

```json
[
  {
    "mccmnc": "22201"
  },
  {
    "mccmnc": "22208",
    "messageIdTemplate": "[g-code]"
  },
  {
    "mccmnc": "22201",
    "mccmncOriginal": "22299",
    "messageIdTemplate": "[pass7]"
  },
  {
    "externalMsisdn": "3936622667777"
  }
]

```

Object contains params to create tests, like mccmnc and optionally original mccmnc, external number or messageId template

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|mccmnc|string|true|none|Enter MCCMNC network code to get phone number for test|
|mccmncOriginal|string|false|none|Enter MCCMNC original network code to get phone number for testing ported scenario|
|externalMsisdn|string|false|none|Enter you own phone number to create test. Other params will be ignored if externalMsisdn exists. Format E.164 without + prefix.|
|messageIdTemplate|string|false|none|Optionally choose how should look messageId. Available templates are [g-code],[code],[code6],[pass],[pass7] etc.|

<h2 id="tocS_TokenResponse">TokenResponse</h2>
<!-- backwards compatibility -->
<a id="schematokenresponse"></a>
<a id="schema_TokenResponse"></a>
<a id="tocStokenresponse"></a>
<a id="tocstokenresponse"></a>

```json
{
  "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzUxMiJ9.eyJleHAiOjE1NjE4NDc5ODEsImlhdCI6MTU2MTc2MTU4MSwiZW1haWwiOiJtaW1hcmtvQGdtYWlsLmNvbSJ9.wxOmD0rUaK9yONHpcXuWO4VxkWktPB95ea8s_sK7Xe83-oyaP1hK8pjO1lUIPA9iMThgXH8NRCG4_uc0Z72oow",
  "expires_in": 86400,
  "token_type": "Bearer",
  "scope": "write read"
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|access_token|string|false|none|An authorization credential, in the form of an JWT, used to access an API.|
|expires_in|integer(int64)|false|none|By default, an Access Token for  API is valid for 86400 seconds (24 hours).|
|token_type|string|false|none|The client must send this token in the Authorization header when making requests to protected resources: Authorization: Bearer <token>|
|scope|string|false|none|none|

<h2 id="tocS_CreateTestResponse">CreateTestResponse</h2>
<!-- backwards compatibility -->
<a id="schemacreatetestresponse"></a>
<a id="schema_CreateTestResponse"></a>
<a id="tocScreatetestresponse"></a>
<a id="tocscreatetestresponse"></a>

```json
{
  "phoneNumbers": [
    {
      "id": 524232,
      "messageId": "fsdgf3fawcai",
      "msisdn": "4499274098712"
    }
  ]
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|phoneNumbers|[[CreateTestMsisdn](#schemacreatetestmsisdn)]|false|none|[Contains data of created test. ]|

<h2 id="tocS_CreateTestMsisdn">CreateTestMsisdn</h2>
<!-- backwards compatibility -->
<a id="schemacreatetestmsisdn"></a>
<a id="schema_CreateTestMsisdn"></a>
<a id="tocScreatetestmsisdn"></a>
<a id="tocscreatetestmsisdn"></a>

```json
{
  "id": 524232,
  "messageId": "fsdgf3fawcai",
  "msisdn": "4499274098712"
}

```

Contains data of created test. 

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|id|integer(int64)|true|none|Represent ID for test case. Use it to call API to get result for.|
|messageId|string|false|none|Alphanumeric code unique for each test case.  Must be included into SMS body. Format of messageId could be different if that specified into createTest request.|
|msisdn|string|false|none|Phone number for requested network (MCCMNC) for test.|

<h2 id="tocS_SmsTestResponse">SmsTestResponse</h2>
<!-- backwards compatibility -->
<a id="schemasmstestresponse"></a>
<a id="schema_SmsTestResponse"></a>
<a id="tocSsmstestresponse"></a>
<a id="tocssmstestresponse"></a>

```json
{
  "createdOn": "2019-08-24T14:15:22Z",
  "mccMnc": "20610",
  "mccMncPorted": "20603",
  "deliveredSender": "Verify",
  "deliveredText": "trwvu&sryu4o is your verification code",
  "phone": "1555765435",
  "messageId": "trwvu&sryu4o",
  "callbackUrl": "http://example.com/testSmsCallbackUrl",
  "receiptTime": "2019-08-24T14:15:22Z",
  "receiptStatus": "POSITIVE",
  "pdu": "07917283010010F5040BC87238880900F100009930925161958003C16010",
  "scts": "2019-08-24T14:15:22Z",
  "scn": "Orange Belgium",
  "arrivalTs": "2019-08-24T14:15:22Z"
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|createdOn|string(date-time)|false|none|Date time of created test in UTC. Format: yyyy-MM-dd'T'HH:mm:ss.SSSZ|
|mccMnc|string|false|none|A PLMN is identified by a globally unique PLMN code, which consists of a MCC (Mobile Country Code) and MNC (Mobile Network Code)|
|mccMncPorted|string|false|none|Represent originally ported from PLNM value|
|deliveredSender|string|false|none|Sender ID delivered to device|
|deliveredText|string|false|none|Message body delivered to device|
|phone|string|false|none|MSISDN for testing|
|messageId|string|false|none|Alphanumeric code included into message body|
|callbackUrl|string|false|none|Your endpoint where you expect test SMS results|
|receiptTime|string(date-time)|false|none|Received time on device in UTC. Format: yyyy-MM-dd'T'HH:mm:ss.SSSZ|
|receiptStatus|string|false|none|Receipt status|
|pdu|string|false|none|The PDU string contains not only the message, but also a lot of meta-information about the sender, his SMS service center, the time stamp etc. It is all in the form of hexa-decimal octets or decimal semi-octets.|
|scts|string(date-time)|false|none|Service center time in UTC. Format: yyyy-MM-dd'T'HH:mm:ss.SSSZ|
|scn|string|false|none|Service center name|
|arrivalTs|string(date-time)|false|none|Message arrival. Format: yyyy-MM-dd'T'HH:mm:ss.SSSZ|

#### Enumerated Values

|Property|Value|
|---|---|
|receiptStatus|RECEIVED|
|receiptStatus|WAIT|
|receiptStatus|POSITIVE|
|receiptStatus|TEXT_OR_SENDER_REPLACED|
|receiptStatus|NEGATIVE|
|receiptStatus|EXTERNAL|
|receiptStatus|WAIT(0), POSITIVE(1), NUM_NOT_AVAILABLE(2), NUM_OFFLINE(3), TEXT_OR_SENDER_REPLACED(4), NEGATIVE(5)|

<h2 id="tocS_LoginRequest">LoginRequest</h2>
<!-- backwards compatibility -->
<a id="schemaloginrequest"></a>
<a id="schema_LoginRequest"></a>
<a id="tocSloginrequest"></a>
<a id="tocsloginrequest"></a>

```json
{
  "email": "name@comapny.com",
  "password": "******"
}

```

Your credentials for accessing TestSMS API

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|email|string|true|none|Email that you registered for TestSMS portal|
|password|string|true|none|Your password for TestSMS portal|

<h2 id="tocS_MccmncResponse">MccmncResponse</h2>
<!-- backwards compatibility -->
<a id="schemamccmncresponse"></a>
<a id="schema_MccmncResponse"></a>
<a id="tocSmccmncresponse"></a>
<a id="tocsmccmncresponse"></a>

```json
{
  "mccmnc": "20610",
  "country": "string",
  "region": "string",
  "countryCode": "string",
  "isoAlpha2": "string",
  "network": "string",
  "mccmncOriginal": "20603"
}

```

Object contains available test scenario regarding mcc-mnc and mcc-mnc original

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|mccmnc|string|true|none|A PLMN is identified by a globally unique PLMN code, which consists of a MCC (Mobile Country Code) and MNC (Mobile Network Code)|
|country|string|false|none|none|
|region|string|false|none|none|
|countryCode|string|false|none|none|
|isoAlpha2|string|false|none|none|
|network|string|false|none|none|
|mccmncOriginal|string|false|none|Represent originally ported from PLNM value|

<h2 id="tocS_CreateTestsRequest">CreateTestsRequest</h2>
<!-- backwards compatibility -->
<a id="schemacreatetestsrequest"></a>
<a id="schema_CreateTestsRequest"></a>
<a id="tocScreatetestsrequest"></a>
<a id="tocscreatetestsrequest"></a>

```json
{
  "callbackUrl": "https://myserverdomain/api/sms-callback-results",
  "networks": [
    {
      "mccmnc": "22201"
    },
    {
      "mccmnc": "22208",
      "messageIdTemplate": "[g-code]"
    },
    {
      "mccmnc": "22201",
      "mccmncOriginal": "22299",
      "messageIdTemplate": "[pass7]"
    },
    {
      "externalMsisdn": "3936622667777"
    }
  ]
}

```

Object contains array of networks requested for create test

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|callbackUrl|string|false|none|Optionally specify your endpoint to get test results|
|networks|[[CreateTest](#schemacreatetest)]|true|none|Enter array of networks to create test cases.|

