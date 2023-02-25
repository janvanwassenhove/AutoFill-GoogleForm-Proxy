# AutoFill-GoogleForm-Proxy

### Introduction
To test your google forms, mutiple times, with different email address cycling through different proxys.

### Initial Setup 
To setup the script, two main options need to be set up:
- the forms url
- the form variables

Additionally, if your local IP cannot be used, you can configure proxy usage.

##### The Forms URL
Change the URL of google form by replacing '/viewform' at the end of the URL with 'formResponse'. 
Now, your URL should look like this: https://docs.google.com/forms/d/<form_id>/formResponse <br/>
or https://docs.google.com/forms/d/e/<form_id>/formResponse .

##### The Form Variables
To retrieve the form variables, just open the google form in chrome and start inspecting.

The easiest way is to start a network recording when posting the form.
You can do this using the chrome developers tools (Ctrl + Shift + I).
Go to the 'network' tab, start recording, fill in the form (& submit) and finally stop the recording.
Now you'll be able to inspect the formResponse (POST) request.
While selecting formResponse, go to 'Payload' & choose 'Form Data'.

Here you'll find the form fields you'll need.
They will look like 'entry.123456' or 'emailAddress'.
Depending on your needs, you can add/adjust these entries in the GoogleForms.PY script, within the 'get_values' function.

##### Proxy
Additionally, for Proxy setup, if you need to circle your IP address, cf. 'Using a proxy'

### Running the auto form fill script

To simply run it:

`python GoogleForms.py`

Optionally following variables can be manipulated;

| Variable name    | Type    | Default value | Description                                                                                                        |
|------------------|---------|---------------|--------------------------------------------------------------------------------------------------------------------|
| viaProxy         | Boolean | False         | If not activated, form will be filled using the current IP.<br/> If True, the request will go via Proxy            |
| numberOfRequests | Integer | 2             | The amount of times you want the request te be excuted.                                                            |
|    scrambled              | Boolean | False         | If False, more 'human' names for generating the username will be used. If True, scrambled characters will be used. |

In practice, if you want to go via a proxy (different IP's) and do this 5 times in a row:

`python GoogleForms.py --viaProxy=True --numberOfRequests=5`

### Using a proxy
To retrieve a list of available proxies, the API https://api.proxyscrape.com/v2/ is used 
(to use another API you'll need to change the urlProxies variable within the script). 
The code will circle through the list, attempting to submit a form via the available proxy.
By default, proxy usage is not active and local IP is used.
You can activate it running:

`python GoogleForms.py --viaProxy=True`

### Simple Email generation
The email generation is based on my other code example https://github.com/janvanwassenhove/EmailGeneration
