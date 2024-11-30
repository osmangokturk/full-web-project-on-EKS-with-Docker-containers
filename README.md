# full-web-project-on-EKS-with-Docker-containers
complete web project with additional service to add entries to a phonebook on mysql; 
the second service,Result Server, will only search data from the database which is persistent on  ? 

# Prerequisites
- EKS resources on a cloud provider like AWS. you can refer to my repo on "creating aws eks resources with terrafrm" repository. these resources includes kubectl component.
- images created and pushed on the docker-hub. See my repo on how to create a docker image. we are going to use docker images locating on my dockerhob repos. you can  refer to public repos or your own repos. osmangokturk/ and osmangokturk/
-
# Project manifest files resources
We have deployment.yaml, service.yaml for "web-server", "result-server", MySQL,
besides we have a PersistentVolume(PV.yaml) and (PersistentVolumeClaim (PVC.yaml) for persistent volume on ?
And additionally we have secret.yaml file to to manage sexrets required for mySQL like root-pasword and admin and his password.
admin name can be modified where?
Lastly we have a mysql-configmap.yam that contain enviornmet variables for mySQL to access database,
and similaryly servers-configmap.yaml to provide the envionment variables for web-service and resultservice to 
access database and .dab name, username, and Host parameters.
environment variables are defined in the each depöoyment file for each servie. for example the result-server deployment include a reference to the file servers-configmap.
The servers-configmap includes 3 data which are the values for databes name,database-user name, nad db host name which is set to mysql-deploy.
for the environment variables requirent for the setup of servers, meysql  refer to mysql documentation. 

For sections in each manifest refer to their documentatin. 
in this project my focus is to provide a complete deployment with nodePort 
where a client can acces in his browser with workerNodeIP: nodeport defined in the service.yaml.
For a complete guide refer to my project on the kubernetes manifest files. 

# copy your manifest to the cluster(master node)
```bash
scp -r -i C:\Users\xx\Downloads/myKeyPair.pem  C:\Users\xxx\/Downloads/myDocs ubuntu@MasterNODEIP:~/

-r means folders, -i for key pair the first argument is the place of keypari, the second place the folder to be copied, the third argument is the place on the remote to put the code. here we put into home.

will copy files from your local to the clıster. 
establish an ssh tunnel to your cluster to apply 

With all our  files ready (11 yaml files), we can apply wiht  `kubectl apply -f . `.
Dot here refers to all files, as the -f option in "kubectly apply"  is recursive by default. 

Now the container and services are created.

#Result:
go get the ip or domain name from your worker node, and brows in a webbroser like IP:3001 or 30002 as we have defined the nodeport in the services like that. 
