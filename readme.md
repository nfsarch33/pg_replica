
# Apply the ConfigMap
kubectl apply -f db-config.yaml

# Apply the master DB changes
kubectl apply -f db-primary.yaml

# Get logs from pods
kubectl logs -f pods/master-deployment-6c8798c8d9-qgnm9 -c postgres-master --namespace default

# master-service-cluster-ip.yml
# should be possible (connected to pod):
# kubectl exec -it replication-deployment-5d84b7679b-fdgwq -- apt update
# kubectl exec -it replication-deployment-5d84b7679b-fdgwq -- apt install telnet
# kubectl exec -it replication-deployment-5d84b7679b-fdgwq -- telnet master-cluster-dns-name 5439

# master-service-node-port.yml
# should be possible from node:
# telnet ip_of_node 31324
# telnet ip_of_pod  5439

# Steps

kubectl create -f db-config.yaml
kubectl create -f db-primary.yaml
kubectl create configmap pgsql-conf-files-config --from-file config

#
The PersistentVolume "volume-pv-hostpath-standby" is invalid: spec.persistentvolumesource: Forbidden: spec.persistentvolumesource is immutable after creation
