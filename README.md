# Cloudflare-Grafana
Grafana Dashboard that shows Cloudflare Overviews and Analytics from the RESTful API

## Configuration Cloudflare
The preferered authentication method is to use API Tokens.

On your Cloudflare Profile go inside API Tokens menu.

Create a new Token using the Read analytics and logs template: 
![image](https://github.com/pokertour/Cloudflare-Grafana/assets/7757451/b51c9602-99e3-448c-9589-19e66497ff5a)
![image](https://github.com/pokertour/Cloudflare-Grafana/assets/7757451/83524363-06e5-4b0f-98f1-b58220220b1e)

Leave all the field by default. You can add a IP Filtering if you want and a TTL aswell.

Continue to summary and you should have this permissions :
![image](https://github.com/pokertour/Cloudflare-Grafana/assets/7757451/605b8099-f65c-406f-9893-1da1e48f05cc)

Create the token and place it in the script on the setting : cloudflareapitoken


## Configuration Script
Place the script where you want, there is no importance.

change the Configuration section within your details :
```
##
# Configurations
##
# Endpoint URL for InfluxDB
InfluxDBURL="YOURINFLUXSERVERIP" #Your InfluxDB Server, http://FQDN or https://FQDN if using SSL
InfluxDBPort="8086" #Default Port
InfluxBucket="YOURINFLUXBUCKETNAME" #Default Database
InfluxOrg="YOURINFLUXORG"
InfluxToken="YOURINFLUXTOKEN"

# Endpoint URL for login action
cloudflareauthmethod="TOKEN/APIKEY" #Choose Authentication method. Either TOKEN (single token with specific rights) or APIKEY (Global API KEY with Email)
cloudflareapikey="YOURAPIKEY"
cloudflarezone="YOURZONEID"
cloudflareemail="YOUREMAIL"
cloudflareapitoken="YOURTOKEN"
```

Once the changes are done, make the script executable with chmod:

```
chmod +x cloudflare-analytics.sh
```

The output of the command should be something like the next, without errors:
```
HTTP/1.1 204 No Content
Content-Type: application/json
Request-Id: b084ba16-8622-11ea-8dbc-0050569002da
X-Influxdb-Build: OSS
X-Influxdb-Version: 1.7.10
X-Request-Id: b084ba16-8622-11ea-8dbc-0050569002da
Date: Fri, 24 Apr 2020 11:56:53 GMT
```
If so, please now add this script to your crontab, like for example everyday at 9am:
```
0 9 * * * /home/user/cloudflare-analytics.sh >> /var/log/cloudflare.log 2>&1
```

## Configuration InfluxDb
You should create a specific bucket with a specific token with read/write permission on the bucket.

## Configuration Grafana
You must add a Data Sources to the influxDB bucket.
You must set the Query language to Flux.

You can import the dashboard from Grafana website : https://grafana.com/grafana/dashboards/20682-cloudflare-analytics-and-overview/
ID : 20682

# Known Bug
- The Geomap panel is not displaying informations. If you know how to do please add a pull request.

# Planned Features
- Possibility to have multizone
