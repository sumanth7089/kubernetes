# Troublsehoot the cluster
The Game of Pods cluster is Broken! Troubleshoot, fix the cluster issues and then deploy the below architecture to unlock our Image Gallery!
![Screenshot from 2022-03-01 14-34-41](https://user-images.githubusercontent.com/96254942/156142486-94eacde3-9086-4de8-9e93-bb63762bd849.png)

## Master Node
Master node: coredns deployment has image: 'k8s.gcr.io/coredns:1.6.7'
Fix kube-apiserver. Make sure its running and healthy.
kubeconfig = /root/.kube/config, User = 'kubernetes-admin' Cluster: Server Port = '6443'
## worker Node
node01 is ready and can schedule pods?
## /Web
node01 has hostPath created = '/web'
## data-pv
Create new PersistentVolume = 'data-pv'
PersistentVolume = data-pv, accessModes = 'ReadWriteMany'
PersistentVolume = data-pv, hostPath = '/web'
PersistentVolume = data-pv, storage = '1Gi'
## data-pvc
Create new PersistentVolumeClaim = 'data-pvc'
PersistentVolume = 'data-pvc', accessModes = 'ReadWriteMany'
PersistentVolume = 'data-pvc', storage request = '1Gi'
PersistentVolume = 'data-pvc', volumeName = 'data-pv'
## gop pod
Create a pod for fileserver, name: 'gop-fileserver'
pod: gop-fileserver image: 'kodekloud/fileserver'
pod: gop-fileserver mountPath: '/web'
pod: gop-fileserver volumeMount name: 'data-store'
pod: gop-fileserver persistent volume name: data-store
pod: gop-fileserver persistent volume claim used: 'data-pvc'
## gop service
New Service, name: 'gop-fs-service'
Service name: gop-fs-service, port: '8080'
Service name: gop-fs-service, targetPort: '8080'
Service name: gop-fs-service, NodePort: '31200'

