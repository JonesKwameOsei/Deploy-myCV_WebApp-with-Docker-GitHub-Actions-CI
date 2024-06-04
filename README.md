# Build Docker Images with GitHub Actions For My CV WebApp
## Automatically build Docker images with GitHub Actions
![dockergithub](https://github.com/JonesKwameOsei/Build-Docker-Images-with-GitHub-Pipeline-Actions/assets/81886509/f4cc3521-f027-48b7-aa37-fd13f9321680)


## Overview
This project demonstrates how to automatically build Docker images using GitHub Actions. By integrating Docker and GitHub Actions, DevOps engineers can create a seamless **CI/CD (Continuous Integration/Continuous Deployment)** pipeline for projects, ensuring that Docker images are built and pushed to a registry whenever changes are made by developers to the codebase.

## Step-by-Step Process

### 1. Wep Application Development
I developed the web application with the DotNet (.NET) SDK framework which is programmed in C# languaue. 

### 2. Create a GitHub Repository
Begin by creating a new GitHub repository for your project. This will be the central location for your code, configurations, and the GitHub Actions workflow.<p>
1. Open a new terminal in VScode.
2. Create a directory with a repo name you desire (named mine `Deploy-Webapp-with-Kubernetes`).
3. Initialise directory by running:
```
git init
```
4. Use **HuB** to change the local directory to a remote repo. Run:
```
hub create
```
5. Optional: Add README.md (but recommended).
```
echo "## Automatically build Docker images with GitHub Actions" >> README.md
```
6. Push the new repo to GitHub.
```
git add README.md
git commit -m "first commit"
git branch -M main
git push -u origin main
```
if you do not have Hub installed, manually create a github repo and run this command in the terminal:
```
git remote add origin https://github.com/<github-username>/<repo-name>.git
```
For step by step process of creating a github repo from thr terminal, check this [project](https://github.com/JonesKwameOsei/Deploy-Webapp-with-Kubernetes)

### 2. Create the Dockerfile and Package File
In the repository:
- Create a file called Dockerfile.
```
nano Dockerfile
```
- Add these lines of codes:
```
#See https://aka.ms/customizecontainer to learn how to customize your debug container and how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
USER app
WORKDIR /app
EXPOSE 8080
EXPOSE 8081

FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
ARG BUILD_CONFIGURATION=Release
WORKDIR /src
COPY ["myWebCVApp/myWebCVApp.csproj", "myWebCVApp/"]
RUN dotnet restore "./myWebCVApp/myWebCVApp.csproj"
COPY . .
WORKDIR "/src/myWebCVApp"
RUN dotnet build "./myWebCVApp.csproj" -c $BUILD_CONFIGURATION -o /app/build

FROM build AS publish
ARG BUILD_CONFIGURATION=Release
RUN dotnet publish "./myWebCVApp.csproj" -c $BUILD_CONFIGURATION -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "myWebCVApp.dll"]

```
- Perform the steps above to create and add the lines below to the myWebCVApp.csproj.
```
<Project Sdk="Microsoft.NET.Sdk.Web">

  <PropertyGroup>
    <TargetFramework>net8.0</TargetFramework>
    <Nullable>enable</Nullable>
    <ImplicitUsings>enable</ImplicitUsings>
    <UserSecretsId>2f4575b4-591c-4e4f-9ba0-9892f29c50ae</UserSecretsId>
    <DockerDefaultTargetOS>Linux</DockerDefaultTargetOS>
  </PropertyGroup>

  <ItemGroup>
    <PackageReference Include="Microsoft.VisualStudio.Azure.Containers.Tools.Targets" Version="1.20.1" />
  </ItemGroup>

</Project>
```
### 3. Set up the Docker Build Workflow
In the GitHub repository, create a new folder named `.github/workflows`. This is where the GitHub Actions workflow is defined.

Inside the `workflows` folder, create a new file named `dockerhub-push.yml`. This file will contain the configuration for the Docker build workflow.

```
name: Build and Push Docker image to Docker Hub

on:
  push:
    branches: [ "main" ]
  pull_request:
    branches: [ "main" ]

jobs:
  push_to_registry:
    name: Push Docker image to Docker Hub
    runs-on: ubuntu-latest
    steps:
      - name: Check out the repo
        uses: actions/checkout@v4
    
    - name: Set up Docker Buildx
      uses: docker/setup-buildx-action@v1
      
    - name: Login to Docker Hub
        uses: docker/login-action@v2
        with:
          username: ${{ secrets.DOCKERHUB_USERNAME }}
          password: ${{ secrets.DOCKERHUB_TOKEN }}
    
    - name: Build and push Docker image
        uses: docker/build-push-action@v4
        with:
          context: DockerFileFolder/
          push: true
          tags: rekhugopal/testrepo:latest
```

This workflow will be triggered on push and pull request events to the `main` branch. It performs the following steps:

1. Checks out the repository code.
2. Sets up the Docker Buildx environment for multi-architecture builds.
3. Logs in to the GitHub Container Registry (ghcr.io) using the `GITHUB_TOKEN` secret.
4. Builds the Docker image and pushes it to the GitHub Container Registry, tagging it with the current commit SHA.

### 4. Generate Docker Hub Access Token
The need for a Docker Hub access token when using GitHub Actions to build and push Docker images is related to authentication and authorization.
When you want to push a Docker image to a registry, such as Docker Hub, the registry needs to verify that you have the necessary permissions to do so. This is where the access token comes into play.
Here are the key reasons why you need a Docker Hub access token for GitHub Actions:

1. **Authentication**: The access token acts as a credential that authenticates your GitHub Actions workflow with Docker Hub. Without the token, the workflow would not be able to prove its identity to the registry and gain access to push the image.

2. **Authorization**: The access token grants the necessary permissions to your GitHub Actions workflow to push the Docker image to your specific Docker Hub account or organization. This ensures that only authorized parties can push images to the designated registry location.

3. **Security**: Using an access token is more secure than hardcoding your Docker Hub username and password directly in your GitHub Actions workflow. Access tokens can be managed and revoked separately, providing better control and security over your credentials.

By providing the Docker Hub access token as a secret in the GitHub Actions workflow, we can securely authenticate your workflow and grant it the required permissions to push the Docker image to the desired registry location on Docker Hub.

This approach is a best practice for managing credentials in the CI/CD pipelines, as it separates the sensitive information from the workflow code and ensures better security and maintainability of the build and deployment processes.
- In `Docker Hub`, click on the `Docker Hub Profile` on the top right corner.<p>
![image](https://github.com/JonesKwameOsei/Build-Docker-Images-with-GitHub-Pipeline-Actions/assets/81886509/6eaa67b7-f464-497b-8985-ec6e3fe50367)<p>
- Select `My Account `.
- Select `Security`.<p>
![image](https://github.com/JonesKwameOsei/Build-Docker-Images-with-GitHub-Pipeline-Actions/assets/81886509/9c1a3c03-0f51-4537-8159-ef9668278e26)<p>
- Click the `New Access Token` button.<p>
![image](https://github.com/JonesKwameOsei/Build-Docker-Images-with-GitHub-Pipeline-Actions/assets/81886509/e16438c4-eba3-4167-a1b1-fe6ae4d67b2d)<p>
- In the `Access Token Description` field, enter a description `GithubAction` for the token.<p>
![image](https://github.com/JonesKwameOsei/Build-Docker-Images-with-GitHub-Pipeline-Actions/assets/81886509/c6b17bd1-11ff-495e-a392-64f4f0e61774)<p>
- Leave the next field as default and click `Generate Token`.
- Copy the token generated and close the pane. <p>
![image](https://github.com/JonesKwameOsei/Build-Docker-Images-with-GitHub-Pipeline-Actions/assets/81886509/d3207ccd-ca38-476c-9949-c0ee064c94ae)<p>

### 5. Store Secrets in Github Actions
1. In the Github repo, click on settings.
2. On the left silde, find `Secrets and Variables`, click the dropdown and select `Actions`.
![image](https://github.com/JonesKwameOsei/Build-Docker-Images-with-GitHub-Pipeline-Actions/assets/81886509/9ec60cc6-8df0-4905-a16d-76f78d180c87)<p>
3. Under the `Repository secrets`, click on the green button, `New repository Secret`.
4. For `Name` and `Secret`, enter details of the following:<p>

|Name|Secret|
|----|------|
|DOKERHUB_USERNAME|Your docker username|
|DOKERHUB_TOKEN|The access token generated|<p>

The configuration should look like this:<p>
![alt text](image-1.png)<p>

### 6. Run the GitHub Actions Workflow

2. Add the changes and commit
```
git add .
git commit -m "Added configuration files"
```
3. Push the commit to trigger the actions
```
git push origin main
```
Commit and push the changes to the `main` branch of your GitHub repository. This will trigger the `docker-build.yml` workflow, which will automatically build and push your Docker image to the GitHub Container Registry.In the "Actions" tab of the GitHub repository, we can monitor the progress and check the status of the workflow run.<p>

The pipeline action is running.<p>
![image](https://github.com/JonesKwameOsei/Build-Docker-Images-with-GitHub-Pipeline-Actions/assets/81886509/defd6bd1-a3ed-43bd-ad0d-0fcf54bc39f4)<p>
GitHub action completed.We will confirm if the the image is in the `Docker Hub` registry. 
![image](https://github.com/JonesKwameOsei/Build-Docker-Images-with-GitHub-Pipeline-Actions/assets/81886509/76437dc2-b45f-459f-870e-2b2a83a0207a)<p>
Image in docker hub.<p>
![image](https://github.com/JonesKwameOsei/Build-Docker-Images-with-GitHub-Pipeline-Actions/assets/81886509/ee0d34c9-9c9f-4a12-a4cc-3449458f3050)

## Conclusion
By leveraging GitHub Actions, I have seamlessly integrated Docker into a development pipeline. This approach allow us to automatically build and push Docker images to a registry, ensuring that the deployments are consistent and up-to-date with the latest changes to the codebase. This setup provides a reliable and efficient way to manage the Docker-based applications.
