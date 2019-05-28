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

## frontend
1. Remove COPY in Dockerfile
2. Create a configmap from nginx.conf
    - `kubectl create configmap nginx-conf --from-file=nginx.conf=nginx.conf -o yaml --dry-run | kubectl apply -f -`
3. Mount the created configmap as a volume to front deployment
4. create the deployment/service.


### Update nginx.conf
1. Update nginx.conf
2. Update configmap from nginx.conf
    - `kubectl create configmap nginx-conf --from-file=nginx.conf=nginx.conf -o yaml --dry-run | kubectl apply -f -`
3. Make sure the configmap is updated
    - https://kubernetes.io/docs/tasks/configure-pod-container/configure-pod-configmap/#mounted-configmaps-are-updated-automatically
4. Reload nginx to make nginx.conf take effect.
```bash
$ FRONT_POD_NAME=$(kubectl get pod -l app=front -o jsonpath="{.items[0].metadata.name}")
$ kubectl exec $FRONT_POD_NAME -- cat /etc/nginx/conf.d/default.conf
$ kubectl exec $FRONT_POD_NAME -- nginx -s reload
# If there are more than one pods, consider delete the entire deployment
```