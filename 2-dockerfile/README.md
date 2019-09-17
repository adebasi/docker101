# Publish your first image

The index.html of the website from the previous example was mounted into the container. It is not possible to provide this to your production environment. To ship your website, you have to create an image containing your `index.html`. 

## Create your image

Images are created by the docker command `docker build` using a Dockerfile.

Go ahead and create a file named `Dockerfile` in this folder. We want to extend the previously used image `nginx` and copy the `index.html` into the image. Take a look at the official [Dockerfile references](https://docs.docker.com/engine/reference/builder/). You will need the commands `FROM`, which is always the first line of a Dockerfile, and the `COPY` command.

After creating the Dockerfile you can build the image like this: 

`$ docker build -t 1337docker101/website:<your-name> .`

## Run your image

Having your own image, you can start it. Please note that the image name has to be the same like in the `build` command.

`$ docker run -d -p 8080:80 1337docker101/website:<your-name>`

## Publish your image

We created a docker hub account named `1337docker101`. That's why you named your images like that. Non official images at docker hub are prefixed with the account name. 

Login to this account using the credentials we gave to you:

`$ docker login`

You can publish your image now:

`$ docker push 1337docker101/website:<your-name>`

## Run your image on someone else's computer

Now use the laptop of your pairing partner and execute the docker run command from above. You will download your created image and start a container. You shipped your website to someone else's computer! Great success ;-)