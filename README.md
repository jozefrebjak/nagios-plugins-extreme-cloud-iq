![ExtremeCloud IQ](https://www.extremenetworks.com/wp-content/uploads/2019/10/xIQ.screen.01_new-1.png)

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

You can setup nagios service to check status of AP like:

```
# Check AP Status via Cloud API
define service {
  service_description            Status
  hostgroup_name                 YOUR_HOSTGROUP
# servicegroups			             ExtremeCloud-IQ-Status # I'm using also servicegroups
  use                            generic-service,srv-perf # I'm using OMD with Graphana, so I am using srv-perf for graphing 
  check_command                  check_ap
}
```

And there is a command.

```
define command {
  command_name                   check_ap
  command_line                   $USER1$/check_ap_status.sh $HOSTALIAS$ # I'm using $HOSTALIAS$. You can use directly $HOSTNAME$
}
```


This is how service looks like in a Thruk UI.

![check_ap_status Service](/screenshots/check_ap_status_nagios_service.png)


This script also has a support of perf data so you can get nice graphs.


![check_ap_status Graph](/screenshots/check_ap_status_graph.png)
