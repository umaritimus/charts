# mssql-linux

## Install k3d

## Install kubectl

## Install helm

## Create helm chart

cd ./charts
helm create mssql-linux
helm package mssql-linux
helm repo index .
git add . 
git commit -m "my-app-chart"
git push

## Start k3d cluster

k3d cluster create app --api-port 6550 --servers 1 --agents 1 --port 443:443@loadbalancer --volume ./assets/src:/src@all --wait
k3d cluster create app --api-port 6550 --servers 1 --agents 1 --port 443:443@loadbalancer --wait

## Install mssql helm

helm repo add umaritimus-charts https://github.com/umaritimus/charts
helm search repo mssql-linux
kubectl create namespace mssql
helm install sqlserver stable/mssql-linux --namespace mssql --set acceptEula.value=Y --set edition.value=Developer --set collation.value=Latin1_General_BIN  --set service.type.value=LoadBalancer --replace

-- sa password
[Text.Encoding]::Utf8.GetString([Convert]::FromBase64String($(kubectl get secret --namespace mssql sqlserver-mssql-linux-secret -o jsonpath="{.data.sapassword}")))

-- address
kubectl get nodes --namespace default -o jsonpath="{.items[0].status.addresses[0].address}"

### Forward port

kubectl get pods --namespace mssql
kubectl port-forward pod/sqlserver-mssql-linux-757bbdcb5b-g8dgd 15789:1433 --namespace mssql

### Connect

mssql-cli -S 127.0.0.1,15789 -U sa
## Get sa password

[Text.Encoding]::Utf8.GetString([Convert]::FromBase64String($(kubectl get secret --namespace mssql sqlserver-mssql-linux-secret -o jsonpath="{.data.sapassword}") 


## Cleanup

### Remove deployment

helm uninstall sqlserver --namespace mssql
### Remove cluster

k3d cluster delete --all