# Add this user to kubeconfig
k config set-credentials drogo --client-key=/root/drogo.key --client-certificate=/root/drogo.crt
# Create a new context in the default config file
k config set-context developer --user=drogo --cluster=kubernetes  
# set context 'developer' as current context 
k config use-context developer 

create role, rolebinding, pod, services, pv, pvc with responding yaml files 
