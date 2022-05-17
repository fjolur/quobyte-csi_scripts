# quobyte-csi_scripts


On your host machine install and setup Docker, k8s ans kind
Make sure they are working ok - https://kind.sigs.k8s.io/docs/user/quick-start/

Use scripts in following order:
1. ```setup_kind_cluster_and_login_to_control_plane.sh```
when your kind cluster is up and running and you're logged in to its control-plane node

2. copy ```install_csi_3x``` and ```pre-flight_checks.sh``` files to the control-plane node:

```
docker cp <path to scripts>/install_csi_3x $(docker ps -aqf "name=control-plane"):/
docker cp <path to scripts>/pre-flight_checks.sh $(docker ps -aqf "name=control-plane"):/
```
3. Make those scripts executable - at control-plane terminal

```
chmod +x <path to scripts>/install_csi_3x <path to scripts>/pre-flight_checks.sh
```
4. ```./install_csi_3x install``` - to install Quobyte CSI driver
5. ```./pre-flight_checks.sh``` makes sure use Quobyte volumes in Kubernetes works fine prior e2e tests running
6. If pre-flight checks went fine, then we can run e2e tests - ```./install_csi_3x e2e```



To uninstall Quobyte CSI driver - use ```./install_csi_3x uninstall```

To revert changes made to the cluster with pre-flight script - use ```./pre-flight_checks.sh cleanup```

To delete kind cluster and all related resources - run ```delete_cluster.sh``` on your host machine
