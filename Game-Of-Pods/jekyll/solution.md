# Add this user to kubeconfig
k config set-credentials drogo --client-key=/root/drogo.key --client-certificate=/root/drogo.crt
# Create a new context in the default config file
k config set-context developer --user=drogo --cluster=kubernetes  
# set context 'developer' as current context 
k config use-context developer 

create role, rolebinding, pod, services, pv, pvc with responding yaml files 
## creating a developer-role
k create role developer-role --resources=pods,pvc,svc --verb="*" --namespace=development 
## creating a developer-rolebinding
k create rolebinding developer-rolebinding --role=developer-role --user=drogo --namespace=development 