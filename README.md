# tutorial11-adpro Part 1 Reflection

1.  Compare the application logs before and after you exposed it as a Service.
Try to open the app several times while the proxy into the Service is running.
What do you see in the logs? Does the number of logs increase each time you open the app?

Before being exposed as a service:
<img width="635" alt="image" src="https://github.com/PascalPahlevi/tutorial11-adpro/assets/143638456/04bd654c-be90-4ef1-98d1-6edf7245c247">

After being exposed as a service:
<img width="630" alt="image" src="https://github.com/PascalPahlevi/tutorial11-adpro/assets/143638456/06d9ccf5-394a-4ca1-b2b6-b180e85d96e9">

When comparing these two screenshots, it is quite obvious what the differences between the two are. To begin with, prior to the application being exposed as a service, the application logs only showed two lines, those being "Started HTTP server on port 8080" and "Started UDP server on pot 8081". From these two messages, we can say that before the application was exposed as a service, the application was simply initiating a server, not allowing any access to it. However, in the second screenshot, we can see that two more lines were added to the application logs after it was exposed as a service and both of those lines showed "Get/". What we can get from this is that as soon as the application was exposed as a service, access to the application was essentially enabled hence when accessed, a get protocol was established in order to get the necessary data to appear on the application.
 
2.  Notice that there are two versions of `kubectl get` invocation during this tutorial section.
The first does not have any option, while the latter has `-n` option with value set to
`kube-system`.
What is the purpose of the `-n` option and why did the output not list the pods/services that you
explicitly created?

# tutorial11-adpro Part 2 Reflection

1. What is the difference between Rolling Update and Recreate deployment strategy?
2. Try deploying the Spring Petclinic REST using Recreate deployment strategy and document
your attempt.
3.  Prepare different manifest files for executing Recreate deployment strategy
4. What do you think are the benefits of using Kubernetes manifest files? Recall your experience
in deploying the app manually and compare it to your experience when deploying the same app
by applying the manifest files (i.e., invoking `kubectl apply -f` command) to the cluster.
