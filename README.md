# CI Cluster Config

This repository contains configuration for our CI Cluster - known as "hivemind" - to be loaded as an ArgoCD/OpenShift GitOps application!

## Updating a ClusterPool

If yuou wish to update a ClusterPool to a newer OCP release, or create a new pool, you can do the following:

1. Clone this repository and checkout a new branch.
2. Create a new ClusterImageSet in the appropriate folder (or create a new folder for a new Y-stream) in the `ci-pools/clusterimagesets` directory.  **Try to keep naming consistent as `openshift-vXYZ`.**
3. [If you're updating a pool's z-stream level] Edit the ClusterPool's definition in the `ci-pools/clusterpools` directory to reference the new ClusterImageSet by name for each cloud platform where you would like that OCP version represented.
4. [If you're adding a new y-stream build or pool] Add a new ClusterPool definition in the `ci-pools/clusterpools` directory for the correct cloud platform, referencing your ClusterImageSet.  **Try to keep naming consistent as `canary-<platform>-<latest/minus>-XY`.**
5. Push your branch and open a PR, once merged it will automatically roll out to the CI cluster.
6. Wait for the pool on the CI cluster to be consumed and eventually replaced by the new version.  The ClusterPool object has a status item to track the status of the pool!