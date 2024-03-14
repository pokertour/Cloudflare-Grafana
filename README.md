# Cloudflare-Grafana
Grafana Dashboard that shows Cloudflare Overviews and Analytics from the RESTful API

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
