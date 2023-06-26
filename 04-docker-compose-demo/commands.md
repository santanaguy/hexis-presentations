First, create the docker-compose file



``` bash
cat <<EOF > docker-compose.yml
services:
  vote: #service name
    scale: 3
    image: dockersamples/examplevotingapp_vote 
    ports:
      - "5000-5005:80" #format host_port:container_port
    networks: #which networks will this container belong to?
      - front-tier
      - back-tier

  result:
    image: dockersamples/examplevotingapp_result
    ports:
      - "5001:80"
    networks:
      - front-tier
      - back-tier

  worker:
    image: dockersamples/examplevotingapp_worker
    networks:
      - back-tier

  redis:
    image: redis:alpine
    volumes:
      - "./healthchecks:/healthchecks"
    networks:
      - back-tier

  db:
    image: postgres:15-alpine
    environment:
      POSTGRES_USER: "postgres"
      POSTGRES_PASSWORD: "postgres"
    volumes:
      - "db-data:/var/lib/postgresql/data"
      - "./healthchecks:/healthchecks"
    networks:
      - back-tier

volumes:
  db-data:

networks:
  front-tier:
  back-tier:
EOF
```

For Powershell: 
```powershell
@'
services:
  vote: #service name
    scale: 3
    image: dockersamples/examplevotingapp_vote 
    ports:
      - "5000-5005:80" #format host_port:container_port
    networks: #which networks will this container belong to?
      - front-tier
      - back-tier

  result:
    image: dockersamples/examplevotingapp_result
    ports:
      - "5001:80"
    networks:
      - front-tier
      - back-tier

  worker:
    image: dockersamples/examplevotingapp_worker
    networks:
      - back-tier

  redis:
    image: redis:alpine
    volumes:
      - "./healthchecks:/healthchecks"
    networks:
      - back-tier

  db:
    image: postgres:15-alpine
    environment:
      POSTGRES_USER: "postgres"
      POSTGRES_PASSWORD: "postgres"
    volumes:
      - "db-data:/var/lib/postgresql/data"
      - "./healthchecks:/healthchecks"
    networks:
      - back-tier

volumes:
  db-data:

networks:
  front-tier:
  back-tier:
'@ | Out-File -FilePath "docker-compose.yml" -Encoding UTF8

```

Then bring the containers up by running:

```
docker compose up
```

Finally open the ports on which the containers are exposed (5000 and 5001)
Now, vote!