## Kafka

```bash
$ helm init
$ helm repo add confluentinc https://confluentinc.github.io/cp-helm-charts/
$ helm repo update
$ helm install --set cp-schema-registry.enabled=false,cp-kafka-rest.enabled=false,cp-kafka-connect.enabled=false confluentinc/cp-helm-charts --name infra

```

## Postgres



