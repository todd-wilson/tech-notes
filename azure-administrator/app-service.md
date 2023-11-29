# Azure App Service App
Can be create with:
* Azure Portal
* Azure CLI
* A script like Powershell or Python
* An IDE (Integrated Development Environment) like Visual Studio

# Azure App Service
* Web-hosting platform for applications.
* It is platform as a service (PaaS) so the focus is on building the app and not maintaining the infrastructure and worrying about scalling up and down as your needs change. Azure takes care of all of this.

## Deployment Slots
* Live applications
* Each has their own hostname.
* Typical use case might be to have a staging slot to do your testing on and when you like what you seeing swapping this with the app running in the production slot.

## Continuous Integration Continuous Deployment (CICD)
* CICD realized in App Service Deployment Center via DevOps, GitHub, Bitbucket, FTP or a local GIT repository.
* App Service will automatically sync your code after you connect.
* Azure DevOps allows you to define a build and release process every time you commit code.
* Integration also exists between Visual Studio via its Web Deploy Technology.
* Use FTP to support older workflows.

## Autoscaling is Built In
* Allows you to scale your app to support changing workloads.
* You can increase or decrease the resource for the underlying machine which is hosting your web app.
* Scale up increases CPU cores and RAM for processing (latency).
* Scale out by adding new instances (throughput).

## Create a Web App
* When you create an app Azure allocates hosting resources in App Service.
* Apps can be
  * ASP.NET Core
  * Node.js
  * Java
  * Python
  * and more!

### Required Fields
* Subscription
  * You Azure subscription
* Resource Group
  * Logical container for resources
* App name
  * A unique name for your app. This name will be part of the apps URL.
* Publish
  * Deploy to app service as code or Docker image.
    * Retrieve your docker image from the Docker registry on the Docker tab.
* Runtime stack
  * Your programming language your app runs on. If you have a Docker image that image will have your runtime and you don't need to choose a stack.
* OS
  * Depending on your runtime stack, you will have a choice of either or both of the following:
    * Windows
      * Monitoring tab gets enabled and you can use Application Insights.
    * Linux
      * Application Insights is also available on Linux, but it requires some setup.
  * If you are using Docker, choose the OS on which you image will run.
* Region
  * The Azure region where you app's server will run.
* App Service Plan
  * A set of virtual server resources that run App Service apps.
  * The sku or pricing tier determines the resources allocated.
  * One to many relationship. The same app service plan can host multiple apps.
    * The number of web apps you deploy has no effect on you bill.
  * If you use the Azure Portal to create a web app the app service plan can also be created at the same time.

## App Service Plan
An App Service Plan are the virtual resources that run your App Service Apps.
<br/>Each plan has their own prices depending on the resources you need to allocate. This is called the plan's size, sku or pricing tier.
<br/>**The relationship for App Server Apps to App Service Plans is one to one and it is not optional. Each App Server App must have one App Service Plan assigned to it.**

### How is it charged?
* You pay for the resources you use. As the App Service Plan size increases so does the cost.
* You can use one App Service Plan to run multiple Web apps.
* A Web App **must** be assigned to one App Service Plan.

When you create a Web App from The Azure Portal you can assign it to an existing App Service Plan or create a new one.

# Web Application Setup (Local)

1. Install a web application framework.

  Here we will use flask.
  ```
  pip install flask
  ```

1. Create a small web app. This is a server which responds with a message.

  ```
  from flask import Flask
  app = Flask(__name__)
  message = "Web Apps are Cool!\n"

  @app.route("/")
  def hello():
      return message
  ```
1. Add to GIT source control. Need to

  ```
  git init
  git add .
  git commit -m "This is the first commit."
  ```

This will create a GIT source control repository locally. You can use GitHub, DevOps or another remote source control repo to set up CI/CD. You don't need a remote source control repo for this small app, but for production it is *highly* recommended as a best practice.

# Web Application Setup (Azure Cloud Shell)

blinker==1.7.0
<br>click==8.1.7
<br>Flask==3.0.0
<br>importlib-metadata==6.8.0
<br>itsdangerous==2.1.2
<br>Jinja2==3.1.2
<br>MarkupSafe==2.1.3
<br>Werkzeug==3.0.1
<br>zipp==3.17.0

1. Open Azure Cloud Shell. Make sure you have **PowerShell** selected for you editor on the top left.

1. Set up your environment.

  ```
  python3 -m venv venv
  source venv/bin/activate
  pip install flask
  ```
1. Create and new directory and switch to that directory.

  ```
  mkdir ~/HelloApp
  cd ~/HelloApp
  ```

1. Create a file for you app.
  
  ```
  code my_hello_app.py
  ```

1. Create your app.

  ```
  from flask import Flask
  app = Flask(__name__)

  @app.route("/")
  def hello():
    return "<html><body><h1>Hello World!</h1></body></html>\n"
  ```

1. Save your file.
  * Menu
    * Right-click inside the editor and select Save. Right-click again and select Quit.
  * Quick Keys
    * CTRL+S then CTRL+Q (Save and Quit)

1. Deploy

  ```
  pip freeze > my_requirements.txt
  ```

## Test your Web App

1. Open a new browser tab and go to:
  https://shell.azure.com

1. From your original shell (not this new one) run the following:

  ```
  cd ..
  source venv/bin/activate
  ```

1. Stay in the original shell and run the following:

  ```
  cd ~/HelloApp
  export FLASK_APP=my_hello_app.py
  flask run
  ```

1. Switch and go to yous secondary shell and run the following to connect to your application:

  ```
  curl https://127.0.0.1:5000/
  ```

1. You should see the following output:

<html><body><h1>Hello World!</h1></body></html>

## Deploy application on App Service

### Automated Deployment
  * Deployment Options
    * Azure DevOps
      * Build, Test and Release from the Cloud.
    * GitHub
      * Connect your Github repo to Azure. Changes which are committed to your GitHub prod branch are auto-deployed.
    * Bitbucket
      * Similar to Github in that changes committed to Bitbucket are automatically deployed for you.
    * OneDrive
      * Microsoft's storage in the cloud. OneDrive must be setup with your Microsoft account.
    * Dropbox
      * Similar to OneDrive and supported by Azure.

### Manual Deployment
* Git
  * App Service apps have a GIT Url you can use to deploy your app.
* az webapp up
  * webapp up is used with the Azure CLI to package your app and deploy it.
  * Use az webapp up to create a new web app if you don't have one already.
* ZIP deploy
  * az webapp deployment source config.zip.
    * Sends a zip of your files to App Service
    * Also available using HTTP utilities like curl.
* WAR deploy
  * Deploys Java web applications.
  * Access WAR deploy using the KUDU API here:
  https://<your-app-name>.scm.azurewebsites.net/api/wardeploy
* Visual Studio
  * Visual Studio has an app deployment wizard to help with deploying your app on App Service.
* FTP/S
  * FTP and FTPS (secure FTP) is the older way to push your code to App Service.

## Deploy to App Service

### az webapp up

Use this command to deploy your python package on yoru Azure App Service.

1. Set variables.
  * App Name
  * App Resource Group
  * App Plan
  * App Sku
  * App Location

  ```
  export APPNAME=$(az webapp list --query [0].name --output tsv)
export APPRG=$(az webapp list --query [0].resourceGroup --output tsv)
  export APPPLAN=$(az appservice plan list --query [0].name --output tsv)
export APPSKU=$(az appservice plan list --query [0].sku.name --output tsv)
  export APPLOCATION=$(az appservice plan list --query [0].location --output tsv)
  ```

1. Run az webapp up

  ```
  cd ~/HelloApp
  az webapp up --name $APPNAME --resource-group $APPRG --plan $APPPLAN --sku $APPSKU --location "$APPLOCATION"
  ```

1. Test

Look for the URL (should be right before the JSON code). Use this to open your app in a new browser tab.

You should see this in your browser:

<html><body><h1>Hello World!</h1></body></html>

## Clean up application on App Service

1.
