# create Namespace
Let us now deploy an Ingress Controller. First, create a namespace called ingress-space.


# create Ingress-deployment 
Let us now deploy the Ingress Controller. Create a deployment using the file given.
Deployed in the correct namespace.
Replicas: 1
Use the right image
Namespace: ingress-space

# create a service
create a service to make Ingress available to external users.
Create a service following the given specs.
Name: ingress
Type: NodePort
Port: 80
TargetPort: 80
NodePort: 30080
Namespace: ingress-space
Use the right selector

# Create the ingress resourceIngress Created
Path: /wear
Path: /watch
path: /pay
Configure correct backend service for /wear
Configure correct backend service for /watch
configure correct backend service for /pay
Configure correct backend port for /wear service
Configure correct backend port for /watch service
configure correct backend service for /pay service
Create the ingress resource to make the applications available at /wear and /watch on the Ingress service.
Create the ingress in the app-space namespace.