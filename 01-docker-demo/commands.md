First, clone the app into the server

```
git clone https://github.com/docker/getting-started.git
```

Then, change into the directory of the app

```
cd getting-started/app
```

Create a Dockerfile

```bash
cat <<EOF > Dockerfile
# syntax=docker/dockerfile:1
   
FROM node:18-alpine
WORKDIR /app
COPY . .
RUN yarn install --production
CMD ["node", "src/index.js"]
EXPOSE 3000
EOF
```

```powershell
@'
# syntax=docker/dockerfile:1
   
FROM node:18-alpine
WORKDIR /app
COPY . .
RUN yarn install --production
CMD ["node", "src/index.js"]
EXPOSE 3000
'@ | Out-File -FilePath "Dockerfile" -Encoding UTF8

```

Now build the image

```
docker build -t getting-started .
```

You will now have an image named getting-started

Finally, create a container from that image and expose the port 3000 of the container on port 3001 of the host
```
docker run -p 3001:3000 getting-started
```

You can now open the port 3001 of the host. You will be able to access it from outside and see your todo app!
Play around and add some todos

Ctrl + C to stop running the container

Try running the command again. 
* Refresh the page
* What happened to the todo list you created?