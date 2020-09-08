# Introduction To Kubernetes

## What is Kubernetes

- an open-source platform designed to automate deploying, scaling, and operating application containers


## What the benefits of using K8




## Installing kubernetes

- Click the link [Here](https://storage.googleapis.com/kubernetes-release/release/v1.19.0/bin/windows/amd64/kubectl.exe)
- Once the application has installed, move it from the downloads folder into a new folder that you will name 'kube' in your C drive directory

![](/images/Kube-folder.png)

- Now we must add this folder to the PATH in our environment variables (system variables)


![](/images/Edit-Path.png)


- We also want to move the kube folder above our Docker folders, this ensures that Docker does not dictate the installation version of kubernetes


![](/images/Kube-env-variable.png)

- #### We can now run the following command to see if K8 installed successfully

```
kubectl version --client
```

## Installing Minikube


- We can install minikube with the link [Here](https://github.com/kubernetes/minikube/releases/download/v1.13.0/minikube-windows-amd64.exe)

- After minikube has installed, we can move it from our downloads folder into the same **kube** folder we made for kubernetes

- We must enter our Hyper v manager
- Go to virtual switch manager and create a internal virtual switch, in this instance we will call it **minikube**
- We will then have to go to our control panel, and under our Wifi network we must allow connection between this minikube virtual switch


- We can then start minikube running the below command

```
minikube start --vm-driver="hyperv" --hyperv-virtual-switch="minikube"
```

- When doing this we may receive an error saying ``Exiting due to GUEST_NOT_FOUND: Failed to start host: Error loading existing host.``, to overcome this we delete and then start minikube

```
minikube delete
minikube start
```

![](/images/minikube-start.png)

- This will take a while as it will provision our VM, creating all the virtual resources required
- It will prepare  kubernetes to interact with docker



## Running our first Hello World application with K8

- Below we can see that our master node named minikube is ready to use

![](/images/kubectl-get-nodes.png)


```
kubectl get all  # this will show us all our resources
```

- We can now relocate to the into the 03_04 folder which is inside the exercise files folder,
once here we can run our hello world yaml file

```
kubectl create -f helloworld.yaml
```

### Accessing the webpage

- This will allow us to see our hello world app webpage

```
kubectl expose deployment helloworld --type=NodePort
```
- We can now see below that our application is running on port ``31776``

![](/images/running-app-on-port.png)

- Using the minikube command below, it will actually take us to the web browser straight away

- We also have a small recap of the service ans where it has been deployed

![](/images/Recap-of-deploy.png)


```
# we are reffering to the service ``helloworld`` that we have just created
minikube service helloworld
```

- Now as you can see the web browser will be loaded for us

![](/images/Web-browser-loaded.png)


### Understanding the hello world application

- Usually you would have to create the service yml resource and then the deployment yml resource, however using `---` in a yml file
allows you to create multiple resources in just a single yml file

- This means we will only have to run this one file to create our resources

```
kubectl create -f helloworld-all.yml
```
- You will see thsat now two resoruces have been created from this one file