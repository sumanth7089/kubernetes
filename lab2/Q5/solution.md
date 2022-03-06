```
extract the logs from pod container 
k logs -c log-x dev-pod-dind-878516
```
then grep logs which are showing WARNING and save it ina file 
k logs -c log-x dev-pod-dind-878516 | grep WARNING > /opt/dind-878516_logs.txt