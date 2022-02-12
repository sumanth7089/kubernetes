There is an application that needs to be deployed on Kubernetes cluster under Apache web server. The Nautilus application development team has asked the DevOps team to deploy it. We need to develop a template as per requirements mentioned below:
1. Create a namespace named as httpd namespace devops.
2. Create a service named as httpd-service-devops, targetPort 80 to
nodePort30004.
3. Create a deployment named as httpd-deployment-devops under the same namespace as mentioned above, Its service should also be same as the one mentioned above. Use image httpd with latest tag only and remember to mention tag i.e httpd+latest, and container name should be httpd. And make sure replicas counts are 2.
4. Set labels app to httpd.
Note: The kubect1 utility on jump_ host has been configured to work with the
kubernetes cluster.