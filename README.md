Create Jenkins pipeline to build and deploy microservice-1 to the local cluster. #1

# microservice-1
This repo holds a sample microservice to be deployed to Kubernetes

Congiure Jenkins
1. Manage Jenkins->Congiure system-> environmental variable
Name: ORGANIZATION_NAME value: Your Github organization name
2. Cloud->Add kubernete->Add cluster url and namespace
3. Manage Jenkins ->Global tool configuration
Add gradle installer
4. Manage Jenkins-> Manage credentials
Create personal access token in github with user jenkins-user
Add them to jenkins credentials with ID GitHub
5. Create a multibranch  pipeline 
Add branch source github-> Select user ->add repo url
Add owner name as organization name and select repo and save
