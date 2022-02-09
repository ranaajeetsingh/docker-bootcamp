Sample Applicatin to start with --

cd /path/to/working/directory
git clone https://github.com/spring-projects/spring-petclinic.git
cd spring-petclinic

Test the application without docker

mvnw spring-boot:run

Application access: http://localhost:8080

Create a Dockerfile for Java
A Dockerfile is a text document that contains the instructions to assemble a Docker image. When we tell Docker to build our image by executing the [docker build ]command, Docker reads these instructions, executes them, and creates a Docker image as a result.

What to name your Dockerfile?

The default filename to use for a Dockerfile is Dockerfile (without a file- extension). Using the default name allows you to run the docker build command without having to specify additional command flags.

Some projects may need distinct Dockerfiles for specific purposes. A common convention is to name these Dockerfile.<something> or <something>.Dockerfile. Such Dockerfiles can then be used through the --file (or -f shorthand) option on the docker build command. Refer to the “Specify a Dockerfile” section in the docker build reference to learn about the --file option.

Reference file: Dockerfile

Create a .dockerignore file

To increase the performance of the build, and as a general best practice, we recommend that you create a .dockerignore file in the same directory as the Dockerfile. Folders or files mentioned in this file excludes from the Docker build context.

Reference file: .dockerignore

Build an image

The tag is used to set the name of the image and an optional tag in the format name:tag. We’ll leave off the optional tag for now to help simplify things. If we do not pass a tag, Docker uses “latest” as its default tag.

docker build --tag java-docker .

View local images

docker images

Tag images

The docker tag command creates a new tag for an image. It does not create a new image. The tag points to the same image and is just another way to reference the image.

docker tag java-docker:latest java-docker:v1.0.0

Let’s remove the tag that we just created. To do this, we’ll use the rmi command. The rmi command stands for “remove image”.

docker rmi java-docker:v1.0.0

To delete the image:

docker image rm -f java-docker:latest

To run an image inside a container, we use the docker run command

docker run java-docker

container is running in isolation which includes networking. To publish a port for our container, we’ll use the --publish flag (-p for short) on the docker run command. The format of the --publish command is [host port]:[container port].

docker run --publish 8080:8080 java-docker

Run in detached mode

To do this, we can use the --detach or -d for short.

docker run -d -p 8080:8080 java-docker

List containers

docker ps

docker stop [name_in_ps_command]

Stop, start, and name containers

When we pass the --all or -a for short, we see all containers on our machine, irrespective of their start or stop status.

docker ps -a

To restart a container:

docker restart trusting_beaver

When you restart a container, it starts with the same flags or commands that it was originally started with.

To remove a container, simple run the docker rm command passing the container name.

docker rm trusting_beaver modest_khayyam lucid_greider

Now, let’s address the random naming issue. To name a container, we just need to pass the --name flag to the docker run command.

docker run --rm -d -p 8080:8080 --name springboot-server java-docker