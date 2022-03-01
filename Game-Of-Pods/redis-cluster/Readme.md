# RedisCluster
The Kingdom of Redis Islands needs reinforcement! Build a highly available Redis Cluster based on the below architecture.
![Screenshot from 2022-03-01 15-03-23](https://user-images.githubusercontent.com/96254942/156143469-ef6a09c3-f432-4617-93d0-e1e0e5da242d.png)

## redis01
PersistentVolume - Name: redis01
Access modes: ReadWriteOnce
Size: 1Gi
hostPath: /redis01, directory should be created on worker node

## redis02
PersistentVolume - Name: redis02
Access modes: ReadWriteOnce
Size: 1Gi
hostPath: /redis02, directory should be created on worker node

## redis03
PersistentVolume - Name: redis03
Access modes: ReadWriteOnce
Size: 1Gi
hostPath: /redis03, directory should be created on worker node

## redis04
PersistentVolume - Name: redis04
Access modes: ReadWriteOnce
Size: 1Gi
hostPath: /redis04, directory should be created on worker node

## redis05
PersistentVolume - Name: redis05
Access modes: ReadWriteOnce
Size: 1Gi
hostPath: /redis05, directory should be created on worker node

## redis06
PersistentVolume - Name: redis06
Access modes: ReadWriteOnce
Size: 1Gi
hostPath: /redis06, directory should be created on worker node
## redis-cluster-statefulset
StatefulSet - Name: redis-cluster
Replicas: 6
Pods status: Running (All 6 replicas)
Image: redis:5.0.1-alpine
container name: redis, command: ["/conf/update-node.sh", "redis-server", "/conf/redis.conf"]
Env: name: 'POD_IP', valueFrom: 'fieldRef', fieldPath: 'status.podIP' (apiVersion: v1)
Ports - name: 'client', containerPort: '6379'
Ports - name: 'gossip', containerPort: '16379'
Volume Mount - name: 'conf', mountPath: '/conf', readOnly:'false' (ConfigMap Mount)
Volume Mount - name: 'conf', mountPath: '/conf', defaultMode = '0755' (ConfigMap Mount)
Volume Mount - name: 'data', mountPath: '/data', readOnly:'false' (volumeClaim)
volumes - name: 'conf', Type: 'ConfigMap', ConfigMap Name: 'redis-cluster-configmap',
volumeClaimTemplates - name: 'data'
volumeClaimTemplates - accessModes: 'ReadWriteOnce'
volumeClaimTemplates - Storage Request: '1Gi'
## redis-cluster-service
Ports - service name 'redis-cluster-service', port name: 'client', port: '6379'
Ports - service name 'redis-cluster-service', port name: 'gossip', port: '16379'
Ports - service name 'redis-cluster-service', port name: 'client', targetPort: '6379'
Ports - service name 'redis-cluster-service', port name: 'gossip', targetPort: '16379'
## redis-cluster-config
Configure the Cluster. Once the StatefulSet has been deployed with 6 'Running' pods, run the below commands and type 'yes' when prompted.
Command: kubectl exec -it redis-cluster-0 -- redis-cli --cluster create --cluster-replicas 1 $(kubectl get pods -l app=redis-cluster -o jsonpath='{range.items[*]}{.status.podIP}:6379 ')