# monitoring
Used the following helm charts 

Grafana - > https://grafana.github.io/helm-charts
prometheus -> https://github.com/prometheus-community/helm-charts

**Installing prometheus **

Add the helm repo to your local machine 
1. helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
Once repo is ready we can install the prometheus 
2. helm install prometheus prometheus-community/prometheus

To access the prometheus use the following command 
#export POD_NAME=$(kubectl get pods --namespace default -l "app=prometheus,component=server" -o jsonpath="{.items[0].metadata.name}")
#kubectl --namespace default port-forward $POD_NAME 9090

**Installing grafana**

Add the repo 

1. helm repo add grafana https://grafana.github.io/helm-charts
2. helm install grafana stable/grafana
3. kubectl expose service grafana --type=NodePort --target-port=3000 --name=grafana-np


1. Get your 'admin' user password by running

   kubectl get secret --namespace default grafana -o jsonpath="{.data.admin-password}" | base64 --decode ; echo

2. The Grafana server can be accessed via port 80 on the following DNS name from within your cluster:

   grafana.default.svc.cluster.local

   Get the Grafana URL to visit by running these commands in the same shell:

   export POD_NAME_GF=$(kubectl get pods --namespace default -l "app.kubernetes.io/name=grafana,app.kubernetes.io/instance=grafana" -o jsonpath="{.items[0].metadata.name}")
     kubectl --namespace default port-forward $POD_NAME_GF 3000
 
3. Access the UI on http://localhost:3000

--------------------------------------------------------------------------


**Add datasource in grafana**

1. Go setting in the left panel 
2. select add source and add add source 
3. select prometheus as data source 
4. prometheus node expoter service is already expose. provide name for datasource and provide the node exporter URL and port. 
5. save and test the connection. 

**Add dashboard**

1. Add the dashboard from the dashboard menu 
2. select manage and selet new dashboard 
3. from panel add the quey for services which you like to monitor from edit menu. 




