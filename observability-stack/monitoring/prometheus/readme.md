# Prometheus Application Monitoring

## Start Prometheus, Grafana

docker-compose up -d prometheus
docker-compose up -d grafana



## Start the example app

docker-compose up -d --build nodejs-application


## Generate some requests by opening the application in the browser

http://localhost:83


## Check Dashboards

http://localhost:3000

# If this application to be run using prometheus operator in kubernetes then

Go to DeployAppUsingOperator folder.


