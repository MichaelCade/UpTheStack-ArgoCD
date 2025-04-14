# UpTheStack-ArgoCD
GitOps


You get this token from your influxdb installation 

```
kubectl get secret -n monitoring influxdb-influxdb2-auth -o jsonpath="{.data.admin-token}" | base64 --decode; echo
```

We will then take this token and create a secret that is used by Grafana and Telegraf to connect with InfluxDB 


```
kubectl create secret generic telegraf-influx-token \
  --namespace monitoring \
  --from-literal=influx-token=<ENTER TOKEN>
```

I also made the change here for 

kubectl create secret generic grafana-admin-secret \
  --namespace monitoring \
  --from-literal=admin-password=your-secure-password