# PAwChO
Budowanie obrazu:
`docker build -f Dockerfile_z1 -t local/z1:v0 .`

Uruchomienie:
`docker run -d -p 8080:8080 --name web100 local/z1:v0`

![docker history](https://i.imgur.com/mQOBcow.png)

