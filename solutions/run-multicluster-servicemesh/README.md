# Set up a Multicluster Service Mesh on OCM

This solution sets up an [Istio multi-primary, multi-network service mesh](https://istio.io/latest/docs/setup/install/multicluster/multi-primary_multi-network/)
across OCM managed clusters, with the Istio control plane installed by the
[Sail Operator](https://github.com/istio-ecosystem/sail-operator).

The per-cluster Istio configuration (`Istio` CR, east-west gateway) is delivered from the hub by the `istio-mesh`
addon, an AddOnTemplate addon maintained in addon-contrib:
[istio-mesh-addon](https://github.com/open-cluster-management-io/addon-contrib/tree/main/istio-mesh-addon).

> This replaces the previous version of this solution, which depended on the
> [multicluster-mesh](https://github.com/open-cluster-management-io/multicluster-mesh) addon.
> That repository was archived on Jul 24, 2025 and installed Istio 1.16 through the in-cluster
> IstioOperator, which Istio removed in 1.24.

## Prerequisite

Set up the dev environment in your local machine following [setup dev environment](../setup-dev-environment).
It creates the hub (`kind-hub`) and two managed clusters (`cluster1` and `cluster2`).

## Set up and verify the mesh

Follow the steps in the [istio-mesh-addon README](https://github.com/open-cluster-management-io/addon-contrib/tree/main/istio-mesh-addon#prerequisites):

1. Prepare each managed cluster: Sail Operator, work agent RBAC, shared CA (`cacerts`), east-west gateway Service.
2. Install the addon from the hub and label the clusters to join the mesh.
3. Connect the clusters with remote secrets.
4. Verify cross-cluster traffic with the `helloworld` sample.
