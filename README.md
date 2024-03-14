# Cloudflare-Grafana
Grafana Dashboard that shows Cloudflare Overviews and Analytics from the RESTful API

## Configuration InfluxDb
You should create a specific bucket with a specific token with read/write permission on the bucket.

## Configuration Grafana
You must add a Data Sources to the influxDB bucket.
You must set the Query language to Flux.

You can import the dashboard

# Known Bug
- The Geomap panel is not displaying informations. If you know how to do please add a pull request.
