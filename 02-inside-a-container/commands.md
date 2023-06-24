Run the getting started container once again, but now in detached mode

```
docker run -d --name getting-started -p 3001:3000 getting-started
```

Now attach to the container using a shell

```
docker exec -it getting-started /bin/sh
```

First, lets list the filesystem of the container
```
ls
```

We have a full file system in it.

Now lets list the processes running in this container

```
top
```

Notice how the container is only running node, and then our commands.

Also notice how the PID 1 is node. What happens if we kill this process?

```
kill 1
``` 

The container exits because the root process was aborted. 
This means if your application dies, the container dies with it. Also, it explains why containers are so lightweight: nothing else besides your app is running on them