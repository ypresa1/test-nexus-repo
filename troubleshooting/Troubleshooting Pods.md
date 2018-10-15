# Troubleshooting Pods
Some of the errors you might receive with pods are: 

## Pending Status
Some pods get stuck in Pending, but to verify check the messages found on the status. To see the status and logs of your pod: 

`$ oc describe pod <pod-name>`
`$ oc logs <pod-name>`

You can cancel an in-progress deployment: 
	
`$  oc deploy <config-name> --cancel`

If you do not have any pending deployments, create a new one: 

`$ oc deploy <config-name> --latest`

**NOTE: There could be many issues to a Pod stuck in Pending. This indicates that the Pod has not been scheduled yet and could be for a number of reasons including not having enough resources. It is very important to check the details and status of your pod.**

## CrashLoopBackOff
The Pod has been started and deployed but keeps getting terminated and stuck on a never ending loop. 

To view the logs for the pod: 

`$ oc describe pod <pod-name>`
`$ oc logs <pod-name>`

The outcome will show you the reason for the crashing. 

## ImagePullBackOff
The Pod cannot pull the image after several times of trying. The two most common problems are either: 
	1. Incorrect image name 
	2. Incorrect docker secret 
	
To verify if the image you are using is correct: 

`$ docker pull <image>`

For certain images, a docker registry secret needs to be created. For example when using Red Hat Container Catalog you first need to login using docker, replacing the information with your Red Hat account info: 

` $ docker login -u <user> -p <passwd> registry.connect.redhat.com`

**NOTE: The above command should complete with Login Succeeded. If this isn't the case and your password contains special characters, try encapsulating it in quotes.**

Create the image pull secret by referencing the docker config.json file that was created by the previous docker login command:

`$ oc create secret generic rhcc \
--from-file=.dockerconfigjson=/root/.docker/config.json \
--type=kubernetes.io/dockerconfigjson`

Create a service account named sysdig-agent:

`$ oc create serviceaccount sysdig-agent`

Finally, link the newly created secret to the sysdig-agent service account:

`$ oc secrets link sysdig-agent rhcc --for=pull`




