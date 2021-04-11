# DemoAzureServiceBus
Demo to use Services of queues / send messages and receive 

Prerequisites

It's necessary to have account in Azure and to install Visual Studio Code. 

Steps

1- Acess your Account in Azure (https://portal.azure.com )
2 - Create a Service Bus namespace and queue using the Azure Cli 
3- Open a new session of Azure Cli into your brownser 
![image](https://user-images.githubusercontent.com/22642792/114311805-9d686a00-9ac6-11eb-8e94-04b50edbe33f.png)


4- Will go to create a new Resource Group (I created my resource group using eastus but you can to use other location (see more: https://docs.microsoft.com/en-us/cli/azure/manage-azure-groups-azure-cli))

  Command:
  
  myLocation=eastus
  myResourceGroup="svcbusdemo-rg"
  az group create -n $myResourceGroup -l $myLocation
  
 5- Create a Service Bus namespace and a queue
  Note - The Service Bus namespace is unique.
  
   - Create a Service Bus namespace
    namespaceName=svcbus$RANDOM
    az servicebus namespace create \
    --resource-group $myResourceGroup \
    --name $namespaceName \
    --location $myLocation
    ![image](https://user-images.githubusercontent.com/22642792/114310797-7871f800-9ac2-11eb-8324-acd04b820eab.png)

   - Create a queue
   az servicebus queue 
   
   create --resource-group $myResourceGroup \
  --namespace-name $namespaceName \
  --name svcbusqueue
  
 6 - Now get connection string that you use into your project - After cloning the project replace a variable connection string (ServiceBusConnectionString - Program.cs) with the content of your connection 
 
 connectionString=$(az servicebus namespace authorization-rule keys list \
--resource-group $myResourceGroup \
--namespace-name $namespaceName \
--name RootManageSharedAccessKey \
--query primaryConnectionString --output tsv)
echo $connectionString
![image](https://user-images.githubusercontent.com/22642792/114311755-5bd7bf00-9ac6-11eb-9e62-81e6e33b8920.png)


 7 - Use Dotnet Run command to start bother projects
 
 
 
 
 
