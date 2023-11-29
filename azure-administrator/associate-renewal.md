{
  "nbformat": 4,
  "nbformat_minor": 0,
  "metadata": {
    "colab": {
      "provenance": [],
      "toc_visible": true,
      "authorship_tag": "ABX9TyMoYA1wI4s6oXFFwFksky8w",
      "include_colab_link": true
    },
    "kernelspec": {
      "name": "python3",
      "display_name": "Python 3"
    },
    "language_info": {
      "name": "python"
    }
  },
  "cells": [
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "view-in-github",
        "colab_type": "text"
      },
      "source": [
        "<a href=\"https://colab.research.google.com/github/todd-wilson/tech-notes/blob/main/azure-administrator/Administrator_Associate_Renewal.ipynb\" target=\"_parent\"><img src=\"https://colab.research.google.com/assets/colab-badge.svg\" alt=\"Open In Colab\"/></a>"
      ]
    },
    {
      "cell_type": "markdown",
      "source": [
        "# Prerequisites\n",
        "* Google Colab\n",
        "  * What is Google Colab?\n",
        "* Markup Language\n",
        "  What is Markup Language?\n",
        "* Install Python\n",
        "  * What is Python?\n",
        "* Install GIT\n",
        "  * What is GIT?\n",
        "    * Benefits?\n",
        "      * More frequent code deployment by automating building, testing and deploying when code is changed and committed.\n",
        "      * More frequent code deployment means you can respond to bug changes and app enhancements more quickly and effectively.\n",
        "* Azure Portal\n",
        "* Azure Cloud Shell\n",
        "  * How to access?\n",
        "    * Top left on the Azure Portal.\n",
        "  <br>![image.png](data:image/png;base64,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)\n"
      ],
      "metadata": {
        "id": "pYIcIU5Xdg2w"
      }
    },
    {
      "cell_type": "markdown",
      "source": [
        "# Why Azure Portal?\n",
        "* Graphical which makes things easier to learn.\n",
        "* Helps you discover available features."
      ],
      "metadata": {
        "id": "VqDjeG5a51Vw"
      }
    },
    {
      "cell_type": "markdown",
      "source": [
        "# Azure App Service App\n",
        "Can be create with:\n",
        "* Azure Portal\n",
        "* Azure CLI\n",
        "* A script like Powershell or Python\n",
        "* An IDE (Integrated Development Environment) like Visual Studio"
      ],
      "metadata": {
        "id": "2od01T9s5GYj"
      }
    },
    {
      "cell_type": "markdown",
      "source": [
        "# Azure App Service\n",
        "* Web-hosting platform for applications.\n",
        "* It is platform as a service (PaaS) so the focus is on building the app and not maintaining the infrastructure and worrying about scalling up and down as your needs change. Azure takes care of all of this."
      ],
      "metadata": {
        "id": "iaDT_N8m6Kvy"
      }
    },
    {
      "cell_type": "markdown",
      "source": [
        "## Deployment Slots\n",
        "* Live applications\n",
        "* Each has their own hostname.\n",
        "* Typical use case might be to have a staging slot to do your testing on and when you like what you seeing swapping this with the app running in the production slot.\n",
        "\n"
      ],
      "metadata": {
        "id": "_3nv0xUo6Mzy"
      }
    },
    {
      "cell_type": "markdown",
      "source": [
        "## Continuous Integration Continuous Deployment (CICD)\n",
        "* CICD realized in App Service Deployment Center via DevOps, GitHub, Bitbucket, FTP or a local GIT repository.\n",
        "* App Service will automatically sync your code after you connect.\n",
        "* Azure DevOps allows you to define a build and release process every time you commit code.\n",
        "* Integration also exists between Visual Studio via its Web Deploy Technology.\n",
        "* Use FTP to support older workflows."
      ],
      "metadata": {
        "id": "uEx7rhvv6Mxg"
      }
    },
    {
      "cell_type": "markdown",
      "source": [
        "## Autoscaling is Built In\n",
        "* Allows you to scale your app to support changing workloads.\n",
        "* You can increase or decrease the resource for the underlying machine which is hosting your web app.\n",
        "* Scale up increases CPU cores and RAM for processing (latency).\n",
        "* Scale out by adding new instances (throughput)."
      ],
      "metadata": {
        "id": "2A3fIYzC6Muz"
      }
    },
    {
      "cell_type": "markdown",
      "source": [
        "## Create a Web App\n",
        "* When you create an app Azure allocates hosting resources in App Service.\n",
        "* Apps can be\n",
        "  * ASP.NET Core\n",
        "  * Node.js\n",
        "  * Java\n",
        "  * Python\n",
        "  * and more!"
      ],
      "metadata": {
        "id": "OToGibqf6MsJ"
      }
    },
    {
      "cell_type": "markdown",
      "source": [
        "### Required Fields\n",
        "* Subscription\n",
        "  * You Azure subscription\n",
        "* Resource Group\n",
        "  * Logical container for resources\n",
        "* App name\n",
        "  * A unique name for your app. This name will be part of the apps URL.\n",
        "* Publish\n",
        "  * Deploy to app service as code or Docker image.\n",
        "    * Retrieve your docker image from the Docker registry on the Docker tab.\n",
        "* Runtime stack\n",
        "  * Your programming language your app runs on. If you have a Docker image that image will have your runtime and you don't need to choose a stack.\n",
        "* OS\n",
        "  * Depending on your runtime stack, you will have a choice of either or both of the following:\n",
        "    * Windows\n",
        "      * Monitoring tab gets enabled and you can use Application Insights.\n",
        "    * Linux\n",
        "      * Application Insights is also available on Linux, but it requires some setup.\n",
        "  * If you are using Docker, choose the OS on which you image will run.\n",
        "* Region\n",
        "  * The Azure region where you app's server will run.\n",
        "* App Service Plan\n",
        "  * A set of virtual server resources that run App Service apps.\n",
        "  * The sku or pricing tier determines the resources allocated.\n",
        "  * One to many relationship. The same app service plan can host multiple apps.\n",
        "    * The number of web apps you deploy has no effect on you bill.\n",
        "  * If you use the Azure Portal to create a web app the app service plan can also be created at the same time."
      ],
      "metadata": {
        "id": "ruB1qGez6Mmx"
      }
    },
    {
      "cell_type": "markdown",
      "source": [
        "## App Service Plan\n",
        "An App Service Plan are the virtual resources that run your App Service Apps.\n",
        "<br/>Each plan has their own prices depending on the resources you need to allocate. This is called the plan's size, sku or pricing tier.\n",
        "<br/>**The relationship for App Server Apps to App Service Plans is one to one and it is not optional. Each App Server App must have one App Service Plan assigned to it.**\n"
      ],
      "metadata": {
        "id": "UA4nDrQz6MkE"
      }
    },
    {
      "cell_type": "markdown",
      "source": [
        "### How is it charged?\n",
        "* You pay for the resources you use. As the App Service Plan size increases so does the cost.\n",
        "* You can use one App Service Plan to run multiple Web apps.\n",
        "* A Web App **must** be assigned to one App Service Plan.\n",
        "\n",
        "When you create a Web App from The Azure Portal you can assign it to an existing App Service Plan or create a new one."
      ],
      "metadata": {
        "id": "e_d1bM7W8DeS"
      }
    },
    {
      "cell_type": "markdown",
      "source": [
        "# Web Application Setup (Local)\n",
        "\n",
        "1. Install a web application framework.\n",
        "\n",
        "  Here we will use flask.\n",
        "  ```\n",
        "  pip install flask\n",
        "  ```\n",
        "\n",
        "1. Create a small web app. This is a server which responds with a message.\n",
        "\n",
        "  ```\n",
        "  from flask import Flask\n",
        "  app = Flask(__name__)\n",
        "  message = \"Web Apps are Cool!\\n\"\n",
        "\n",
        "  @app.route(\"/\")\n",
        "  def hello():\n",
        "      return message\n",
        "  ```\n",
        "1. Add to GIT source control. Need to\n",
        "\n",
        "  ```\n",
        "  git init\n",
        "  git add .\n",
        "  git commit -m \"This is the first commit.\"\n",
        "  ```\n",
        "\n",
        "This will create a GIT source control repository locally. You can use GitHub, DevOps or another remote source control repo to set up CI/CD. You don't need a remote source control repo for this small app, but for production it is *highly* recommended as a best practice.\n",
        "\n"
      ],
      "metadata": {
        "id": "QP1MoV9ob7Ox"
      }
    },
    {
      "cell_type": "markdown",
      "source": [
        "# Web Application Setup (Azure Cloud Shell)\n",
        "\n",
        "blinker==1.7.0\n",
        "<br>click==8.1.7\n",
        "<br>Flask==3.0.0\n",
        "<br>importlib-metadata==6.8.0\n",
        "<br>itsdangerous==2.1.2\n",
        "<br>Jinja2==3.1.2\n",
        "<br>MarkupSafe==2.1.3\n",
        "<br>Werkzeug==3.0.1\n",
        "<br>zipp==3.17.0\n",
        "\n",
        "1. Open Azure Cloud Shell. Make sure you have **PowerShell** selected for you editor on the top left.\n",
        "\n",
        "1. Set up your environment.\n",
        "\n",
        "  ```\n",
        "  python3 -m venv venv\n",
        "  source venv/bin/activate\n",
        "  pip install flask\n",
        "  ```\n",
        "1. Create and new directory and switch to that directory.\n",
        "\n",
        "  ```\n",
        "  mkdir ~/HelloApp\n",
        "  cd ~/HelloApp\n",
        "  ```\n",
        "\n",
        "1. Create a file for you app.\n",
        "  \n",
        "  ```\n",
        "  code my_hello_app.py\n",
        "  ```\n",
        "\n",
        "1. Create your app.\n",
        "\n",
        "  ```\n",
        "  from flask import Flask\n",
        "  app = Flask(__name__)\n",
        "\n",
        "  @app.route(\"/\")\n",
        "  def hello():\n",
        "    return \"<html><body><h1>Hello World!</h1></body></html>\\n\"\n",
        "  ```\n",
        "\n",
        "1. Save your file.\n",
        "  * Menu\n",
        "    * Right-click inside the editor and select Save. Right-click again and select Quit.\n",
        "  * Quick Keys\n",
        "    * CTRL+S then CTRL+Q (Save and Quit)\n",
        "\n",
        "1. Deploy\n",
        "\n",
        "  ```\n",
        "  pip freeze > my_requirements.txt\n",
        "  ```\n"
      ],
      "metadata": {
        "id": "8JGryG8hg9Vt"
      }
    },
    {
      "cell_type": "markdown",
      "source": [
        "## Test your Web App\n",
        "\n",
        "1. Open a new browser tab and go to:\n",
        "  https://shell.azure.com\n",
        "\n",
        "1. From your original shell (not this new one) run the following:\n",
        "\n",
        "  ```\n",
        "  cd ..\n",
        "  source venv/bin/activate\n",
        "  ```\n",
        "\n",
        "1. Stay in the original shell and run the following:\n",
        "\n",
        "  ```\n",
        "  cd ~/HelloApp\n",
        "  export FLASK_APP=my_hello_app.py\n",
        "  flask run\n",
        "  ```\n",
        "\n",
        "1. Switch and go to yous secondary shell and run the following to connect to your application:\n",
        "\n",
        "  ```\n",
        "  curl https://127.0.0.1:5000/\n",
        "  ```\n",
        "\n",
        "1. You should see the following output:\n",
        "\n",
        "<html><body><h1>Hello World!</h1></body></html>"
      ],
      "metadata": {
        "id": "55AgcAUFnCvF"
      }
    },
    {
      "cell_type": "markdown",
      "source": [
        "## Deploy application on App Service"
      ],
      "metadata": {
        "id": "OuodyL9d6MhH"
      }
    },
    {
      "cell_type": "markdown",
      "source": [
        "### Automated Deployment\n",
        "  * Deployment Options\n",
        "    * Azure DevOps\n",
        "      * Build, Test and Release from the Cloud.\n",
        "    * GitHub\n",
        "      * Connect your Github repo to Azure. Changes which are committed to your GitHub prod branch are auto-deployed.\n",
        "    * Bitbucket\n",
        "      * Similar to Github in that changes committed to Bitbucket are automatically deployed for you.\n",
        "    * OneDrive\n",
        "      * Microsoft's storage in the cloud. OneDrive must be setup with your Microsoft account.\n",
        "    * Dropbox\n",
        "      * Similar to OneDrive and supported by Azure."
      ],
      "metadata": {
        "id": "iu5UdME_6Mej"
      }
    },
    {
      "cell_type": "markdown",
      "source": [
        "### Manual Deployment\n",
        "* Git\n",
        "  * App Service apps have a GIT Url you can use to deploy your app.\n",
        "* az webapp up\n",
        "  * webapp up is used with the Azure CLI to package your app and deploy it.\n",
        "  * Use az webapp up to create a new web app if you don't have one already.\n",
        "* ZIP deploy\n",
        "  * az webapp deployment source config.zip.\n",
        "    * Sends a zip of your files to App Service\n",
        "    * Also available using HTTP utilities like curl.\n",
        "* WAR deploy\n",
        "  * Deploys Java web applications.\n",
        "  * Access WAR deploy using the KUDU API here:\n",
        "  https://<your-app-name>.scm.azurewebsites.net/api/wardeploy\n",
        "* Visual Studio\n",
        "  * Visual Studio has an app deployment wizard to help with deploying your app on App Service.\n",
        "* FTP/S\n",
        "  * FTP and FTPS (secure FTP) is the older way to push your code to App Service."
      ],
      "metadata": {
        "id": "xNi07P-j6Mb6"
      }
    },
    {
      "cell_type": "markdown",
      "source": [
        "## Deploy to App Service"
      ],
      "metadata": {
        "id": "O-KIQrLb6MZE"
      }
    },
    {
      "cell_type": "markdown",
      "source": [
        "### az webapp up\n",
        "\n",
        "Use this command to deploy your python package on yoru Azure App Service.\n",
        "\n",
        "1. Set variables.\n",
        "  * App Name\n",
        "  * App Resource Group\n",
        "  * App Plan\n",
        "  * App Sku\n",
        "  * App Location\n",
        "\n",
        "  ```\n",
        "  export APPNAME=$(az webapp list --query [0].name --output tsv)\n",
        "export APPRG=$(az webapp list --query [0].resourceGroup --output tsv)\n",
        "  export APPPLAN=$(az appservice plan list --query [0].name --output tsv)\n",
        "export APPSKU=$(az appservice plan list --query [0].sku.name --output tsv)\n",
        "  export APPLOCATION=$(az appservice plan list --query [0].location --output tsv)\n",
        "  ```\n",
        "\n",
        "1. Run az webapp up\n",
        "\n",
        "  ```\n",
        "  cd ~/HelloApp\n",
        "  az webapp up --name $APPNAME --resource-group $APPRG --plan $APPPLAN --sku $APPSKU --location \"$APPLOCATION\"\n",
        "  ```\n",
        "\n",
        "1. Test\n",
        "\n",
        "Look for the URL (should be right before the JSON code). Use this to open your app in a new browser tab.\n",
        "\n",
        "You should see this in your browser:\n",
        "\n",
        "<html><body><h1>Hello World!</h1></body></html>"
      ],
      "metadata": {
        "id": "z_42LZOi6MWe"
      }
    },
    {
      "cell_type": "markdown",
      "source": [
        "## Clean up application on App Service\n",
        "\n",
        "1."
      ],
      "metadata": {
        "id": "cBUAPMG46MUE"
      }
    },
    {
      "cell_type": "markdown",
      "source": [
        "# Build a Containerized web application using Docker"
      ],
      "metadata": {
        "id": "5l6uOKxE6MRo"
      }
    },
    {
      "cell_type": "markdown",
      "source": [
        "## Prerequisites\n",
        "* Web App Dev familiarity\n",
        "* A Docker Subscription\n",
        "* Docker on your Desktop\n",
        "* GIT on your Desktop"
      ],
      "metadata": {
        "id": "wVAGhcil6MPY"
      }
    },
    {
      "cell_type": "markdown",
      "source": [
        "## Benefits of Containerization\n",
        "* No hardware configuration, OS intallation or special software for your deployment.\n",
        "  * This saves time and money!\n",
        "* Multiple applications can run in their containers on the same hardware.\n",
        "* Scaling out is as simple as starting more instances of your container.\n",
        "* Container images can be extended over time to include more functionality.\n",
        "* Containerized App are are usually much smaller than an virtual machine because the VM needs to supply the entire OS and supporting runtimes.\n",
        "  * A Docker container uses the host computer to supply resources to the container. As a result container images are fast and space-saving as opposed to a virtual machine."
      ],
      "metadata": {
        "id": "PZuzHCTm6MMv"
      }
    },
    {
      "cell_type": "markdown",
      "source": [
        "## Docker Overview\n",
        "1. Build an image with the files and any configuration informatio your application might need.\n",
        "1. Start a container in Docker based on the image you created.\n",
        "\n",
        "Docker will provide OS resources and is responsible for security. It will make sure your containers are running at the same time, and remain mostly isolated from each other by preventing one container from accessing another. A virtual machine can isolate at the hardware level. Docker containers can't do this because they share underlying OS resources."
      ],
      "metadata": {
        "id": "0k3aI1Vx6MKg"
      }
    },
    {
      "cell_type": "markdown",
      "source": [
        "## Azure Container Registry and Instance\n",
        "* Docker images can be uploaded to the Azure Container Registry and then run in an Azure Container Instance."
      ],
      "metadata": {
        "id": "0y0ud7ob6MIJ"
      }
    },
    {
      "cell_type": "markdown",
      "source": [
        "## Linux and Windows Docker Images\n",
        "* Images are either Windows or Linux-based.\n",
        "* To offer functionality on both Windows and Linux you will need to maintain separate images.\n",
        "* You can use an environment such as ASP.NET Core which will provide the same functionality on both Windows and Linux.\n",
        "* If you have a Linux host then you can only run Linux containers. If you have a Windows host you can run both Windows and Linux."
      ],
      "metadata": {
        "id": "0ASVUxdX6MFx"
      }
    },
    {
      "cell_type": "markdown",
      "source": [
        "## Docker Hub and Registries\n",
        "* Docker images are stored in registries which is a web service which serves container images.\n",
        "* A registry is a web service which consists of one or more repositories.\n",
        "  * A repository will have multiple images of containers which are grouped by name and functionality.\n",
        "    * The repository is the unit of privacy for the image. You can have private repositories if you don't want to share images.\n",
        "  * Images will have different versions which a tag is used to identify. This allows a developer to maintain multiple versions of their image.\n",
        "  * To download an image you need to specify the following:\n",
        "    * registry\n",
        "    * repository\n",
        "    * version tag\n",
        "      * Version tags are simple text and you can use your own versioning system (v1, v2 or 1.1, 1.2 etc.)\n",
        "\n",
        "      ```\n",
        "      mcr.microsoft.com/dotnet/core/aspnet:2.1\n",
        "      mcr.microsoft.com/dotnet/core/aspnet:2.2\n",
        "      ```\n",
        "      * Registry is mcr.microsoft.com\n",
        "      * Repository is dotnet/core/aspnet\n",
        "      * The version tag is 2.1 or 2.2\n",
        "\n",
        "      ```\n",
        "      mcr.microsoft.com/dotnet/samples:dotnetapp\n",
        "      mcr.microsoft.com/dotnet/samples:aspnetapp\n",
        "      ```\n",
        "      * Registry is mcr.microsoft.com\n",
        "      * Repository is dotnet/samples\n",
        "      * The version tag is dotnetapp or aspnetapp.\n",
        "\n",
        "      * **A single image can have multiple tags assigned to it.**\n",
        "\n",
        "* Docker Hub is a public registry.\n",
        "* Since Docker runs on a desktop, server or in the cloud, container images can be downloaded from Docker Hub (a public registry) and run on Docker. You can also upload and host your images there at no cost."
      ],
      "metadata": {
        "id": "C5aEu7bz6MDf"
      }
    },
    {
      "cell_type": "markdown",
      "source": [
        "## Get an Image from Docker Hub\n",
        "* Useful commands\n",
        "  * docker pull\n",
        "\n",
        "      ```\n",
        "      docker pull <repository-path>:<tags>\n",
        "      ```\n",
        "\n",
        "      Fetches an image from the registry. If you leave off the tag the Docker will pull the image with the \"latest\" tag.\n",
        "\n",
        "  * docker image list\n",
        "\n",
        "      ```\n",
        "      docker image list\n",
        "      ```\n",
        "      Lists images in the local registry.\n",
        "\n",
        "  * docker run\n",
        "\n",
        "      ```\n",
        "      docker run mcr.microsoft.com/dotnet/samples:aspnetapp\n",
        "      ```\n",
        "\n"
      ],
      "metadata": {
        "id": "s27mwSnA6MBD"
      }
    },
    {
      "cell_type": "markdown",
      "source": [
        "### Networking on a Container\n",
        "\n",
        "The default is to not allow inbound requests to reach your container. You may be running a web app on port 80, but unless you specify a port when running a container that port will not be visible to the outside world.\n",
        "\n",
        "```\n",
        "docker run -p 8080:80 mcr.microsoft.com/dotnet/samples:aspnetapp\n",
        "```\n",
        "\n",
        "The -p switch maps a port from your container to a port on your computer. -p 8080:80 maps port 80 on the guest container to port 8080 on your computer.\n",
        "\n",
        "Now, if you go to localhost:8080 on your computer you will see the asp.net sample app!"
      ],
      "metadata": {
        "id": "CiIQ8GNZ6L-0"
      }
    },
    {
      "cell_type": "markdown",
      "source": [
        "### Files in a Running Container\n",
        "* Any changes you make to files in your container are lost when the container is stopped unless you take care to preseve the state of the container.\n",
        "* Containers do not share files. Each container has its own copy of the files in the image.\n",
        "* Containers can't read data from other containers.\n",
        "* Writable volumes are allowed and can be mounted by a container and made available to your apps running in the container. This volume will persist when the container stops and allow you to presever state. Likewise, multiple containers can share the same writable volume.\n",
        "\n",
        "**Best practice is to not make changes to the filesystem of the image deployed by docker. Use this as ephemeral storage knowing that your files will be lost when the container stops.**"
      ],
      "metadata": {
        "id": "TVocoohD6L1a"
      }
    },
    {
      "cell_type": "markdown",
      "source": [
        "## Container Management\n",
        "* Useful commands\n",
        "  * View active containers\n",
        "      ```\n",
        "      docker ps\n",
        "      ```\n",
        "      This will show the status of the container.\n",
        "\n",
        "      * Container statuses\n",
        "        * Up (running)\n",
        "        * Exited (terminated)\n",
        "        * Other information such as command-line flags when the image was started.\n",
        "\n",
        "      * Use the -a flag to include non-active containers.\n",
        "\n",
        "The output will include a unique container name such as fearful_newton. Use this to refer to your container.\n",
        "  \n",
        "  * Stop an active container\n",
        "\n",
        "      ```\n",
        "      docker stop <container-name>\n",
        "      ```\n",
        "\n",
        "Docker lets you run multiple containers from the same image. Each container is assigned a unique ID and a unique human-readable name. When referring to a specific container you will need to use this unique id to reference it.\n",
        "\n",
        "  * Stop an active container by name\n",
        "      ```\n",
        "      docker stop fearful_newton\n",
        "      ```\n",
        "\n",
        "  * Remove a container\n",
        "      ```\n",
        "      docker rm fearful_newton\n",
        "      ```\n",
        "\n",
        "  * You cannot remove a running container.\n",
        "    * To stop and remove a running container, you will need to use the -f switch.\n",
        "        ```\n",
        "        docker rm -f fearful_newton\n",
        "        ```\n",
        "        This stops the container and then removes it.\n",
        "\n",
        "  * Remove an image\n",
        "      ```\n",
        "      docker image rm mcr.microsoft.com/dotnet/core/samples:aspnetapp\n",
        "      ```\n",
        "      **Containers running images must be terminated before the image can be removed.**\n"
      ],
      "metadata": {
        "id": "JuTwSA7C6LrQ"
      }
    },
    {
      "cell_type": "markdown",
      "source": [
        "## Sample App\n",
        "\n",
        "\n",
        "```\n",
        "docker pull mcr.microsoft.com/dotnet/samples:aspnetapp\n",
        "docker image ls\n",
        "docker run -d -p 5555:80 mcr.microsoft.com/dotnet/samples:aspnetapp\n",
        "```\n",
        "\n",
        "Got to http://localhost:5555\n",
        "\n",
        "Stop and Remove Container\n",
        "```\n",
        "docker stop <container-name>\n",
        "docker rm <container-name>\n",
        "```\n",
        "* Container can be started again with `docker start <container-name>`.\n",
        "\n",
        "Remove the Image\n",
        "\n",
        "```\n",
        "docker image rm mcr.microsoft.com/dotnet/samples:aspnetapp\n",
        "```\n",
        "If you get an error, don't forget to stop and remove the container.\n",
        "\n"
      ],
      "metadata": {
        "id": "OHLaw5aA6LQq"
      }
    },
    {
      "cell_type": "markdown",
      "source": [
        "## Custom Sample App\n",
        "* Docker Hub allows you to download images to get your started on building your own application. To do this you simply download an existing image and add any functionality you requires.\n",
        "\n",
        "1. Get your base image.\n",
        "1. Make your modifications.\n",
        "1. Run `docker commit` to save your changes to a new image.\n",
        "\n",
        "There is an easier way to do this with Dockerfiles!\n",
        "\n",
        "A Dockerfile is a text document that contains all the commands to build your image.\n",
        "\n",
        "\n"
      ],
      "metadata": {
        "id": "lGVadI8yoSqJ"
      }
    },
    {
      "cell_type": "markdown",
      "source": [
        "### Dockerfile Example\n",
        "\n",
        "When creating a Dockerfile for your app, place it at the root of your source code. No need to get fancy with the name, just name it Dockerfile.\n",
        "\n",
        "```\n",
        "FROM mcr.microsoft.com/dotnet/core/sdk:2.2\n",
        "WORKDIR /app\n",
        "COPY myapp_code .\n",
        "RUN dotnet build -c Release -o /rel\n",
        "EXPOSE 80\n",
        "WORKDIR /rel\n",
        "ENTRYPOINT [\"dotnet\", \"myapp.dll\"]\n",
        "```\n",
        "\n",
        "Command|Comments\n",
        ":--|:--|\n",
        "FROM|This is the image that you are going to download.|\n",
        "WORKDIR|Sets your current working directory.|\n",
        "COPY|This will copy files from your computer to the container. The first argument `myapp_code` is the file or folder you want to copy over. <br>The `.` is the location where you want to put your files and folder in the container. <br>Since we set the working directory to `/app` this is where your files and folders will be copied.|\n",
        "RUN|Runs or executes a command. Think command-line.|\n",
        "EXPOSE|Specifies which port(s) to open when the container runs|\n",
        "ENTRYPOINT|What the container will run when it starts. Specify the command and each argument as string array.|\n",
        "\n"
      ],
      "metadata": {
        "id": "zpU3U3ZnoSnR"
      }
    },
    {
      "cell_type": "markdown",
      "source": [
        "## Create a New Image\n",
        "\n",
        "Use `docker build` to create a new image by running a Dockerfile.\n",
        "\n",
        "* Use the -f switch to set the name of the Dockerfile you want to use.\n",
        "* Use the -t flag to specify the name of the image you want to create.\n",
        "* The `.` at the end sets the build context for the COPY command. These are the files that are needed during the build process.\n",
        "\n",
        "Example:\n",
        "```\n",
        "docker build -t myapp:v1 .\n",
        "```\n",
        "\n",
        "Docker will:\n",
        "1. Create a container.\n",
        "1. Run commands in the container from your Dockerfile.\n",
        "1. Commit the changes to a new image.\n",
        "\n",
        "\n"
      ],
      "metadata": {
        "id": "XKZYWcmpoSkc"
      }
    },
    {
      "cell_type": "markdown",
      "source": [
        "#### Example from MS Learn"
      ],
      "metadata": {
        "id": "NVjQZhyZoShu"
      }
    },
    {
      "cell_type": "markdown",
      "source": [
        "##### Create a Dockerfile\n",
        "\n",
        "```\n",
        "git clone https://github.com/MicrosoftDocs/mslearn-hotel-reservation-system.git\n",
        "cd mslearn-hotel-reservation-system/src\n",
        "copy NUL Dockerfile\n",
        "notepad Dockerfile\n",
        "```\n",
        "\n",
        "Add this to the Dockerfile:\n",
        "\n",
        "```\n",
        "FROM mcr.microsoft.com/dotnet/core/sdk:2.2\n",
        "WORKDIR /src\n",
        "COPY [\"/HotelReservationSystem/HotelReservationSystem.csproj\", \"HotelReservationSystem/\"]\n",
        "COPY [\"/HotelReservationSystemTypes/HotelReservationSystemTypes.csproj\", \"HotelReservationSystemTypes/\"]\n",
        "RUN dotnet restore \"HotelReservationSystem/HotelReservationSystem.csproj\"\n",
        "```\n",
        "\n",
        "1. Fetches an image containing the .NET Core Framework SDK.\n",
        "1. Files are copied to /src folder in the container.\n",
        "1. `dotnet restore` downloads dependencies for the project from NuGet.\n",
        "\n",
        "Append this code to the Dockerfile:\n",
        "\n",
        "```\n",
        "COPY . .\n",
        "WORKDIR \"/src/HotelReservationSystem\"\n",
        "RUN dotnet build \"HotelReservationSystem.csproj\" -c Release -o /app\n",
        "```\n",
        "\n",
        "1. Copies the apps source code to the container.\n",
        "1. Builds the app using the dotnet build command.\n",
        "1. The build files are written to /app\n",
        "\n",
        "Append this command to the Dockerfile:\n",
        "\n",
        "```\n",
        "RUN dotnet publish \"HotelReservationSystem.csproj\" -c Release -o /app\n",
        "```\n",
        "\n",
        "1. Copies executables to a new folder and cleans up any temp files. These files in the new folder can be deployed.\n",
        "\n",
        "Append this command to the Dockerfile:\n",
        "\n",
        "```\n",
        "EXPOSE 80\n",
        "WORKDIR /app\n",
        "ENTRYPOINT [\"dotnet\", \"HotelReservationSystem.dll\"]\n",
        "```\n",
        "\n",
        "1. Opens port 80 on the container.\n",
        "1. Change the working directory to the /app directory where the solution was built.\n",
        "1. Specifies which library should run."
      ],
      "metadata": {
        "id": "0x8dzqtsoSfD"
      }
    },
    {
      "cell_type": "markdown",
      "source": [
        "## Build and Deploy"
      ],
      "metadata": {
        "id": "oSQKJd_loScR"
      }
    },
    {
      "cell_type": "markdown",
      "source": [],
      "metadata": {
        "id": "I4HuXOheoSZS"
      }
    },
    {
      "cell_type": "markdown",
      "source": [],
      "metadata": {
        "id": "ocoEm7i5oSWh"
      }
    },
    {
      "cell_type": "markdown",
      "source": [],
      "metadata": {
        "id": "qLywMSeyoSUA"
      }
    },
    {
      "cell_type": "markdown",
      "source": [],
      "metadata": {
        "id": "9w12ejrBoSRl"
      }
    },
    {
      "cell_type": "markdown",
      "source": [],
      "metadata": {
        "id": "XqhsRN32oSOv"
      }
    },
    {
      "cell_type": "markdown",
      "source": [],
      "metadata": {
        "id": "DlCKhPPRoSMC"
      }
    },
    {
      "cell_type": "markdown",
      "source": [],
      "metadata": {
        "id": "y52TYUoQoSJZ"
      }
    },
    {
      "cell_type": "markdown",
      "source": [],
      "metadata": {
        "id": "ZMIOeVd4oSGv"
      }
    },
    {
      "cell_type": "markdown",
      "source": [],
      "metadata": {
        "id": "ANJF2gL2oSEH"
      }
    },
    {
      "cell_type": "markdown",
      "source": [],
      "metadata": {
        "id": "zCKaJAdgoSBy"
      }
    },
    {
      "cell_type": "markdown",
      "source": [],
      "metadata": {
        "id": "zPTH6XDIoR_X"
      }
    },
    {
      "cell_type": "markdown",
      "source": [],
      "metadata": {
        "id": "KKkFPnFVoR8j"
      }
    },
    {
      "cell_type": "markdown",
      "source": [],
      "metadata": {
        "id": "bMOA9wuSoR6K"
      }
    },
    {
      "cell_type": "markdown",
      "source": [],
      "metadata": {
        "id": "0XoKvmIaoR3X"
      }
    },
    {
      "cell_type": "markdown",
      "source": [],
      "metadata": {
        "id": "QjzrEJZ6oR0t"
      }
    },
    {
      "cell_type": "markdown",
      "source": [],
      "metadata": {
        "id": "eIUUNr4NoRxw"
      }
    },
    {
      "cell_type": "markdown",
      "source": [],
      "metadata": {
        "id": "nxA86e_GoRuw"
      }
    },
    {
      "cell_type": "markdown",
      "source": [],
      "metadata": {
        "id": "hibDaHPAoRrs"
      }
    },
    {
      "cell_type": "markdown",
      "source": [],
      "metadata": {
        "id": "D_OhMteooRjB"
      }
    }
  ]
}