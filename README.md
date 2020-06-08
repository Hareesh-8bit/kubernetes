# kubernetes

1.	List all the namespaces in the cluster

Kubectl get namespaces

Kubectl get ns
2.	List all the pods in all namespaces

Kubectl get po –all-namespaces
3.	List all the pods in the particular namespaces

Kubectl get po –n <namespace name>
4.	List all the services in the particular namespace

Kubectl get svc –n <namespace name>
5.	List all the pods showing name and namespace with a json path expression

Kubectl get pods –o=jsonpath=”{.items[*] [‘meadata.name’, ‘metadata.namespace’]}”


6.	Create an nginx pod in a default namespace and verify the pod running

//creating a pod
Kubectl run nginx –image=nginx –restart=Never

//list the pod
Kubectl get po

7.	Create the same nginx pod with a yaml file

//get the yaml file with - -dry-run flag

Kubectl run nginx –image=nginx –restart=Never –dry –run –o yaml > nginx-pod.yaml

//cat nginx –pod.yaml

apiVersion : V1
kind: Pod
metadata:
     createionTimestamp: null
     labels :
          run: nginx
     name nginx
spec:
    containers:
-	Image: nginx
Name: nginx
Resources: {}
                 dnsPolicy: ClusterFirst
                  restartPolicy : Never
                   
            status: {}
// create a pod
Kubectl create –f nginx-pod.yaml
8.	Output the yaml file of the pod you just created

Kubectl get po nginx –o yaml

9.	Output the yaml file of the pod you just created without the cluster-specific information
Kubectl get po nginx –o ymal –export
10.	Get the complete details of the pod you just created
Kubectl describe pod nginx
11.	Delete the pod you just created

Kubectl delete po nginx

12.	 Delete the pod you just created without any delay (force delete)
Kubectl delete po nginx –grace-period=0 --force
13.	Create the nginx pod with version 1.17.4 and expose it on port 80

Kubectl run nginx –image=nginx:1.17.4 –restart=Never –port=80

14.	Change the image version to 1.15-alpine for the pod you just created and verify the image version is updated

Kubectl set image pod/nginx nginx=nginx:1.15-alpine

Kubectl describe po nginx

//another way it will open vi editior and change the version

Kubectl edit po nginx
Kubectl describe po nginx

15.	Change the image version back to 1.17.1 for the pod you just updated and observe the changes
Kubectl set image pod/nginx nginx=nginx:1.17.1
Kubectl describe po nginx
Kubectl get po nginx –w # watch it
16.	Check the image version without the describe command
Kubectl get po nginx –o jsonpath= ‘ {.spec.containers[].image} {“\n”} ‘

17.	Create the nginx pod and execute the simple shell on the pod

Kubectl run nginx –image=nginx –restart=Never

//exec into the pod
Kubectl exec –it nginx /bin/sh

18.	Get the IP address of the pod you just created 
Kubectl get po nginx –o wide
19.	Create a busybix pod and run command ls while creating it and checking the logs

Kubectl run busybox –image=busybox –restart=Never  -- ls

Kubectl logs busybox

20.	If pod crashed check the previous logs of the pod
Kubectl logs busybox –p

21.	Create a busybix pod with command sleep 3600

Kubectl run busybox –image-busybox –restart=Never -- /bin/sh –c “sleep 3600”

22.	Check the connection of the nginx pod from the busybox pod
Kubectl get po nginx –o wide

//check the connection
Kubectl exec –it busybox   --   wget  –o- <ip address>
23.	Create a busybox pod and echo message ‘how are you’ and delete it manually

Kubectl run busybox –image=busypod –restart=Never –it – echo “how are you”.

Kubectl delete po busybox

24.	Create a busybox pod and echo message ‘how are you’ and deleted immediately

//notice the - -rm flag

Kubectl run busybox - - image =nginx –restart=Never –it - -rm - -echo “How are you”

25.	Create an nginx pod and list the pod with different levels of verbosity

//create a pod
Kubectl run nginx –image –nginx –restart=Never –port=80

//list the pod with different verbosity
Kubectl get po nginx - -v=7
Kubectl get po nginx  - -v=8
Kubectl get po nginx  - -v=9




 

 
