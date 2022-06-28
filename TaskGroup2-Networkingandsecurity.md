## Scenario: grafana + prometheus is in public or different subnet then host machines or sources

Assuming the grafana + prometheus is in subnet A (might be public or private) and sources machines like application server, db servers and others are in subnet B which is obviously privaye and does not have a direct connection.

### Solutions

1. We can use the combination of  bastion host  and agents which has all the access and can ship data acroos subnets and have access to the internet.
2. Install prometheus agent in host servers and fetch the data in graphana dashboard, Scrape Prometheus sources and import metrics.
3. Use the bastion host to fetch the metrics of host servers and save it to external disk or safer place which is autonomously used to metrics only and provide access to grafana + prometheus servers for better monitoring.
4. Prometheus configuration can register the targets in YAML configuration file. 
5. Public cloud has the ability to use the monitoring agents and inject them in servers even they are in different networks they used the routings and different gateways architecture to make the system less coupled.



### QS: What could it mean if no metrics are available for a lengthy period of time?
####      We will loose the ability to moniter the behaviour of the system/infra and metrics with proper messures. Lesser the time period more the data frequency and more the data stored in prometheus server then accuracy curve can be found to gather correctness about system health checks.
