1) MongoDB Deployment

Creating the database container/pod, in which the mongodb runs.

2) Secret

Creating the Secret component, where the username and password are stored.

3) Internal Service

Creating the service for MongoDB to be accessible by other Kubernetes components.

4) Mongo Express Deployment

Creating the Mongo Express container/pod, in which the web application runs.

5) ConfigMap

Creating the ConfigMap component, where the server url of the MongoDB is stored.

6) External Service

Creating the external service for Mongo Express to be accessible from outside the kubernetes cluster (from the browser)

