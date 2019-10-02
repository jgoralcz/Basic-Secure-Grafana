# Securely Installing Grafana with Docker
## References:
1. https://grafana.com/docs/installation/docker/
2. https://www.digitalocean.com/community/tutorials/how-to-install-and-secure-grafana-on-ubuntu-18-04

## Docker:
```
mkdir data # creates a folder for your data

ID=$(id -u) # saves your user id in the ID variable

docker run \
  -d \
  --user $ID \
  -e GF_SECURITY_ADMIN_USER=USERNAME_GOES_HERE \
  -e GF_SECURITY_ADMIN_PASSWORD=PASSWORD_GOES_HERE \
  --name=grafana \
  -p 9003:3000 \
  -v "$PWD/data:/var/lib/grafana" \
  -v "$PWD/defaults.ini:/usr/share/grafana/defaults.ini" \
  grafana/grafana
```

Go to localhost:3000 and enter your credentials from above.

## Notes:
1. Change your username/password in the environment variables above.
2. Make sure you have the defaults.ini file.
3. Change the port to access grafana via changing `3000:3000`. Example: `9003:3000` then look at localhost:9003
4. If you are using a database, ensure that you have a user setup with only read (SELECT) access.
