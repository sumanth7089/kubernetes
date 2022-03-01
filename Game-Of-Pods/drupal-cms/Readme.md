# Drupal-CMS 
Deploy the below architecture for Drupal CMS.
![Screenshot from 2022-03-01 13-00-15 (1)](https://user-images.githubusercontent.com/96254942/156125622-7afe6121-1c9d-4080-a45f-3e28dbba9472.png)
## Drupal
Drupal is a free, open-source content management system (CMS) with a large, supportive community. It is a flexible CMS based on the LAMP stack,It's used by millions of people and organizations around the globe to build and maintain their websites.
### drupal-pv-hostpath:
 Configure drupal-pv with hostPath = /drupal-data (create the directory on Worker Nodes)
### drupal-pv
Access modes: ReadWriteOnce, Volume Name: drupal-pv, Storage: 5Gi
### drupal-pvc
Claim Name: drupal-pvc, Storage Request: 5Gi, Access modes: ReadWriteOnce
### drupal-deployment 
#### initContainer
Deployment Name: drupal, Replicas: 1, Image: drupal:8.6, Deployment has an initContainer has name: 'init-sites-volume', image: drupal:8.6, persistentVolumeClaim: drupal-pvc, mountPath: /data, Command: [ "/bin/bash", "-c" ], Args: [ 'cp -r /var/www/html/sites/ /data/; chown www-data:www-data /data/ -R' ].
#### container
Deployment 'drupal' uses correct pvc: drupal-pvc
Deployment has a regular container, name: 'drupal', image: 'drupal:8.6'
container: 'drupal', Volume mountPath: /var/www/html/modules, subPath: modules
container: 'drupal', Volume mountPath: /var/www/html/profiles, subPath: profiles
container: 'drupal', Volume mountPath: /var/www/html/sites, subPath: sites
container: 'drupal', Volume mountPath: /var/www/html/themes, subPath: themes
Deployment: "drupal" running
Deployment: 'drupal' has label 'app=drupal'
 ### drupal-service
frontend service name: drupal-service, drupal-service configured as NodePort, drupal-service uses NodePort 30095
## Drupal-mysql
### drupal-mysql-pv-hostpath
Configure drupal-mysql-pv with hostPath = /drupal-mysql-data (create the directory on Worker Nodes)
### drupal-mysql-pv 
Volume Name: drupal-mysql-pv, Storage: 5Gi, Access modes: ReadWriteOnce
### drupal-mysql-pvc
Claim Name: drupal-mysql-pvc, Storage Request: 5Gi, Access modes: ReadWriteOnce
### drupal-mysql-secret
Secret Name: drupal-mysql-secret, MYSQL_ROOT_PASSWORD=root_password, MYSQL_DATABASE=drupal-database
### drupal-mysql-deployment
Name: drupal-mysql
Replicas: 1
Image: mysql:5.7
Deployment Volume uses PVC : drupal-mysql-pvc
Volume Mount Path: /var/lib/mysql, subPath: dbdata
Deployment: 'drupal-mysql' running
### drupal-mysqlservice
Name: drupal-mysql-service, Type: ClusterIP, Port: 3306