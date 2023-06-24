# Portainer

docker volume create portainer_data
docker run -d -p 8000:8000 -p 9000:9000 --name portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce:latest

# SQL Server
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=yourStrong()Password" -p 1433:1433 --name sqlserver -d mcr.microsoft.com/mssql/server:2022-latest

docker exec -it sqlserver /opt/mssql-tools/bin/sqlcmd -S localhost -U sa -P "yourStrong()Password"

# Ravendb