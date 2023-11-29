# Build a Containerized web application using Docker

## Prerequisites
* Web App Dev familiarity
* A Docker Subscription
* Docker on your Desktop
* GIT on your Desktop

## Benefits of Containerization
* No hardware configuration, OS intallation or special software for your deployment.
  * This saves time and money!
* Multiple applications can run in their containers on the same hardware.
* Scaling out is as simple as starting more instances of your container.
* Container images can be extended over time to include more functionality.
* Containerized App are are usually much smaller than an virtual machine because the VM needs to supply the entire OS and supporting runtimes.
  * A Docker container uses the host computer to supply resources to the container. As a result container images are fast and space-saving as opposed to a virtual machine.

## Docker Overview
1. Build an image with the files and any configuration informatio your application might need.
1. Start a container in Docker based on the image you created.

Docker will provide OS resources and is responsible for security. It will make sure your containers are running at the same time, and remain mostly isolated from each other by preventing one container from accessing another. A virtual machine can isolate at the hardware level. Docker containers can't do this because they share underlying OS resources.

## Azure Container Registry and Instance
* Docker images can be uploaded to the Azure Container Registry and then run in an Azure Container Instance.

## Linux and Windows Docker Images
* Images are either Windows or Linux-based.
* To offer functionality on both Windows and Linux you will need to maintain separate images.
* You can use an environment such as ASP.NET Core which will provide the same functionality on both Windows and Linux.
* If you have a Linux host then you can only run Linux containers. If you have a Windows host you can run both Windows and Linux.

## Docker Hub and Registries
* Docker images are stored in registries which is a web service which serves container images.
* A registry is a web service which consists of one or more repositories.
  * A repository will have multiple images of containers which are grouped by name and functionality.
    * The repository is the unit of privacy for the image. You can have private repositories if you don't want to share images.
  * Images will have different versions which a tag is used to identify. This allows a developer to maintain multiple versions of their image.
  * To download an image you need to specify the following:
    * registry
    * repository
    * version tag
      * Version tags are simple text and you can use your own versioning system (v1, v2 or 1.1, 1.2 etc.)

      ```
      mcr.microsoft.com/dotnet/core/aspnet:2.1
      mcr.microsoft.com/dotnet/core/aspnet:2.2
      ```
      * Registry is mcr.microsoft.com
      * Repository is dotnet/core/aspnet
      * The version tag is 2.1 or 2.2

      ```
      mcr.microsoft.com/dotnet/samples:dotnetapp
      mcr.microsoft.com/dotnet/samples:aspnetapp
      ```
      * Registry is mcr.microsoft.com
      * Repository is dotnet/samples
      * The version tag is dotnetapp or aspnetapp.

      * **A single image can have multiple tags assigned to it.**

* Docker Hub is a public registry.
* Since Docker runs on a desktop, server or in the cloud, container images can be downloaded from Docker Hub (a public registry) and run on Docker. You can also upload and host your images there at no cost.

## Get an Image from Docker Hub
* Useful commands
  * docker pull

      ```
      docker pull <repository-path>:<tags>
      ```

      Fetches an image from the registry. If you leave off the tag the Docker will pull the image with the "latest" tag.

  * docker image list

      ```
      docker image list
      ```
      Lists images in the local registry.

  * docker run

      ```
      docker run mcr.microsoft.com/dotnet/samples:aspnetapp
      ```

### Networking on a Container

The default is to not allow inbound requests to reach your container. You may be running a web app on port 80, but unless you specify a port when running a container that port will not be visible to the outside world.

```
docker run -p 8080:80 mcr.microsoft.com/dotnet/samples:aspnetapp
```

The -p switch maps a port from your container to a port on your computer. -p 8080:80 maps port 80 on the guest container to port 8080 on your computer.

Now, if you go to localhost:8080 on your computer you will see the asp.net sample app!

### Files in a Running Container
* Any changes you make to files in your container are lost when the container is stopped unless you take care to preseve the state of the container.
* Containers do not share files. Each container has its own copy of the files in the image.
* Containers can't read data from other containers.
* Writable volumes are allowed and can be mounted by a container and made available to your apps running in the container. This volume will persist when the container stops and allow you to presever state. Likewise, multiple containers can share the same writable volume.

**Best practice is to not make changes to the filesystem of the image deployed by docker. Use this as ephemeral storage knowing that your files will be lost when the container stops.**

## Container Management
* Useful commands
  * View active containers
      ```
      docker ps
      ```
      This will show the status of the container.

      * Container statuses
        * Up (running)
        * Exited (terminated)
        * Other information such as command-line flags when the image was started.

      * Use the -a flag to include non-active containers.

The output will include a unique container name such as fearful_newton. Use this to refer to your container.
  
  * Stop an active container

      ```
      docker stop <container-name>
      ```

Docker lets you run multiple containers from the same image. Each container is assigned a unique ID and a unique human-readable name. When referring to a specific container you will need to use this unique id to reference it.

  * Stop an active container by name
      ```
      docker stop fearful_newton
      ```

  * Remove a container
      ```
      docker rm fearful_newton
      ```

  * You cannot remove a running container.
    * To stop and remove a running container, you will need to use the -f switch.
        ```
        docker rm -f fearful_newton
        ```
        This stops the container and then removes it.

  * Remove an image
      ```
      docker image rm mcr.microsoft.com/dotnet/core/samples:aspnetapp
      ```
      **Containers running images must be terminated before the image can be removed.**

## Sample App


```
docker pull mcr.microsoft.com/dotnet/samples:aspnetapp
docker image ls
docker run -d -p 5555:80 mcr.microsoft.com/dotnet/samples:aspnetapp
```

Got to http://localhost:5555

Stop and Remove Container
```
docker stop <container-name>
docker rm <container-name>
```
* Container can be started again with `docker start <container-name>`.

Remove the Image

```
docker image rm mcr.microsoft.com/dotnet/samples:aspnetapp
```
If you get an error, don't forget to stop and remove the container.

## Custom Sample App
* Docker Hub allows you to download images to get your started on building your own application. To do this you simply download an existing image and add any functionality you requires.

1. Get your base image.
1. Make your modifications.
1. Run `docker commit` to save your changes to a new image.

There is an easier way to do this with Dockerfiles!

A Dockerfile is a text document that contains all the commands to build your image.

### Dockerfile Example

When creating a Dockerfile for your app, place it at the root of your source code. No need to get fancy with the name, just name it Dockerfile.

```
FROM mcr.microsoft.com/dotnet/core/sdk:2.2
WORKDIR /app
COPY myapp_code .
RUN dotnet build -c Release -o /rel
EXPOSE 80
WORKDIR /rel
ENTRYPOINT ["dotnet", "myapp.dll"]
```

Command|Comments
:--|:--|
FROM|This is the image that you are going to download.|
WORKDIR|Sets your current working directory.|
COPY|This will copy files from your computer to the container. The first argument `myapp_code` is the file or folder you want to copy over. <br>The `.` is the location where you want to put your files and folder in the container. <br>Since we set the working directory to `/app` this is where your files and folders will be copied.|
RUN|Runs or executes a command. Think command-line.|
EXPOSE|Specifies which port(s) to open when the container runs|
ENTRYPOINT|What the container will run when it starts. Specify the command and each argument as string array.|

## Create a New Image

Use `docker build` to create a new image by running a Dockerfile.

* Use the -f switch to set the name of the Dockerfile you want to use.
* Use the -t flag to specify the name of the image you want to create.
* The `.` at the end sets the build context for the COPY command. These are the files that are needed during the build process.

Example:
```
docker build -t myapp:v1 .
```

Docker will:
1. Create a container.
1. Run commands in the container from your Dockerfile.
1. Commit the changes to a new image.

#### Example from MS Learn

##### Create a Dockerfile

```
git clone https://github.com/MicrosoftDocs/mslearn-hotel-reservation-system.git
cd mslearn-hotel-reservation-system/src
copy NUL Dockerfile
notepad Dockerfile
```

Add this to the Dockerfile:

```
FROM mcr.microsoft.com/dotnet/core/sdk:2.2
WORKDIR /src
COPY ["/HotelReservationSystem/HotelReservationSystem.csproj", "HotelReservationSystem/"]
COPY ["/HotelReservationSystemTypes/HotelReservationSystemTypes.csproj", "HotelReservationSystemTypes/"]
RUN dotnet restore "HotelReservationSystem/HotelReservationSystem.csproj"
```

1. Fetches an image containing the .NET Core Framework SDK.
1. Files are copied to /src folder in the container.
1. `dotnet restore` downloads dependencies for the project from NuGet.

Append this code to the Dockerfile:

```
COPY . .
WORKDIR "/src/HotelReservationSystem"
RUN dotnet build "HotelReservationSystem.csproj" -c Release -o /app
```

1. Copies the apps source code to the container.
1. Builds the app using the dotnet build command.
1. The build files are written to /app

Append this command to the Dockerfile:

```
RUN dotnet publish "HotelReservationSystem.csproj" -c Release -o /app
```

1. Copies executables to a new folder and cleans up any temp files. These files in the new folder can be deployed.

Append this command to the Dockerfile:

```
EXPOSE 80
WORKDIR /app
ENTRYPOINT ["dotnet", "HotelReservationSystem.dll"]
```

1. Opens port 80 on the container.
1. Change the working directory to the /app directory where the solution was built.
1. Specifies which library should run.

## Build and Deploy
