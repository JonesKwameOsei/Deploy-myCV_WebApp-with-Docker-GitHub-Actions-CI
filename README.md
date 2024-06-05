# Build Docker Images with GitHub Actions For My CV WebApp
## Automatically build Docker images with GitHub Actions
![dockergithub](https://github.com/JonesKwameOsei/Build-Docker-Images-with-GitHub-Pipeline-Actions/assets/81886509/f4cc3521-f027-48b7-aa37-fd13f9321680)


## Overview
This project demonstrates how to automatically build Docker images using GitHub Actions. By integrating Docker and GitHub Actions, DevOps engineers can create a seamless **CI/CD (Continuous Integration/Continuous Deployment)** pipeline for projects, ensuring that Docker images are built and pushed to a registry whenever changes are made by developers to the codebase.

## Step-by-Step Process

### 1. Wep Application Development
I developed the web application using `C#` the .NET SDK framework. Utilising thw ASP.NET for web application, I was able to build this simple web application for my CV. In efficiently created this simple CV web application using the ASP.NET Core Razor pages. The steps are listed below:<p>
**Step One: Create a New ASP.NET Core Project**
- Open Visual Studio. Download it [here.](https://visualstudio.microsoft.com/thank-you-downloading-visualstudio/sku=Community&channel=Release&version=VS2022&source=VSLandingPage&cid=2030&passive=false).
- Select "Create a new project".
- Select "ASP.NET Core Web App" and click "Next".
- Configure the project details and click "Create".
- Select ".NET 8.0 (or later)" and click "Create".<p>

**Step Two: Set Up the Layout**
- In the Pages folder, modify the `Shared/_Layout.cshtml` file to include a background of your choice. I chose to go with a dark background and link to the CSS.
- Add `class="bg-dark text-white"` to the open body tag to look like this:<p>
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>@ViewData["Title"] - My CV</title>
    <link rel="stylesheet" href="~/css/site.css" />
</head>
<body class="bg-dark text-white">           # This is where to modify the background colour
    <div class="container">
        <main role="main" class="pb-3">
            @RenderBody()
        </main>
    </div>
    <script src="~/lib/jquery/dist/jquery.min.js"></script>
    <script src="~/lib/bootstrap/dist/js/bootstrap.bundle.min.js"></script>
    <script src="~/js/site.js" asp-append-version="true"></script>
    @RenderSection("Scripts", required: false)
</body>
</html>
```
**Step Three: Create the CV Page**
- Add a new Razor Page to the Pages folder named CV.cshtml.
```
@page
@model Pages_CV
@{
    ViewData["Title"] = "My CV";
}

<div class="cv">
    <div class="header text-center">
        <img src="~/images/profile.png" class="profile-img" alt="Profile Photo" />
        <h1>Jones Osei</h1>
        <p>DevOps Engineer</p>
        <p>
            <a href="mailto:oseikwamejones@gmail.com" class="text-email">oseikwamejones@gmail.com</a> |
            <a href="tel:+44 7943 645 460" class="text-phone">+44 7943 645 460</a>
        </p>
        <p>
            <a href="https://www.linkedin.com/in/kwameds/" class="text-linkedin">LinkedIn</a> |
            <a href="https://github.com/JonesKwameOsei" class="text-github">GitHub</a>
        </p>
    </div>
    <div class="content">
        <section>
            <h2><u>Professional Summary</u></h2>
            <p>
                A DevOps Engineer with hands-on experience of containerising applications with Docker ensuring maximum security and performance optimisation.
                Utilised Helm and Kubernetes to orchestrate containers with 98% High Availability synchronization and 99% full security features. 
                Provisioned secured and scalable infrastructure in the cloud. 
            </p>
        </section>
        <section>
            <h2><u>Professional Experience</u></h2>
            <div class="experience">
                <h3>DevOps Consultant</h3>
                <p class="company">Jomacs IT Consult, Birmingham, UK</p>
                <p class="dates">June 2023 - Present</p>
                <ul>
                    <li>Implemented an automated deployment pipeline using Git, Jenkins, and Docker, reducing deployment time by 50% and increasing release frequency by 75%.</li>
                    <li>Orchestrated a Kubernetes cluster for a production environment, improving scalability and resource utilization, leading to a 30% reduction in infrastructure costs.</li>
                    <li>Developed and maintained a comprehensive CI/CD pipeline using Jenkins, Maven, and Git, resulting in a 90% reduction in manual build and deployment processes.</li>
                    <li>Implemented infrastructure as code using CloudFormation and Terraform to provision AWS resources such as EC2 instances, S3 buckets, and RDS databases, resulting in a 57% reduction in maintenance costs.</li>
                    <li>Applied automated testing to ensure continuous service availability using AWS Lambda and Amazon CloudWatch alarms.</li>
                    <li>Performed project monitoring, tracking, and reporting with Grafana and Prometheus.</li>
                </ul>
                <p><strong>Achievements:</strong></p>
                <ul>
                    <li>Automated integration and deployment processes, eliminating human error by 99% resulting in a 90% reduction in manual build and deployment processes.</li>
                    <li>Increased continuous delivery and deployment speed by 75% and leading to a 30% reduction in infrastructure costs.</li>
                    <li>Automated planned and exploratory tests, improving release quality by 69%.</li>
                </ul>
            </div>
            <div class="experience">
                <h3>DevOps Engineer</h3>
                <p class="company">Dunwell Health Service, Birmingham, UK</p>
                <p class="dates">January 2022 - June 2023</p>
                <ul>
                    <li>Packaged and built applications with Maven, NPM, Python, and NuGet, managing them with Azure Artifacts.</li>
                    <li>Dockerized and deployed applications to Azure Kubernetes Services (AKS).</li>
                    <li>Utilized Azure Pipelines to create continuous integration and continuous deployment pipelines from scratch.</li>
                    <li>Used Terraform to provision infrastructure and resources in Microsoft Azure Cloud.</li>
                    <li>Performed project monitoring, tracking, and reporting with Azure Boards.</li>
                </ul>
                <p><strong>Achievements:</strong></p>
                <ul>
                    <li>Automated build processes, eliminating human error by 98%.</li>
                    <li>Increased continuous delivery and deployment speed by 72%.</li>
                    <li>Automated planned and exploratory tests, improving release quality by 69%.</li>
                </ul>
            </div>
        </section>
        <section>
            <h2>Education</h2>
            <ul>
                <li>
                    <strong>Master of Science, Data Science</strong><br />
                    University of Gloucestershire, United Kingdom
                </li>
                <li>
                    <strong>Bachelor of Education, Educational Psychology</strong><br />
                    University of Cape Coast, Ghana
                </li>
            </ul>
        </section>
        <section>
            <h2>Certifications</h2>
            <ul>
                <li>AWS Certified Cloud Practitioner</li>
                <li>Microsoft Certified: Azure Data Fundamentals</li>
            </ul>
        </section>
        <section>
            <h2>Skills</h2>
            <ul>
                <li>Linux</li>
                <li>Python</li>
                <li>Go</li>
                <li>Bashscripting</li>
                <li>Docker</li>
                <li>Kubernetes</li>
                <li>Helm</li>
                <li>Terraform</li>
                <li>Ansible</li>
                <li>Git and GitHub</li>
                <li>Jenkins CI</li>
                <li>AWS Cloud Services</li>
                <li>Azure Cloud Services</li>
            </ul>
        </section>
        <section>
            <h2>Projects</h2>
            <ul>
                <li>
                    <strong>Super-Mario-Deployment-on-AWS-EKS-with-using-Terraform-Kubernetes</strong><br />
                    <p>
                        The deployment of the popular game Super Mario on Amazon Elastic Kubernetes Service (EKS) using Terraform and Continuous Integration/Continuous Deployment (CI/CD) pipelines.
                    </p>
                    <p>
                        <a href="https://github.com/JonesKwameOsei/Super-Mario-Deployment-on-AWS-EKS-with-using-Terraform-Kubernetes" class="text-project-link">Project Link</a>
                    </p>
                </li>
                <li>
                    <strong>Deploying an Online Boutique Web Application with Kubernetes</strong><br />
                    <p>
                        Deploy an online shopping application with Kubernetes.
                    </p>
                    <p>
                        <a href="https://github.com/JonesKwameOsei/Deploy-Webapp-with-Kubernetes" class="text-project-link">Project Link</a>
                    </p>
                </li>
            </ul>
        </section>
        <section>
            <h2>Contact Information</h2>
            <p>
                Email: <a href="mailto:oseikwamejones@gmail.com" class="text-email">oseikwamejones@gmail.com</a><br />
                Phone: <a href="tel:+44 7943 645 460" class="text-phone">+44 7943 645 460</a><br />
                LinkedIn: <a href="https://www.linkedin.com/in/kwameds/" class="text-linkedin">https://www.linkedin.com/in/kwameds/</a><br />
                GitHub: <a href="https://github.com/JonesKwameOsei" class="text-github">https://github.com/JonesKwameOsei</a>
            </p>
        </section>
    </div>
</div>
```

**Step 4: Add CSS for Styling**
- In the wwwroot/css/site.css file, add the following CSS to style the CV page:
```
/* Formatting the web pages */
html {
  font-size: 14px;
}

@media (min-width: 768px) {
  html {
    font-size: 16px;
  }
}

.btn:focus, .btn:active:focus, .btn-link.nav-link:focus, .form-control:focus, .form-check-input:focus {
  box-shadow: 0 0 0 0.1rem white, 0 0 0 0.25rem #258cfb;
}

html {
  position: relative;
  min-height: 100%;
}

/* Style the visible content */
body {
    font-family: Arial, sans-serif;
    background-color: #1a1a1a;
    color: white;
    margin: 0;
    padding: 0;
}

.cv {
    padding: 20px;
    background-color: #2c2c2c;
    color: white;
    border-radius: 10px;
    margin: 20px auto;
    max-width: 800px;
}

.header {
    text-align: center;
    margin-bottom: 20px;
}

.profile-img {
    border-radius: 50%;
    width: 150px;
    height: 150px;
    margin-bottom: 20px;
}

h1, h2 {
    color: #00bfff;
}

.content section {
    margin-bottom: 20px;
}

ul {
    list-style-type: circle;
    padding: 0;
}

ul li {
    margin-bottom: 10px;
}

a.text-light {
    color: #00bfff;
    text-decoration: none;
}

a.text-light:hover {
    text-decoration: underline;
}

a.text-email {
    color: #0e76a8; /* LinkedIn blue color */
}

a.text-phone {
    color: #0e76a8; /* LinkedIn blue color */
}

a.text-linkedin {
    color: #0e76a8; /* LinkedIn blue color */
}

a.text-github {
    color: #0e76a8; /* LinkedIn blue color */
}

a.text-project-link {
    color: #00bfff; /* Light blue for project links */
    text-decoration: none;
}
a.text-project-link:hover {
   text-decoration: underline;
}
.experience {
    margin-bottom: 20px;
}
.company {
    font-style: italic;
    color: #cccccc;
}
.dates {
    font-weight: bold;
    color: #999999;
}
```
**Step 5: Run the Application**
- To run the application, press F5 or click the "Run" button in Visual Studio.In the browser, Navigate to /CV (localhost:home/cv) to view the CV page.

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

### 3. Set Up Dockerfile:
Create a `Dockerfile` in the root directory of your `ASP.NET` web application. 
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
### 4. Set up the Docker Build Workflow
In the GitHub repository, create a new folder named `.github/workflows`. This is where the GitHub Actions workflow is defined.

Inside the `workflows` folder, create a new file named `dockerhub-push.yml`. This file will contain the configuration for the Docker build workflow.

```
name: Dockerise and Push Docker image CI

on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v2

      - name: Set up Docker Buildx
        uses: docker/setup-buildx-action@v1

      - name: Login to Docker Hub
        uses: docker/login-action@v1
        with:
          username: ${{ secrets.DOCKER_USERNAME }}
          password: ${{ secrets.DOCKER_PASSWORD }}

      - name: Build and push Docker image
        uses: docker/build-push-action@v2
        with:
          context: .
          push: true
          tags: kwameds/mycvwebapp:2.0.0
```

This workflow will be triggered on push and pull request events to the `main` branch. It performs the following steps:

1. Checks out the repository code.
2. Sets up the Docker Buildx environment for multi-architecture builds.
3. Logs in to the GitHub Container Registry (ghcr.io) using the `GITHUB_TOKEN` secret.
4. Builds the Docker image and pushes it to the GitHub Container Registry, tagging it with the current commit SHA.

### 5. Generate Docker Hub Access Token
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

### 6. Store Secrets in Github Actions
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

### 7. Manually build and Push the Docker Image Locally
Open a terminal, navigate to the directory containing the Dockerfile, and build the Docker image.
```
docker build -t kwameds/mycvwebapp:1.0.0 .
```
Image is built:<p>
```
[+] Building 569.1s (18/18) FINISHED                                docker:default
 => [internal] load build definition from Dockerfile                          0.1s
 => => transferring dockerfile: 904B                                          0.0s 
 => [internal] load metadata for mcr.microsoft.com/dotnet/sdk:8.0             1.0s 
 => [internal] load metadata for mcr.microsoft.com/dotnet/aspnet:8.0          0.9s 
 => [internal] load .dockerignore                                             0.0s
 => => transferring context: 464B                                             0.0s 
 => [build 1/7] FROM mcr.microsoft.com/dotnet/sdk:8.0@sha256:1e0c55b0ae732  554.6s 
 => => resolve mcr.microsoft.com/dotnet/sdk:8.0@sha256:1e0c55b0ae732f333818f  0.0s
 => => sha256:4369f7f50afbe743842fb8431f68ba4c280217854a4 15.73MB / 15.73MB  53.8s 
 => => sha256:9cca61ea7dcde9e148fce1ff995332d2ad533b2d 183.59MB / 183.59MB  472.2s 
 => => sha256:843791b459d2398954cec1204e9d601346fcc7793fc 30.69MB / 30.69MB  83.2s 
 => => extracting sha256:843791b459d2398954cec1204e9d601346fcc7793fcbc522033  0.6s 
 => => extracting sha256:9cca61ea7dcde9e148fce1ff995332d2ad533b2d4c5927d344d  2.5s 
 => => extracting sha256:4369f7f50afbe743842fb8431f68ba4c280217854a444db13a5  0.3s 
 => [base 1/2] FROM mcr.microsoft.com/dotnet/aspnet:8.0@sha256:a22d22bcedc  105.5s 
 => => resolve mcr.microsoft.com/dotnet/aspnet:8.0@sha256:a22d22bcedc67df31b  0.0s 
 => => sha256:026220c9919398c3ac236b91cbf15c448fb5383eed7 11.03MB / 11.03MB  37.4s 
 => => sha256:fb5d00a9ff0e9f7f92e11503fbbdf16143ca63c8c357d82841 153B / 153B  0.8s 
 => => sha256:4ede38c3f6aeccac1e49f0cee1f685968f6502c801 32.23MB / 32.23MB  104.7s 
 => => sha256:cc7f450a69e27d8e92017b26b10f914c0adbde22f39dea 3.28kB / 3.28kB  1.0s 
 => => sha256:09f376ebb190216b0459f470e71bec7b5dfa611d66b 29.15MB / 29.15MB  88.8s 
 => => sha256:898e6be7b1d63a481b0a404455fe5b3c65450c37074 18.52MB / 18.52MB  78.2s 
 => => extracting sha256:09f376ebb190216b0459f470e71bec7b5dfa611d66bf008492b  0.7s 
 => => extracting sha256:898e6be7b1d63a481b0a404455fe5b3c65450c37074a0e386d3  0.3s 
 => => extracting sha256:cc7f450a69e27d8e92017b26b10f914c0adbde22f39dead838e  0.0s 
 => => extracting sha256:4ede38c3f6aeccac1e49f0cee1f685968f6502c801605dd4538  0.4s 
 => => extracting sha256:fb5d00a9ff0e9f7f92e11503fbbdf16143ca63c8c357d828412  0.0s 
 => => extracting sha256:026220c9919398c3ac236b91cbf15c448fb5383eed772379acf  0.1s 
 => [internal] load build context                                             0.8s 
 => => transferring context: 16.63MB                                          0.7s 
 => [base 2/2] WORKDIR /app                                                   0.6s 
 => [final 1/2] WORKDIR /app                                                  0.0s 
 => [build 2/7] WORKDIR /src                                                  1.1s 
 => [build 3/7] COPY [myWebCVApp/myWebCVApp.csproj, myWebCVApp/]              0.0s 
 => [build 4/7] RUN dotnet restore "./myWebCVApp/myWebCVApp.csproj"           3.9s 
 => [build 5/7] COPY . .                                                      0.1s 
 => [build 6/7] WORKDIR /src/myWebCVApp                                       0.0s 
 => [build 7/7] RUN dotnet build "./myWebCVApp.csproj" -c Release -o /app/bu  5.2s 
 => [publish 1/1] RUN dotnet publish "./myWebCVApp.csproj" -c Release -o /ap  2.1s 
 => [final 2/2] COPY --from=publish /app/publish .                            0.1s 
 => exporting to image                                                        0.5s 
 => => exporting layers                                                       0.4s 
 => => exporting manifest sha256:458dae421596fdd372d413e651b829acb1d3eeb93ae  0.0s 
 => => exporting config sha256:76ef9ba27503224cac6394aabcde92b83d56fc04a9605  0.0s 
 => => exporting attestation manifest sha256:23aa0b687d5e7b874cb8e3b9d312acc  0.0s 
 => => exporting manifest list sha256:26af15f605adebd95eae2e82c44b8919e151ef  0.0s 
 => => naming to docker.io/kwameds/mycvwebapp:1.0.0                           0.0s 
 => => unpacking to docker.io/kwameds/mycvwebapp:1.0.0                        0.1s 

View build details: docker-desktop://dashboard/build/default/default/hcmeaq9cb3mq23pliwjm1o0z9

What's Next?
  View a summary of image vulnerabilities and recommendations → docker scout quickview
```
We can verify from on Docker CLI if the image is actually built. To do this, run:
```
docker images
```
![image](https://github.com/JonesKwameOsei/myCV_WebApp/assets/81886509/abedb5d2-e476-497e-9fc9-2a32433ea236)<p>
Verification from Docker Desktop:<p>
![image](https://github.com/JonesKwameOsei/myCV_WebApp/assets/81886509/5f2a882c-293e-49f7-be4d-4e75d4f20970)<p>

Next, we will run the Docker Image Locally. This is to test the image locally to ensure it works correctly.
```
docker run -d -p -- name mycvwebapp 8080:8080 kwameds/mycvwebapp:1.0.0
```
The application access at http://localhost:8080.<p>
![image](https://github.com/JonesKwameOsei/myCV_WebApp/assets/81886509/4a6a6940-c4a4-4442-b769-3e4c6fb7b2c3)<p>
The `Home Page` is live:<p>
![image](https://github.com/JonesKwameOsei/myCV_WebApp/assets/81886509/d50e3c87-6013-4e4a-ba9c-4e94ec229905)<p>
The **CV** page can be viewed when a user clicks on the `CV` tab at the top:<p>
![image](https://github.com/JonesKwameOsei/myCV_WebApp/assets/81886509/0cedbdd5-c2df-42a3-80f8-ff4047b8640c)<p>

It will be good to push this image to my docker hub repository so that we can compare this image to the one built with automation - GitHub actions pipeline. <p>
I will log into my Docker Hub account from the terminal.
```
docker login
```
Then push the image to Docker Hub:<p>
```
docker push kwameds/mycvwebapp:1.0.0
```
![image](https://github.com/JonesKwameOsei/myCV_WebApp/assets/81886509/4fd4e6f8-69b0-4601-9035-c3666c6c0c7f)<p>
Imaged has been pushed successfully.<p>
![image](https://github.com/JonesKwameOsei/myCV_WebApp/assets/81886509/72e672ca-5841-4736-8927-11445b3d9702)<p>
Let us get a confirmation from Docker Hub. <p>
![image](https://github.com/JonesKwameOsei/myCV_WebApp/assets/81886509/39e8d72b-31a3-4f31-8909-e00a6764dea9)<p>
![image](https://github.com/JonesKwameOsei/myCV_WebApp/assets/81886509/8b55a231-7903-4357-bb6b-32dc18c0206c)<p>
![image](https://github.com/JonesKwameOsei/myCV_WebApp/assets/81886509/9b8f606a-c9ad-42dc-9d5c-7775dcc1b8a5)<p>


### 7. Run the GitHub Actions Workflow

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

The pipeline actions has been executed:<p>
![workflow1](https://github.com/JonesKwameOsei/myCV_WebApp/assets/81886509/17403ab6-559a-44f7-9c19-3cb3b811fa2e)<p>
![workflow2](https://github.com/JonesKwameOsei/myCV_WebApp/assets/81886509/34de5e66-5437-496c-a152-8d43a3a8f7ac)<p>
![workflow3](https://github.com/JonesKwameOsei/myCV_WebApp/assets/81886509/c6e5832e-7bd7-4f28-8f9c-68e69f7d0839)<p>
![workflow4](https://github.com/JonesKwameOsei/myCV_WebApp/assets/81886509/e619c1ed-babf-406e-ba62-6361563817ad)<p>

GitHub action completed. We will confirm if the the image is in the `Docker Hub` registry. 
![image](https://github.com/JonesKwameOsei/myCV_WebApp/assets/81886509/0e101d3d-c3e3-4929-81b2-146142fb0108)<p>
Image in docker hub.<p>
![image](https://github.com/JonesKwameOsei/myCV_WebApp/assets/81886509/24ab17e0-045b-43de-a8a6-e85a8f123690)<p>
![image](https://github.com/JonesKwameOsei/myCV_WebApp/assets/81886509/9cac5376-ae6d-4454-9a9e-78a9b6f2689d)<p>

### Test the New Image
Having automatically build and pushed the image to Docker Hub, it is important to run the application to verify if it is working. Run:
```
docker run -d -p 8081:8080 --name newCVapp kwameds/mycv_webapp:2.0.0
```
Docker pulled the image from my repo in the Docker Hub registry as it couldn't find the image locally. Docker goes ahead to run a container based on that image. The `-d` option runs the container in detached mode, `-p 8081:8080` maps the `host's port 8081` to the `container's port 8080`, and `--name newCVapp` assigns the name **newCVapp** to the container.<p>
![image](https://github.com/JonesKwameOsei/myCV_WebApp/assets/81886509/6c4c691c-ba28-4537-8762-a3a93288a4f9)<p>
Let us confirm if the image is now in our local registry by running:
```
docker images        # lists all images
docker ps            # lists containers running
```
![image](https://github.com/JonesKwameOsei/myCV_WebApp/assets/81886509/8167e1df-968e-4061-ab5d-28df771662ae)<p>
Next, We will view the web app in the browser by typing: `http://localhost:8081`. <p>
The web page is accessible: <p>
![image](https://github.com/JonesKwameOsei/myCV_WebApp/assets/81886509/47d9669b-6966-44b3-a3ce-d10e15f1267a)<p>
![image](https://github.com/JonesKwameOsei/myCV_WebApp/assets/81886509/b12bf5b8-014e-4427-8c97-5cd0fb8f11a4)<p>
![image](https://github.com/JonesKwameOsei/myCV_WebApp/assets/81886509/8c838419-cf0d-4efe-ad53-94175172cb28)<p>
![image](https://github.com/JonesKwameOsei/myCV_WebApp/assets/81886509/77142a96-8f4f-4f29-9399-f59889ffe369)<p>

### Modify the codebase and Apply Continous Integration to Build and Push Updates
The web app has been tested and it is working as expected. However, there there are some updates that needs to be done. In the privacy page, it can be observed that the point no.6 states the website may have external links. This needs to be updated because there are no external links. <p>
![image](https://github.com/JonesKwameOsei/myCV_WebApp/assets/81886509/59bae05c-d927-467b-b6d3-a8ceaa73bded)


## Conclusion
In this project, I have demonstrated how to utilised continuous integration in the software development circle. I also leveraged on my programming abilities to develop my web application with `Microsoft .NET SDK` written in `C#`. This was done with `Microsoft Visual Studio`. I have seamlessly integrated Docker into a development pipeline. This approach allow **DevOps Enginees** to automatically build and push Docker images to a registry, ensuring that the deployments are consistent and up-to-date with the latest changes to the codebase. This setup provides a reliable and efficient way to manage the Docker-based applications.
