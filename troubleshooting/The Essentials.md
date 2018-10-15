# The Essentials
These commands are considered to be a base to start troubleshooting. You will be able to find more information and identify some issues using these commands.

## Nodes 
Verify docker is running: 

`$ systemctl status docker` 

For a brief view of Nodes Name, Status, Age, and Version:

`$ oc get nodes` 

For more details of a specific node:

`$  oc describe node <node-name>`

## Pods
For a brief view of Pod Name, Status, Restarts and Age: 

`$ oc get pods` 

For brief view of Pod Name, Status, Restarts, Age, IP and Node it is running on: 

`$ oc get pods -o wide` 

To look at Pods event:

`$ oc describe pod <pod-name>` 

Checking logs for a specific Pod: 

`$ oc logs <pod-name>` 

## Projects
To view all projects:

`$ oc projects`

To change to a specific project: 

`$ oc project <project-name>`

To see a brief status of project you are currently in:

`$ oc status` 
