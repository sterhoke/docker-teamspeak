ster/teamspeak
docker image for TeamSpeak 3 Server
based off of debian:jessie

To pull this image:
docker pull ster/teamspeak

Note: This Dockerfile will always install the very latest version of TS3 available.

Example usage (no persistent storage; for testing only - you will lose your data when the container is removed):

docker run -d --name teamspeak -p 9987:9987/udp -p 30033:30033 -p 10011:10011 -p 41144:41144 ster/teamspeak

Advanced usage with persistent storage:
On your host, create necessary directories, files, and set permissions:

mkdir -p /data/teamspeak
chown -R 503:503 /data/teamspeak
Start container:

 docker run -d --restart=always --name teamspeak \
   -p 9987:9987/udp -p 30033:30033 -p 10011:10011 -p 41144:41144 \
   -v /data/teamspeak:/data \
   ster/teamspeak
In order to get the credentials for your TS server, check the container logs as it will output the serveradmin password and your ServerAdmin privilege key.

For additional parameters, check the (6) Commandline Parameters section of the TeamSpeak 3 Server Quickstart Guide. Either add the parameters to ts3server.ini or specify them after the Docker image name.

Example:

docker run -d --restart=always --name teamspeak \
  -p 9987:9987/udp -p 30033:30033 -p 10011:10011 -p 41144:41144 \
  -v /data/teamspeak:/data \
  ster/teamspeak \
  clear_database=1 \
  create_default_virtualserver=0
