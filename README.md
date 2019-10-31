# Securely Installing Grafana with Docker
## References:
1. https://grafana.com/docs/installation/docker/
2. https://www.digitalocean.com/community/tutorials/how-to-install-and-secure-grafana-on-ubuntu-18-04

## Docker:
```
mkdir data

docker run \
  -d \
  -e USER=$USER \
  -e USERID=$UID \
  --memory="1024m" \
  --cpu-shares=512 \
  -e GF_SECURITY_ADMIN_USER=USERNAME_GOES_HERE \
  -e GF_SECURITY_ADMIN_PASSWORD=PASSWORD_GOES_HERE \
  --name=grafana \
  -p 9003:3000 \
  -v "$PWD/data:/var/lib/grafana" \
  -v "$PWD/defaults.ini:/usr/share/grafana/defaults.ini" \
  grafana/grafana
```

Go to localhost:9003 and enter your credentials from above the GF_SECURITY_ADMIN_USER and GF_SECURITY_ADMIN_PASSWORD.

## Notes:
1. Change your username/password in the environment variables above.
2. Make sure you have the defaults.ini file.
3. Change the port to access grafana via changing `3000:3000`. Example: `9003:3000` then look at localhost:9003
4. If you are using a database, ensure that you have a user setup with only read (SELECT) access.
5. To change the password in grafana, log in as the admin and go to Server Admin > User then click on the user.
6. To add a user in grafana (such as a guest), log in as the admin and go to Server Admin > User > New User .
7. If you restart the server with different username/password, the changes won't be made because of the volume we made with data. It is stored. You can either remove the data directory (you'd lose everything) or you can change the password and create a user in grafana.

## Next Steps:
1. Include Prometheus in your projects for the PEG stack.
2. Include an Exporter (ex: Node-Exporter) for the PEG stack.
