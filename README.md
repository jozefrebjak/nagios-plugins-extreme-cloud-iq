# check_ap_status

With this plugin you can get status of your AP's connected to the ExtremeCloud IQ (formerly Aerohive).

- Firstly you will be need to go to [developer portal](https://developer.aerohive.com) to register your application. Register and sign in.
- There is a [video](https://youtu.be/1dhP-QGoizg) about how to get working API app.

If you will have all needed then just copy it to `check_ap_status` shell script into variables section.

```
#Variables
ENDPOINT="YOUR_ENDPOINT" # For example https://cloud-fra.aerohive.com
OWNER_ID="YOUR_OWNER_ID" 
AUTH="Bearer YOUR_AUTH_TOKEN" # Access Token
ID="YOUR_ID" # Client ID
URI="YOUR_URI" # Redirect URL
SECRET="YOUR_SECRET" # Client Secret
```

Then just run script with a hostname of your AP. For example: `./check_ap_status.sh AP01`

If is your AP **up** then you will get message like:

```
OK: AP_650X is connected to the Cloud. Uptime: 79 days 06 hours 05 minutes 12 seconds|Status=1;;0;1;
```

Uptime is there because I want to know if AP was restarted or just lost connection to the cloud. 

If is your AP **down** then you will get message like:

```
CRITICAL: AP_650X is not connected to the Cloud.|Status=0;;0;1;
```

This script also has a support of perf data so you can get nice graphs.


![check_ap_status Graph](/screenshots/check_ap_status_graph.png)
