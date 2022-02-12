#1 Set Node Affinity to the deployment to place the pods on node01 only.


Name: blue
Replicas: 3
Image: nginx
NodeAffinity: requiredDuringSchedulingIgnoredDuringExecution
Key: color
values: blue

#2 Create a new deployment named red with the nginx image and 2 replicas, and ensure it gets placed on the controlplane node only.



Use the label - node-role.kubernetes.io/master - set on the controlplane node.

Name: red
Replicas: 2
Image: nginx
NodeAffinity: requiredDuringSchedulingIgnoredDuringExecution
Key: node-role.kubernetes.io/master
Use the right operator