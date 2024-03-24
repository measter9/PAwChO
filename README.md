# PAwChO
Budowanie obrazu:

`docker build -f Dockerfile_z1 -t local/z1:v0 .`

Uruchomienie:

`docker run -d -p 8080:8080 --name web100 local/z1:v0`

obraz posiada 4 wartwy powstałe w wyniku operacji RUN i COPY oraz podstawowej warstwy ubuntu

![docker history](https://i.imgur.com/mQOBcow.png)

![curl](https://i.imgur.com/vSVm5Kp.png)

