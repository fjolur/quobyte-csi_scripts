# quobyte-csi_scripts


On your host machine install and setup Docker, k8s ans kind
Make sure they are working ok - https://kind.sigs.k8s.io/docs/user/quick-start/

Use scripts in following order:
1. ```setup kind cluster and login to control plane.sh```
when your kind cluster is up and running and you're logged in to its control-plane node

2. copy ```install_csi_3x``` and ```pre-flight checks.sh``` files to the control-plane node:

```docker cp <path to scripts>/install_csi_3x <path to scripts>/pre-flight checks.sh $(docker ps -aqf "name=control-plane"):/```

3. ```./install_csi_3x install``` - to install Quobyte CSI driver
4. ```pre-flight checks.sh``` makes sure use Quobyte volumes in Kubernetes works fine prior e2e tests running
5. If pre-flight checks went fine, then we can run e2e tests - ```./install_csi_3x e2e```



To uninstall Quobyte CSI driver - use ```./install_csi_3x uninstall```

To revert changes made to the cluster with pre-flight script - use ```./pre-flight checks.sh cleanup```

To delete kind cluster and all related resources - run ```delete cluster.sh``` on your host machine
