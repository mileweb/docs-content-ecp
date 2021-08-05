## Deploy a containerized web application
This demo describes how to build and upload a containerized web application, and then run the application at scale across global ECP locations. It also shows how to leverage ECP’s intelligent traffic management feature to manage global traffic for the application.

### Objectives
In this demo, you will learn how to:
- Package a sample web application into a Docker container image.    
- Upload the image to ECP’s built-in container registry.    
- Run the image in multiple edge locations on the ECP platform.    
- Manage global traffic for the application.    

### Prerequisites
Before you get started, make sure you have: 

- Subscribed to ECP service and have a master portal user account to use the console.    
- Docker installed on your computer.    
- NodeJS and NPM installed.

### Create an ECP registry project and registry user
In this demo, we’ll upload a Docker image to the ECP registry, and then deploy it from the registry. Before the image can be uploaded, we will need to create an ECP registry project and a registry user.
  
Log in to the [ECP management console](https://console.cdnetworks.com/ecp).

**Create an ECP registry project**
<p align=center><img src="/docs/resources/images/recipes/recipe1/create-registry-project.png" alt="create registry project" width="720"></p>

1.  Open the **Registry Projects** page and click the top-right **Add New Project** button to open a dialog box.    
2.  Enter “myproject1” as the **Project Name**.    
3.  Disable the **Deployment Security** setting. We are disabling this setting to make sure our demo image can be deployed. When running your images in production, it is recommended to enable this setting.    
4.  Turn on **Vulnerability Scan**.  
5. Click the **Submit** button to create the registry project.

**Create an ECP registry user**
<p align=center><img src="/docs/resources/images/recipes/recipe1/create-registry-user.png" alt="create registry user" width="720"></p>

1.  Open the **Registry Users** page and click the top-right **Add New User** button.    
2.  Enter “myreguser1” as the **Username**.    
3.  Enter a password and an email address.    
4.  Give the new registry user read-write access to existing registry projects. This demo has one “existing project” called “myproject1”. Read-write permission is required so the new registry user can upload images to and download images from the registry project.    
5.  Click the **Submit** button to create this registry user.   
  
To avoid naming collisions, ECP appends a random string to the username when a registry user is created. The following screenshot shows the new registry user which has a random string appended as part of its username.
<p align=center><img src="/docs/resources/images/recipes/recipe1/registry-user-list.png" alt="registry user list" width="720"></p>

Remember this full username as well as the password you provided. You’ll need the credentials when you log into the ECP registry and upload images to the registry using the docker CLI.
  
An imagePullSecret is created automatically for the new registry user, as shown on the imagePullSecrets page. You’ll need to select this imagePullSecret when deploying the sample web application to ECP locations.
<p align=center><img src="/docs/resources/images/recipes/recipe1/imagePullSecret-list.png" alt="imagePullSecret list" width="720"></p>

### Build a sample web application into a Docker image
**Prepare a sample web application**

For this demo, let’s use [Express application generator](https://expressjs.com/en/starter/generator.html) to quickly “write” a very basic NodeJS web application.

 1. Run the following commands to make sure that NodeJS and NPM are installed on your machine.
```
>node -v
>npm -v
```
 2. Install the Express application generator as a global npm package, and then launch it.
```
>npm install -g express-generator
>express
```
 3. Use the application generator to create a web app named `myapp`. This will create a folder named `myapp` in your working directory. All source files for this web app will be stored in this folder.
```
>express myapp
```
 4. Enter the `myapp` folder and install dependencies.
```
>cd myapp
>npm install
```
5. Run the app.
```
>npm start
```
6. Access the app in your browser via http://localhost:3000 (the app listens on port 3000). If the app is generated correctly, a page similar to the following appears.
<p align=center><img src="/docs/resources/images/recipes/recipe1/express-demo-page.png" alt="express demo page" width="720"></p>

If you’re using Linux, run the command `curl http://localhost:3000` to access the app.

The generated app will have the following directory structure.
```
.
├── app.js
├── bin
│ └── www
├── package.json
├── public
│ ├── images
│ ├── javascripts
│ └── stylesheets
│ └── style.css
├── routes
│ ├── index.js
│ └── users.js
└── views
├── error.pug
├── index.pug
└── layout.pug 

7 directories, 9 files
```
**Build the sample web application into a Docker image**

Now that we finished “writing” the application and have the source code, let’s containerize the application, where we will build the application into a Docker image, and then run the application as container(s).
1. Write a Dockerfile.

According to the [official Docker documentation](https://docs.docker.com/engine/reference/builder/), “*Docker can build images automatically by reading the instructions from a Dockerfile. A Dockerfile is a text document that contains all the commands a user could call on the command line to assemble an image.*” Therefore, to build our application into a Docker image, we first need to write a Dockerfile. 

On the `myapp` directory, create a file named `Dockerfile` and include the following content in the file.
```
FROM node:14-alpine # Specify a base image to start building a new image from. As we’re building a NodeJS app, let’s use “node” as the base image and pick one of its image tags
WORKDIR /usr/src/app # Set the working directory inside the image
COPY package*.json ./ # Copy local file “package.json” onto the image’s filesystem
RUN npm install # Run this command to install project dependencies as per “package.json”
COPY . . # Copy the application source code onto the image’s filesystem
EXPOSE 3000 # Tell Docker which port the application will be listening on at runtime
CMD ["npm", "start"] # Tell Docker how to run the application
```
2. Write a `.dockerignore` file.

On the `myapp` directory, create a `.dockerignore` file to tell Docker to skip unnecessary files when building a Docker image. This will reduce the image size. For this demo, the subdirectory `node_modules` and the `Dockerfile` itself on the `myapp` directory can be skipped. As a result, the `.dockerignore` file will have the following content.
```
node_modules
Dockerfile
```
3. Build a Docker image.

Build an image with the Dockerfile written in step 1. Run the `docker build` command on the `myapp` directory, and pass the `-t` flag to tag the image. Remember that you should have Docker installed on your computer.
```
>docker build -t myapp:v1 .
```
If the build succeeds, you’ll see the image in the output of the `docker images` command.
```
>docker images
REPOSITORY TAG IMAGE ID CREATED SIZE
myapp v1 00ec08c1dfcb 7 seconds ago 125MB
```
4. Run the Docker image locally to verify that the containerized application works as expected.

Enter `docker run` to run the image you just built. Use the `-d` flag to run the container in detached mode and the `-p` flag to port forward port 3000 on which the NodeJS app listens to port 3000 on your local machine.
```
>docker run -d -p 3000:3000 myapp:v1
```
Run `docker ps` to list active containers.
```
>docker ps
CONTAINER ID IMAGE COMMAND CREATED STATUS PORTS NAMES
a5b5d36594fc myapp:v1 "docker-entrypoint.s…" 10 seconds ago Up 4 seconds 0.0.0.0:3000->3000/tcp, :::3000->3000/tcp hopeful_lalande
```
Access the app in your browser via http://localhost:3000, or run the command `curl http://localhost:3000` if you’re using Linux. 

Then stop the container.
```
>docker stop a5b5d36594fc
```
### Push Docker image to ECP registry
Now that the Docker image is built and verified, let’s push the image to the ECP registry, and then deploy the image from there.  

 1. Docker login ECP registry
```
>docker login registry-qcc.quantil.com
Username: myreguser1-xxxx
Password:
Login Succeeded
```
The ECP registry service is available at [https://registry-qcc.quantil.com](https://registry-qcc.quantil.com). Use the credentials created [above](#create-an-ecp-registry-project-and-registry-user) to authenticate with the registry.
  
When you create an ECP registry user by yourself, you’ll get a unique full username because it contains a randomly generated string. So you’ll need to authenticate with the registry using the full username created for you.

 2. Retag the Docker image.
```
>docker tag myapp:v1 registry-qcc.quantil.com/myproject1/myapp:v1
```
Retag the Docker image and allow it to be pushed to your ECP registry project. The new tag must resemble `registry-qcc.quantil.com/{project}/{repository}:{tag}`, where `{project}` refers to an ECP registry project. In this demo, the project used is `myproject1`. The registry address and project must be correct; otherwise, image pushing will fail. 

Now there should be 2 images on your local machine.
```
>docker images
REPOSITORY TAG IMAGE ID CREATED SIZE
myapp v1 00ec08c1dfcb 30 seconds ago 125MB
registry-qcc.quantil.com/myproject1/myapp v1 00ec08c1dfcb 6 seconds ago 125MB
```
3. Push the Docker image to ECP registry.
```
>docker push registry-qcc.quantil.com/myproject1/myapp:v1
```
When the push succeeds, go to the ECP management console and open the detail page of the registry project `myproject1`. You’ll see an entry similar to the following in the **Repositories** list.
<p align=center><img src="/docs/resources/images/recipes/recipe1/repositories-list.png" alt="repositories list" width="720"></p>

### Deploy the web application to multiple ECP locations
Now it’s time to deploy the web application at scale to global ECP locations.

**Deploy the application**
1. Open the **Applications** page on the console, and then click the top-right **Add New Application** button.
2. Click the **Use a Wizard** option to have a wizard guide you through the steps of adding an application.
3. At step 1 of the wizard, configure the new application.
<p align=center><img src="/docs/resources/images/recipes/recipe1/wizard-step-1-pod-template.png" alt="wizard step 1 pod template" width="720"></p>

Under **Pod Template**, enter “myapp” for **Application Name**, select “Deployment” for **Pod Controller**, and select the imagePullSecret that’s automatically created along with creation of the new ECP registry user.
<p align=center><img src="/docs/resources/images/recipes/recipe1/wizard-step-1-container.png" alt="wizard step 1 container" width="720"></p>

Under **Container**, enter “myapp” for **Container Name**, use the image picker to pick the Docker image that was pushed to the ECP registry, and request resources of 200m cpu and 300MB memory for the container.
  
Then click the top right **Next** button to go to the next step.

4. At step 2 of the wizard, expose the application.
<p align=center><img src="/docs/resources/images/recipes/recipe1/wizard-step-2-select-exposure-method.png" alt="wizard step 2 select exposure method" width="720"></p>

Leave the option **Expose via layer 4 load balancer** at its selected state.
<p align=center><img src="/docs/resources/images/recipes/recipe1/wizard-step-2-listener.png" alt="wizard step 2 listener" width="720"></p>

Enter “3000” for **Listener Port** and select “TCP” for **Protocol**. Although you can change the other fields to suit your requirements, leave them as they are for now. 

Then click the top-right **Next** button to go to the next step.  

5. Choose deployment targets for the application on step 3 of the wizard
<p align=center><img src="/docs/resources/images/recipes/recipe1/wizard-step-3.png" alt="wizard step 3" width="720"></p>

Click the **Distribute per PoP** option, and then add deployment targets. In the example above, we’ll run 2 instances in Seattle (sea), 1 instance in Paris (cdg1), and 1 instance in Sydney (syd1).
  
Click the top-right **Next** button to go to the next step.

6. Review the configurations. If you need to make changes, return to the previous steps and make the change. When done, click the top-right **Submit & Deploy** button to initiate the deployment.

The wizard will close and you’ll be directed to the **Applications** page. The new application appears in the application list. As the deployment proceeds in the background, the status changes from `waiting` to `deploying`, and then to `deployed`. The deployment takes approximately 30 seconds.
<p align=center><img src="/docs/resources/images/recipes/recipe1/applications-list.png" alt="applications list" width="720"></p>

 **View the application**

On the **Applications** page, click the name of the newly deployed application to open its detail page and view application details.
  
The **VIPs** section lists VIPs that expose the application in different ECP locations.
<p align=center><img src="/docs/resources/images/recipes/recipe1/VIPs-list.png" alt="VIPs list" width="720"></p>

Select any VIP and open `{VIP}:3000` in your browser. For example, go to http://163.171.243.176:3000 in your browser. You’ll see the familiar Express demo page. This means the application is now running in multiple ECP locations and that all of its instances are serving traffic from different locations.
  
On the **Applications** page, click the **Instances** column of the newly deployed application to check the instances of the application.
<p align=center><img src="/docs/resources/images/recipes/recipe1/instances-list.png" alt="instances list" width="720"></p>

The instances list shows 2 running instances in Seattle, 1 running instance in Paris, and 1 running instance in Sydney. This matches exactly what we specified as deployment targets.

### Turn on intelligent global traffic management for the web application

Now that the application is running at multiple ECP locations, let’s turn our attention to traffic routing by creating a CNAME.
<p align=center><img src="/docs/resources/images/recipes/recipe1/create-CNAME.png" alt="create CNAME" width="720"></p>

1. Open the **CNAMEs** page on the console and click the top-right **Add New CNAME** button to open a dialog box.
2. Click the **Auto Generate** button to generate a CNAME prefix.
3. Select the newly deployed application “myapp” for **Application**.
4. Click the **Submit** button to create the CNAME.
  
A new CNAME is created, as shown on the **CNAMEs** page.
<p align=center><img src="/docs/resources/images/recipes/recipe1/CNAMEs-list.png" alt="CNAMEs list" width="720"></p>

Open `{CNAME}:3000` in your browser. You’ll see the Express demo page. This page indicates that access to the application can now be routed to its instances at different locations via the CNAME. Note that the newly created CNAME might take a few minutes to work. Also note that using `{CNAME}:3000` to access a deployed ECP application works only for the Express web application in this demo. In practice, your own web application will probably process incoming requests by different hostname(s) and port(s). Therefore, you’ll need to change or create a CNAME record for the hostnames of your web application, point the hostnames to the ECP CNAME, and then access your application via your hostnames and ports instead of directly using the ECP CNAME.
  
To further verify how requests will be routed to different instances at the edge, use the [DNS checker](https://dnschecker.org/) to check what IP address the CNAME will resolve to in various parts of the world.
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEwMjE5MjYwNDgsLTEyMTg2MjA5NCwtMj
AzMzc2MzMzNSw4NzE3MTQ2NDIsLTIwMzA2NzE4MDMsMTExMDg3
MTg2Miw3MzA5OTgxMTZdfQ==
-->