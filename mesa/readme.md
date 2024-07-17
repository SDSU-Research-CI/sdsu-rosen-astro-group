# MESA Jobs
This readme will guide you through submitting and managing interactive and batch jobs on TIDE using the [MESA container image](https://github.com/orgs/SDSU-Research-CI/packages/container/package/mesa-notebook).

This readme assumes that you have:
- Access to the namespace "sdsu-rosen-astro-group"
- Completed the [getting access](https://sdsu-research-ci.github.io/softwarefactory/gettingaccess) guide
- Installed [kubectl](https://kubernetes.io/docs/tasks/tools/#kubectl) on your local machine
- Downloaded your [NRP Portal config](https://portal.nrp-nautilus.io/authConfig) and copied it to ~/.kube/config
- Cloned this repository and run the commands from the rosen-astro-group/mesa directory

## Config

### Step 1: Set Context

If you wish to not pass the namespace name for each command, run the following to set the namespace context:

```
kubectl config set-context nautilus --namespace=sdsu-rosen-astro-group
```

## Interactive Job

Schedule the interactive job

```
kubectl apply -f mesa-interactive-job.yaml
```

Get the pod and ensure it's running:

```
kubectl get pods -n sdsu-rosen-astro-group
```

`Note: Replace "[unique-id]" with the pod name from the ouput of the previous command in the example below.`

Look for the pod. Once running, collect your pod's logs:

```
kubectl logs mesa-interactive-job-[unique-id] -n sdsu-rosen-astro-group
```

From the output, copy the URL to the clipboard that starts with http://127.0.0.1./. 

In a second terminal window, run the following command to set up port forwarding between your computer and the container running Jupyter.

```
kubectl port-forward mesa-interactive-job-[unique-id] -n sdsu-rosen-astro-group 8888:8888
```

*Note*: If you get an error message indicating port 8888 is already taken, simply change the port number on the left side of the colon in the above command i.e. `8889:8888`.
Then when you paste the URL from the output, make sure to update the port from 8888 to 8889, or whatever number you chose.
This issue can arise if you have a local instance of Jupyter Lab already running on port 8888.

You should now be able to access the URL you copied to the clipboard in your web browser.

## Shutdown / Cleanup

When done, delete your pod:

```
kubectl delete -f mesa-interactive-job.yaml -n sdsu-rosen-astro-group
```

`Note: Your volume will persist so you can start the pod again and have acecss to your data.`
