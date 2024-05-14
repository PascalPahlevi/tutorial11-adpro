# tutorial11-adpro Part 1 Reflection

1.  Compare the application logs before and after you exposed it as a Service.
Try to open the app several times while the proxy into the Service is running.
What do you see in the logs? Does the number of logs increase each time you open the app?

Before being exposed as a service: <br>
 <img width="635" alt="image" src="https://github.com/PascalPahlevi/tutorial11-adpro/assets/143638456/04bd654c-be90-4ef1-98d1-6edf7245c247">

After being exposed as a service: <br>
 <img width="630" alt="image" src="https://github.com/PascalPahlevi/tutorial11-adpro/assets/143638456/06d9ccf5-394a-4ca1-b2b6-b180e85d96e9">

When comparing these two screenshots, it is quite obvious what the differences between the two are. To begin with, prior to the application being exposed as a service, the application logs only showed two lines, those being "Started HTTP server on port 8080" and "Started UDP server on pot 8081". From these two messages, we can say that before the application was exposed as a service, the application was simply initiating a server, not allowing any access to it. However, in the second screenshot, we can see that two more lines were added to the application logs after it was exposed as a service and both of those lines showed "Get/". What we can get from this is that as soon as the application was exposed as a service, access to the application was essentially enabled hence when accessed, a get protocol was established in order to get the necessary data to appear on the application.
 
2.  Notice that there are two versions of `kubectl get` invocation during this tutorial section.
The first does not have any option, while the latter has `-n` option with value set to
`kube-system`.
What is the purpose of the `-n` option and why did the output not list the pods/services that you
explicitly created?

The `-n` option in kubernetes stands for "namespace". This feature essentially helps as a way to organize clusters into smaller virtual sub-clusters, allowing us to have better organization of the clusters we have created. After applying `kubectl get -n`, the pods/services that was explicitly created was not listed because, in my case, the pod `hello-node` was created in a different namespace not known as `kube-system`. Since the initial idea behind namespaces was to separate these resources, `hello-node` simply would not appear with the application of `-n` due to the nature behind its function, on the other hand, when simply using `kubectl get`, since the namespace was not specificed, it would have automatically listed down all the created pods.

# tutorial11-adpro Part 2 Reflection

1. What is the difference between Rolling Update and Recreate deployment strategy? <br>

The Rolling Update strategy essentially allows a deployment update to take place with zero downtime. This strategy would allow a much smoother transition, greatly reducing the downtime for the new version to take place. On the other hand, the Recreate strategy essentially initiates a dummy deployment, shutting down the current version. During this downtime, the new version will take its place, allowing the app to redeploy once again. 
 
2. Try deploying the Spring Petclinic REST using Recreate deployment strategy and document
your attempt.

- I first began by creating the spring-petclinic-rest deployment: <br>
<img width="637" alt="image" src="https://github.com/PascalPahlevi/tutorial11-adpro/assets/143638456/9eb82134-b81d-4eb4-bdce-e4757988cfa5">

- Afterwards, I had to expose the spring-petclinic-rest services after quickly checking the logs: <br>
<img width="626" alt="image" src="https://github.com/PascalPahlevi/tutorial11-adpro/assets/143638456/8993d87d-3caa-4be1-8164-26a26e83e7a3">
<img width="614" alt="image" src="https://github.com/PascalPahlevi/tutorial11-adpro/assets/143638456/4b054734-b52b-4024-a545-64b73465490c">

- Then, I created the manifest files for both the deployment and services of spring-petclinic-rest: <br>
<img width="621" alt="image" src="https://github.com/PascalPahlevi/tutorial11-adpro/assets/143638456/30ec1434-5ab5-4c6c-bed6-096ee88476bf">

- To apply the Recreate deployment strategy, I directly edited the yaml file, changing its strategy from Rolling Update into Recreate, additionally also making sure to add 4 replicas to the deployment: <br>
<img width="356" alt="image" src="https://github.com/PascalPahlevi/tutorial11-adpro/assets/143638456/d8e2e39f-5606-4d6d-ad88-37f2da77e5f8">

- Then, I deleted the initial minikube and started a new one, applying both of the created deployment and service manifest files.
<img width="623" alt="image" src="https://github.com/PascalPahlevi/tutorial11-adpro/assets/143638456/7995a546-66bf-48f6-b56b-5d037057beea">
<img width="481" alt="image" src="https://github.com/PascalPahlevi/tutorial11-adpro/assets/143638456/5af4c134-80c7-45c0-b74d-d8aadd1ded2a">

- Finally, I set a new image, making sure it is the new one, and then the Recreate deployment strategy was applied. Also shown below are the results: <br>
<img width="623" alt="image" src="https://github.com/PascalPahlevi/tutorial11-adpro/assets/143638456/a812b985-c2e0-47bf-8fd6-deefe31009d9">
<img width="629" alt="image" src="https://github.com/PascalPahlevi/tutorial11-adpro/assets/143638456/fb320b5c-74e8-428a-8e41-d07b37c47e3a">

3.  Prepare different manifest files for executing Recreate deployment strategy <br>

The manifest files for executing this deployment strategy are `recreate-deployment.yaml` and `recreate-service.yaml`

4. What do you think are the benefits of using Kubernetes manifest files? Recall your experience
in deploying the app manually and compare it to your experience when deploying the same app
by applying the manifest files (i.e., invoking `kubectl apply -f` command) to the cluster.

Using the Kubernetes manifest files prove to provide quite a few benefits. To start with, it essentially acts as a backup for both the deployments and services already applied within the app. For example, if a cluster was to be accidentally deleted, by applying these manifest files, the exact same deployment and service applied to the app previously would be quickly recovered. This leads to another benefit to the manifest files, increased efficiency in the deployment of apps. When deploying manually, there are a few steps that the user must go through, such as creating the deployment and service, then afterwards exposing the service, taking a lot of time. On the other hand, when deploying through the manifest files, since all the necessary details of the deployment and service was already saved into a yml manifest, after running the the command `kubectl -f apply`, the app would immediately be deployed, retaining any previous functionailty it had beforehand.
