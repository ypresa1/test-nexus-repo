# Troubleshooting Pods
Some of the errors you might receive with pods are: 

## Stuck in Pending Status
Some pods get stuck in Pending, but to verify check the messages found on the status. To see the status and logs of your pod: 

`$ oc describe pod <pod-name>`
`$ oc logs <pod-name>`

You can cancel an in-progress deployment: 
	
`$  oc deploy <config-name> --cancel`

If you do not have any pending deployments, create a new one: 

`$ oc deploy <config-name> --latest`

**Note: There could be many issues to a Pod stuck in Pending. This indicates that the Pod has not been scheduled yet and could be for a number of reasons including not having enough resources. It is very important to check the details and status of your pod.**

## Stuck in CrashLoopBackOff
The Pod has been started and deployed but keeps getting terminated and stuck on a never ending loop. 
