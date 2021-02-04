# ray-odh-demo

Prototype an integration of ray with Open Data Hub on OpenShift, using a singleuser profile to provision a ray cluster.

### Demo Directions

Prerequisites - This demo assumes:

1. You have a project namespace in OpenShift to use for your demo, and that you have admin privileges on the cluster to install the Open Data Hub operator and add rolebindings.
1. You have installed the Open Data Hub community operator from the Operator Catalog.
1. You have created a deployment of the ODH operator into your demo namespace. The only ODH component necessary for this demo is JupyterHub, but others may be installed if desired.

To install and run this demo:

1. Edit the rolebinding file `deploy/ray-jh-rolebinding.yaml` in this repository: change the namespace field to correspond to your demo namespace. The JupyterHub launcher needs this rolebinding to give it authorization to create the ray cluster deployment objects in your project.
1. Run `oc apply -f` on all the `.yaml` files in the `deploy` directory.
1. You will need to restart the `jupyterhub-xxxx` pod so that it reads the new profile you just installed. Simply deleting this pod will cause it to be restarted automatically.
1. Log into the ODH JupyterHub launcher. You should see a new notebook image option `ray-notebook:latest`: choose this.
1. In the environment variable section, add `JUPYTER_PRELOAD_REPOS` and set to `https://github.com/erikerlandson/ray-odh-demo.git`
1. Launch your JupyterHub environment. As part of the startup process, the ODH JupyterHub launcher should also start up a Ray cluster.
1. In Jupyter, navigate to directory `ray-odh-demo.git/source` and open the demo notebook.
1. Run the notebook to confirm that it connects to your ray cluster and operates correctly.
