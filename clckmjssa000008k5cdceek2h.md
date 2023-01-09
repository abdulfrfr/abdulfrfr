# Introduction to Docker.

**DOCKER**

**What is Docker?**

Docker is a “Container Runtime” used to run applications as containers in isolated environments, with all source codes and configurations compiled and built as an image to run as a container. Now, this brings us to "What exactly is a container". Now we are going to talk about Containers and Virtual Machines.

**What is a Virtual Machine?**

A Virtual Machine is an emulation of the functionalities of another Operating system running on one physical machine with its own kernel.

**What is a Container?**

Unlike Virtual Machines, Containers share your local machine's kernel and operating system which makes it faster and lightweight compared to virtual machines.

Both Containers and Virtual Machines solve the same problems, but it's all based on your required outcome and the number of resources you intend on using on your project.

To have a Container running, we will need an Image to run as our container. So basically, a container is a running instance of an image.

**What is an Image?**

An Image is a blueprint for containers; it is your built application with all source codes, required packages, dependencies, configuration, and commands built in. With Images, applications can be shared across different machines and will run the same way on any machine.

**DOCKERFILE**

**NOTE: Before following along, please make sure you have Docker Desktop installed and running on your local machine!!!**

**what is Dockerfile?**

A Dockefile is a configuration file in Docker for building images.

Now, let’s create an Image!!!

First of all, let me explain some concepts to you guys.

So basically, images are built in several layers, and in every layer, a new configuration is added, like installing dependencies, copying our source codes, and running the application. That might not get into your head now, but you will understand once I show you a visual example.

Now, we are going to build an image with a node application, as seen in the image below, this is a simple node application that just returns a JSON object.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1673014912169/dd3d01df-84e6-4084-b1e5-e177d9180990.png align="center")

Now, if we are to run this application locally we will need to run “npm install” first, to install all the required dependencies, because we have an express dependency we will need for our node application, as seen below.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1673015008262/3101dea7-ba2f-46a0-8718-17e0f3ae2d89.png align="center")

And after that, we will run "node app.js" to run our application, because app.js is the name of the file carrying our source code, and that will run our application locally on our computer with the node version I have installed on our computer, but that's not what we want, we want to run our application in an isolated environment with its version of the node running inside of it. And for that, we will need to build an image. And out image is going to have its first layer as a parent image. Which will be the "Node" and it version we want our application to run on in its isolated environment. To carry out all the required layers to build our image, we will need to create a file called **“Dockerfile”**. That exact way, because that is what docker has required from us, “the file used to build images in docker must be name Dockerfile”. Please Note that. And, I will show you an image below.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1673015092754/a0357218-0999-4282-bed3-7afb3361369d.png align="center")

Now, we said our first layer will be specifying our parent image which will be the node version we want our application to run on since we are building a node application image. And we do that using the "FROM" keyword from Docker, which tells docker to go and grab a particular image from the docker hub, which is a repository for docker images, and we will talk about that later on. We use the "FROM" keyword together with specifying the name of the image which in our case will be "node" because that is the way it was named in the docker hub. After specifying the name of the parent image, we specify a tag which is the version we need to run our application on like so “node:latest”, which will be the latest version of node, using an older version can be specified as “node:17-alpine” as it will be tagged on Dockerhub, our latest version of node will be written as seen below.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1673015122431/ba4ed71c-b07e-48f6-8b4b-68d10a7916e9.png align="center")

There are other versions of a node image that you can find in the docker hub, but in our case, we are using the latest version, and where the word "latest" is written is where we specify the version of our node. And that’s our first layer, which is specifying our parent image which our application is dependent on.

Now our next layer will be copying our source files and codes over to our image, and it’s done using the keyword “COPY” and then a “.” And then another “.”, as seen below.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1673015169882/f28ee59b-4458-4cdc-9dbe-1ebc3ced0917.png align="center")

And what this means is we are copying all our source files into our image, where the first "." This means the current directory where our Dockerfile is and the second “.” Is a path to the root directory of our image (NOTE: Our Images to has their folder structure inside of it, which can be accessed when we run our container). Now, if our source files are inside a "src” folder and not the current folder where our Dockerfile is, then the first “.” Is going to be “./src”. Now, there is a problem, a lot of times we don't copy our source files into the root directory of our image, so that it doesn't clash with other files in our root directory, instead we specify a path like "/App", which is going to create a new folder inside our image and copy all our source files into it. As seen below.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1673015198780/06309f77-62d6-4328-8c54-39bc6188c18d.png align="center")

Now, our next step is to install our dependencies with “npm install", which we talked about earlier, and to do that we use the keyword "RUN" followed by the command we want to run, like so;

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1673015284989/40ca68de-5ea5-43f0-9f6a-32807c9ad5bf.png align="center")

Now, we have another problem, we copied our source files into a folder we called “App” inside our image, now the “RUN” command is not going to see the “package.json" where our dependencies are specified, and that's a problem because our image will not be built. But there is a solution for that, we can use the keyword "WORKDIR", which tells docker the particular location to carry out every other layer in the process of building our image, and we will do that before we copy all the source files into the “App” folder. Like so;

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1673015421126/2c3960fe-91b1-4783-a880-1cfd2ad851a1.png align="center")

Now, every other command under the "WORKDIR" like "COPY" and "RUN" and others we will specify later will be carried out inside the "/App" folder as we have declaratively specified. And now, here comes another problem, when docker runs the “COPY” command, now a new folder will be created and the source files will be copied to a location like “/App/App” because we have already specified a working path. Now, the solution to that is to copy our source files to the current image directory we are which is the “WORKDIR” we have specified. And that will be done like so;

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1673015455824/4f7c8295-624f-4cc2-bc42-90f59738e3fd.png align="center")

And now while copying our source files, it will be copied into that “/App” folder we have specified as our working directory and then we will be inside that directory and for the “RUN” command, “npm install” will see our package.json file and our dependencies will be installed. All problems solved😊.

Now, the next layer is to run "node app.js" inside our image to run our application, but we cannot use the "RUN" keyword, because what it does is run a command while creating the image, and what we want is to run “node app.js” when we have a running instance of our image and not while building the image. And to do that we use the “CMD” command which values are written in an array of strings like this “\[“node”, “app.js”\]”, and we want that to be done after our image is created and as a running instance. Like so;

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1673015560882/311fd25c-844d-468c-82d3-80ad5e6ba0d9.png align="center")

Now, from our app.js code, we specified a port where our app should listen on, which was “4000”. Now we also want to specify a port where we want docker to expose our application. This is optional if our application is just a command line application, but if we want to access our application from our web browser, then docker is going to need it for what we call “Port Mapping”, which I will talk about in another article of mine. And now we expose our application to a port using the “EXPOSE” keyword and we want to do that before we run our “node app.js” command like so;

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1673015605146/ef518413-91b2-4e03-960b-67aaeb7fc2e0.png align="center")

And now docker will expose our application on port 4000 internally. And can map any external port to it to open our application in a browser.

In summary, the layers docker went through to build our application image for us are these;

First, docker will get us the node image from the docker hub which our application is dependent on, then make us a working directory to carry out all other layers within, then inside that working directory we copied all our source files into it, then run "npm install” to install all the necessary dependencies stated in our package.json file at build time, then after the image is built and we have a running instance of our image, docker exposes our application to port 4000 as we specified, then docker runs the “node app.js” command to start up the application in the image’s running instance(container).

Now that's it for the image-building configuration using Dockerfile. Now to build our image, we need to run a single command. Now we make sure we are in the directory where our "Dockerfile” file is located and run the command like so;

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1673015647389/21df4a6f-b393-4801-ad17-b13175e2c982.png align="center")

We use “docker build”, then “-t” which allows us to specify a name and tag for our image, and then “.”, This indicates that the "Dockerfile” file is inside the same present working directory, so it’s going to go through the “Dockerfile” file and follow the instruction and configuration we have declared. After the build process is completed, you will see the image in your Docker Desktop app and can use the UI to run your image.

Thanks for Reading.

Next, I will be writing to you guys about Docker Compose. Stay tuned. And I will also publish more articles on Sofware Engineering, Cloud, and DevOps. Thank you once again.