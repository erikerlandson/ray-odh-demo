# ray-odh-demo

Prototype an integration of ray with Open Data Hub on OpenShift, using a singleuser profile to provision a ray cluster.

### Demo Directions

#### Prerequisites - This demo assumes:

1. You have a project namespace in OpenShift to use for your demo, and that you have admin privileges on the cluster to install the Open Data Hub operator, add rolebindings define CRDs, etc.
1. You have installed the Open Data Hub community operator from the Operator Catalog.
1. You have created a deployment of the ODH operator into your demo namespace. The only ODH component necessary for this demo is JupyterHub, but others may be installed if desired.

#### Installing the Ray operator

This demo makes use of the Ray operator.
To install the operator, install the following in your demo:

1. Go to your demo namespace: `oc project <your-project-namespace>`
1. Install the CRD for a ray cluster: `oc apply -f deploy/operator/ray-cluster-crd.yaml`
1. Run the operator pod: `oc apply -f deploy/operator/ray-operator.yaml`
1. You should now see the ray operator running in pod `ray-operator-pod`
1. You may optionally test that the operator is working by creating a CR and ensuring it spins a ray cluster: `oc apply -f deploy/operator/ray-test-cluster-cr.yaml`

#### To install and run this demo:

This demo makes use of a role-binding to the role `ray-operator-role` defined for the ray operator during the instructions above.

1. Run `oc apply -f` on all the `.yaml` files in the `deploy/odh` directory.
1. Wait a few minutes and log into the JupyterHub launcher via Routes. You should see a new notebook image option `ray-minimal-notebook:demo`: choose this. If the ray notebook is still not visible, you will need to restart the `jupyterhub-xxxx` pod so that it reads the new profile you just installed. Simply deleting this pod will cause it to be restarted automatically.
1. Launch your JupyterHub environment. As part of the startup process, the ODH JupyterHub launcher should also start up a Ray cluster.
2. Add the git repo `https://github.com/erikerlandson/ray-odh-demo.git` by clicking on "Git Clone" button on top left of Jupyter and pasting the link to repo.
3. In Jupyter, navigate to directory `ray-odh-demo.git/source` and open the demo notebook.
4. Run the notebook to confirm that it connects to your ray cluster and operates correctly.
5. You could also see the head and worker nodes created under pods as `ray-cluster-$USER-ray-cluster-$USER-head-xxxxx` and `ray-cluster-$USER-ray-cluster-$USER-worker-xxxxx` pods
