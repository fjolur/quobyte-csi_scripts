# quobyte-csi_scripts


On your host machine install and setup Docker, k8s ans kind
Make sure they are working ok - https://kind.sigs.k8s.io/docs/user/quick-start/

Use scripts in following order:
1. ```setup kind cluster and login to control plane.sh```
when your kind cluster is up and running and you're logged in to its control-plane node

2. copy ```install_csi_3x``` and 'pre-flight checks.sh' files to the control-plane node - 
use 
```docker cp ../install_csi_3x $(docker ps -aqf "name=control-plane"):/```

3. ```install_csi_3x``` file contains install,e2e and uninstall instructions
4. ```pre-flight checks.sh``` makes sure use Quobyte volumes in Kubernetes works fine prior e2e tests running
it's also contains 'cleanup' script for reverting changes made to the cluster.

to delete kind cluster and all related resources - run ```delete cluster.sh``` on your host machine
