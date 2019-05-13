## Kafka

```bash
$ helm init
$ helm repo add confluentinc https://confluentinc.github.io/cp-helm-charts/
$ helm repo update
$ helm install --set cp-schema-registry.enabled=false,cp-kafka-rest.enabled=false,cp-kafka-connect.enabled=false confluentinc/cp-helm-charts --name infra

```

## Postgres

```bash
$ kubectl create configmap postgres-initdb-config --from-file=00-schema.sql=infra/00-schema.sql,infra/01-data.sql -o yaml --dry-run | kubectl apply -f -
$ kubectl apply -f infra/postgres.yaml

```


