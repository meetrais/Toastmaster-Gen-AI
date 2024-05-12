# Toastmaster-Gen-AI - WORK IN PROGRESS

## Introduction
Gen-AI specialized chatbot designed to answer fundamental questions about Toastmaster program. This project demonstrates how to develop retrieval sugmented generation based chat-bot using Azure Open-AI service and Azure Cosmos-Db for Mongo-DB VCore. Following are main functionalities of this project.  
1. Create database, collection and vector-index in Mongo-DB VCore cluster.  
2. Create and save embeddings for PDF file in Mongo-DB VCore database.  
3. Perform plain vector search for user query/question.  
4. Perform chat-completion for user query/question.
   
## Code Overview
### Folder/File Structure
![image](https://github.com/meetrais/Toastmaster-Gen-AI-RAG/assets/17907862/5966ffc6-dad2-49eb-8d5e-38b070a9bb21)

## Deployment

### Docker Deployment
Once you tested your backend and frontend apps in your local its time to deploy them to Docker.  

Run below commands in the terminal of VS-Code/IDE to deploy and run backend app in Docker.  
cd backend  
docker build -t toastmaster-gen-ai-backend .  
docker run --name toastmaster-gen-ai-backend -p 5000:5000 -d toastmaster-gen-ai-backend  

Then run below commands to deploy and run frontend app in Docker.  
cd..  
cd frontend  
docker build -t toastmaster-gen-ai-frontend .  
docker run --name toastmaster-gen-ai-frontend -p 7860:7860 toastmaster-gen-ai-frontend  

Both the above containers needs to be in the same Docker network so run below commands.  
docker network create toastmaster-network  
docker network connect toastmaster-network toastmaster-gen-ai-backend  
docker network connect toastmaster-network toastmaster-gen-ai-frontend  

### Azure Deployment
I use VS Code for development and deployments. So following steps use VS-Code and its Docker and Azure plugins. But you can also do all those steps using Azure CLI commands.

***Create Azure Container Registry***
1. In Docker plugin click on your Azure Subscription and select Create Registry then follow steps to create ACR. You may have to login to Azure.  
![image](https://github.com/meetrais/Toastmaster-Gen-AI-RAG/assets/17907862/73f78e03-e779-4907-a234-e547ef942a98)

2. If you already have ACR in your Azure Subscription then you can connect to it as below.  
![image](https://github.com/meetrais/Toastmaster-Gen-AI-RAG/assets/17907862/a3d4c095-9d25-4666-b72a-38e7c3abac79)

***Deploy Docker Image of Backend app to ACR***
1. In Docker plugin inside IMAGES section locate your Image of backend app and then right-click and select Tag option.
![image](https://github.com/meetrais/Toastmaster-Gen-AI-RAG/assets/17907862/4fb0e850-a4e9-4288-857b-138be0ce1ee6)

2. Again right-click image and select Push option and follow steps to deploy your image to Azure Container Registry. 
![image](https://github.com/meetrais/Toastmaster-Gen-AI-RAG/assets/17907862/ed837765-3e93-4b01-81fb-8dad02fdd01e)

***Create Azure Container App Environment***
1. In Azure plugin click on + sign to create new Azure resource, select "Create Container Apps Environment" option and then follow the steps. 
![image](https://github.com/meetrais/Toastmaster-Gen-AI-RAG/assets/17907862/90cd3a8c-fb3c-4726-9130-835d6ff087b0)

2. Once your Container Apps Environment is created, right-click on it and select "Create Container App" and follow the steps. Select "Container Registry" option and use 5000 for port. While doing this select ACR and Image of backend app.

![image](https://github.com/meetrais/Toastmaster-Gen-AI-RAG/assets/17907862/9c38ed68-4c0f-4da6-bd6c-59b859319926)

![image](https://github.com/meetrais/Toastmaster-Gen-AI-RAG/assets/17907862/ac57d21d-5c6c-4066-8283-8a6046be71d9)

***Deploy Docker Image of frontend app to Azure Web-App***
1. Before we deploy docker image of frontend app to Azure Web-App, make below change in app.py so frontend app will call backend app endpoint deployed in Azure Container app. Then re-deploy image of frontend app to Docker.  
![image](https://github.com/meetrais/Toastmaster-Gen-AI-RAG/assets/17907862/573702b3-2546-4020-87f1-7111d0ea4d89)

2. In Docker plugin, IMAGES section righ-click on docker image of frontend app and push to ACR. Just like we tagged and pushed docker image of backend app above.

![image](https://github.com/meetrais/Toastmaster-Gen-AI-RAG/assets/17907862/d3fb3e63-c043-4f51-a551-84b609b2508b)

3. After that you should be able to see docker image of frontend app in your ACR like below. Now right click on that image and select option "Deploy Image to Azure App Service.". Follow the steps to create Azure App Service and Service Plan. It will also deploy your docker image of frontend app to Azure App Service.

![image](https://github.com/meetrais/Toastmaster-Gen-AI-RAG/assets/17907862/46d0bc2d-0200-439c-8b2e-bec9baa81a19)

## Showtime
If you followed all the steps properly you should be able to see result of Retrieval Augmented Generation based Chat-Bot as below. 

![image](https://github.com/meetrais/Toastmaster-Gen-AI-RAG/assets/17907862/0b07101b-e0a3-4b62-8674-f7a792a0487b)

If it doesnt work then reach out to me and I will be happy to help.

