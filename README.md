# safAuthorize

<h1>Generating Access token - Daraja API</h1>

### Create an app
Ideally, you'd need to create an app by heading to [safaricom daraja 2.0 wesbite](https://developer.safaricom.co.ke/MyApps/)

### Identify the consumer key and consumer secret
* The App you created will generate the `consumer key` and `consumer secret` that you'll need to generate an Oauth access token necessary for authorizing requests.
![Location of the two credentials](![image](https://github.com/BaronKimaru/safAuthorize/assets/16536231/b78687ce-e0d9-48bd-82c8-881fc4f46b59))

* The required string, i.e., the BasicAuth string, refers to a base64 encoded string of the two aforementoned credentials above.
  
* Basically, you'd have to do this inorder to do a Base-64 encoding of the two:
```
Consumer Key + ":" + Consumer Secret
```
An example of a base64 encoded ctrsing can be generated from the bas64 website
![image](![image](https://github.com/BaronKimaru/safAuthorize/assets/16536231/a6737a3d-1957-4872-b479-49960c3c09be))

An example if using Python would be:
```
result = os.getenv("SAF_CONS_KEY") + ":" + os.getenv("SAF_CONS_SECRET")
result_byte_data = result.encode('utf-8')
result_encoded_data = base64.b64encode(result_byte_data)
result_encoded_data_str = result_encoded_data.decode('utf-8')

result_encoded_data = base64.b64encode(result_byte_data)
api_URL = "https://sandbox.safaricom.co.ke/oauth/v1/generate?grant_type=client_credentials"
response = requests.request(
            "GET", 
            api_URL,
            headers = {
                'Authorization': f'Basic {result_encoded_data_str}'
                }
        )
formatted_response = json.loads(response.text.encode('utf8'))
token = formatted_response['access_token']
```
