# Quobyte CSI Deploy Scripts

This set of scripts setting up Requirements, Deploy Quobyte clients, Deploy Quobyte CSI and Use Quobyte volumes in Kubernetes, described at [quobyte-csi repo](https://github.com/quobyte/quobyte-csi/)

Scripts are developed to be executed against `testing` environment and as far as it's requires encription-in-transit, you'll need to add valid `ca.pem`, `client-cert.pem` and `client-key.pem` files to the working directory, so they'll be used on Quobyte Clients mount



#### On your host machine install and setup Docker, k8s and kind
Make sure they are working ok - https://kind.sigs.k8s.io/docs/user/quick-start/

## Run scripts in the following order:

[From your work directory]

1. `./testing--setup_kind_cluster`
It'll set up a kind cluster and log in to its control-plane node

[On control-plane node]

2. `./install_csi_3x install` - to [deploy Quobyte CSI driver](https://github.com/quobyte/quobyte-csi#deploy-quobyte-csi-driver) and [deploy containerized Quobyte Clients](https://github.com/quobyte/quobyte-csi/blob/master/docs/install_client/deploy_clients_3_x.md#deploy-containerized-quobyte-client)
3. `./pre-flight_checks` makes sure use Quobyte volumes provisioned successfully and are accessible, prior e2e tests running
4. If pre-flight checks went fine, then e2e tests can be executed - `./install_csi_3x e2e`


## Changes revert options

* To uninstall Quobyte CSI driver - use `./install_csi_3x uninstall`

* To revert changes made to the cluster with pre-flight script - use `./pre-flight_checks cleanup`

* To delete kind cluster and all related resources - execute `./delete_cluster` on your host machine (the script is not deleting created docker image)
