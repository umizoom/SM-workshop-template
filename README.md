# Ship with Kubernetes 

This is a workshop that will be running as part of the 2026 OttawaU hack event. 

Press the "**Use this template**" button to make a copy of this template into your personal
GitHub account!

## Pre-requisites

You will need:

1. A personal GitHub account
2. Install Docker or an equivalent tool to run containers. Example Docker Desktop or for mac users [colima](https://github.com/abiosoft/colima).
3. Install [kind](https://kind.sigs.k8s.io/) to run local Kubernetes clusters using Docker container "nodes"
4. Install `kubectl`. Instructions [here](https://kubernetes.io/docs/tasks/tools/#kubectl)


## Work Shop Steps: 

1. Configure GitHub repository

    a. Go to the workshop's project repository and click Use this template.

    b. Make sure the Owner is set to your own personal GitHub account.

    c. Give it a name, we'll use sm-workshop-demo.

    d. Set the visibility to Public.

    e. Click Create repository.

    f. Go to Settings -> Actions -> General.

    g. Scroll down to Workflow Permissions and enable "Read and write permissions" under .

    h. Enable "Allow GitHub Actions to create and approve pull requests".

    i. Click Save.

2. Run GitHub Actions

    a. In GitHub, navigate to the Actions tab.

    b. Select the `Setup Repository` workflow.

    c. Click Run workflow. After the workflow finishes, you should see a PR in the repository.

3. Merge PR

    a. Navigate to Pull Requests.

    b. Check the open PR.

    c. Merge the PR. This triggers a build of the test-app application.

4. Create a cluster

    Run a command to create a new Kubernetes cluster. For example, we're using kind to create a cluster called sm-workshop-cluster.

    ```shell
    kind create cluster --name sm-workshop-cluster
    ```

    If you have already have a cluster, you can skip this step, but take note of your cluster name so you can use it in future steps.

5. Run the bootstrap script

    a. Open up the cloned repository in your code editor.

    b. Run the `./bootstrap.sh` script.

    c. It will prompt you to press enter several times, to ensure there are no errors at each stage.

6. Check Pods Are Running

   `kubectl get pods -A`

7. Get Argocd password

   `kubectl -n argocd get secrets/argocd-initial-admin-secret --template='{{.data.password}}' | base64 -d`

8. Access ArgoCD
   
   `kubectl -n argocd port-forward service/argocd-server 8080:80`

9. Go to your browser and navigate to `localhost:8080`

10. Login to argocd with the password from Step 7

11. Find your `test-app` and click refresh

12. The test app should start up

13. Bonus try to port forward the test app


## Useful Commands

### Creating a Cluster

```shell
kind create cluster --name sm-workshop-cluster
```
### Run the Bootstrap Script

```shell
./bootstrap.sh
```
_Make sure to run this in the folder the checked out repo is cloned into!_


### Check Pods Are Running

```shell
kubectl get pods -A
```

### Retrieve ArgoCD Admin Password

```shell
kubectl -n argocd get secrets/argocd-initial-admin-secret --template='{{.data.password}}' | base64 -d
```

### Access ArgoCD

```shell
kubectl -n argocd port-forward service/argocd-server 8080:80
```

### Access Test App

```shell
kubectl -n default port-forward service/test-app 8081:80
```