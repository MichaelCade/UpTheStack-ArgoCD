kubectl delete cronjob veeam-influxdb-sync -n monitoring
kubectl apply -f veeam-influxdb-sync.yaml
kubectl create job --from=cronjob/veeam-influxdb-sync veeam-influxdb-sync-manual -n monitoring
kubectl get pods -n monitoring

POD_NAME=$(kubectl get pods -n monitoring | grep '^veeam-influxdb-sync-manual-' | awk '{print $1}')
kubectl logs -f $POD_NAME -n monitoring