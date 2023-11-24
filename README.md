# r2mle-workshop

# Airflow

## Install

```bash
helm upgrade --install airflow oci://registry-1.docker.io/bitnamicharts/airflow --namespace airflow --create-namespace
```

Ref: [charts/bitnami/airflow at main · bitnami/charts (github.com)](https://github.com/bitnami/charts/tree/main/bitnami/airflow)

#### Getting username and password
```bash
export AIRFLOW_PASSWORD=$(kubectl get secret --namespace "airflow" airflow -o jsonpath="{.data.airflow-password}" | base64 -d)
    echo User:     user
    echo Password: $AIRFLOW_PASSWORD
```
#### Port forwarding to access the Airflow Web UI
```bash
kubectl port-forward --namespace airflow svc/airflow 8080:8080 &
    echo "Airflow URL: http://127.0.0.1:8080"
```

## Update requirements.txt
```bash
cd airflow

kubectl create -n airflow configmap requirements --from-file=requirements.txt
helm upgrade airflow oci://registry-1.docker.io/bitnamicharts/airflow --namespace airflow -f values.yaml
```

# mlflow

## Install

```bash
helm upgrade --install mlflow oci://registry-1.docker.io/bitnamicharts/mlflow --namespace mlflow --create-namespace
```

Ref: [charts/bitnami/mlflow at main · bitnami/charts (github.com)](https://github.com/bitnami/charts/tree/main/bitnami/mlflow)

#### Getting username and password
```bash
echo Username: $(kubectl get secret --namespace mlflow mlflow-tracking -o jsonpath="{ .data.admin-user }" | base64 -d)
echo Password: $(kubectl get secret --namespace mlflow mlflow-tracking -o jsonpath="{.data.admin-password }" | base64 -d)
```

