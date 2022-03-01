# Deploy the below architecture for implementing a Jekyll SSG.
![52125e17-cbf9-41ed-8e51-63eebbb0c91a](https://user-images.githubusercontent.com/96254942/155839290-9671e891-0122-42a8-aa61-4c6b31e011df.jpeg)

Jekyll is a free and open source static site generator. Like a content management system (for example, Drupal and WordPress), Jekyll can be used to build websites with rich and easy-to-use navigation.
## creating a admin
Certificate and key pair for user drogo is created under /root. Add this user to kubeconfig = /root/.kube/config, User = drogo, client-key = /root/drogo.key client-certificate = /root/drogo.crt
Create a new context in the default config file (/root/.kube/config) called 'developer' with user = drogo and cluster = kubernetes
## creating a developer-role
create a 'developer-role', should have all(*) permissions for services, persistentvolumeclaims, Pods in development namespace
## creating a developer-rolebinding
create a rolebinding = developer-rolebinding, role= 'developer-role', namespace = development and rolebinding = developer-rolebinding should associate with user = 'drogo'
## creating a kubeconfig 
set context 'developer' with user = 'drogo' and cluster = 'kubernetes' as the current context.
## creating a jeklly-service
create a Service 'jekyll' uses targetPort: '4000', port: 8080, nodePort: 30097, selector: run=jekyll  namespace: 'development'
## Init container & container
pod: 'jekyll' has an initContainer, name: 'copy-jekyll-site', image: 'kodekloud/jekyll'
and run command: [ "jekyll", "new", "/site" ] , mountPath= /site, volumename = site
pod: 'jekyll', container: 'jekyll', volume name = site
pod: 'jekyll', container: 'jekyll', mountPath = /site
pod: 'jekyll', container: 'jekyll', image = kodekloud/jekyll-serve, volume name = site, mountPath = /site, uses volume called 'site' with pvc = 'jekyll-site' and label 'run=jekyl' 
jekyll-site pvc used by pod 'jekyll'
## pvc
Storage Request: 1Gi
Access modes: ReadWriteMany
pvc name = jekyll-site, namespace development
## pv
jekyll-pv uses hostPath = /site, make sure it is available on worker nodes, Storage Request: 1Gi
Access modes: ReadWriteMany
## Task completed
![6b9fc76e-3ccf-45d3-a742-03407e6b85cd](https://user-images.githubusercontent.com/96254942/155840959-e4895fce-78e8-4d65-bea4-33080fe0dab1.jpeg)
# output
![06fe5bd6-140a-45ac-95bc-6bd2bf78f925](https://user-images.githubusercontent.com/96254942/155840955-04c6092a-9ded-4fca-b3b6-0338d3f383ab.jpeg)



