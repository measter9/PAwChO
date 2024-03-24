# Tworzenie lokalnego rejestru z samodzielnie podpisanym certyfikatem

Tworzenie drzewa katalogów dla rejestru:

``
mkdir registry
``

``
mkdir /registry/certs
``

``
mkdir /registry/certs
``

Generowanie klucza prywatnego i certyfikatu:

``cd certs/``

``openssl genrsa 1024 > domain.key``

``chmod 400 domain.key``

``openssl req -new -x509 -nodes -sha1 -days 365 -key domain.key -out domain.crt``

Tworzenie danych logowania:

``cd ../auth/``

``docker run --rm --entrypoint htpasswd registry:2.7.0 -Bbn username password > htpasswd``

Uruchomienie kontenera rejestru:

``docker run -d   --restart=always   --name registry_CA   -v `pwd`/auth:/auth   -v `pwd`/certs:/certs   -v `pwd`/certs:/certs   -e REGISTRY_AUTH=htpasswd   -e REGISTRY_AUTH_HTPASSWD_REALM="Registry Realm"   -e REGISTRY_AUTH_HTPASSWD_PATH=/auth/htpasswd   -e REGISTRY_HTTP_ADDR=0.0.0.0:443   -e REGISTRY_HTTP_TLS_CERTIFICATE=/certs/domain.crt   -e REGISTRY_HTTP_TLS_KEY=/certs/domain.key   -p 443:443   registry:2.7.0``

Wgrywanie obrazu na serwer:

``docker push localhost:443/ubuntu``

![docker_push](https://i.imgur.com/d504ZhB.png)

Logowanie

![logowanie](https://i.imgur.com/LV8A2iS.png)

![push_success](https://i.imgur.com/fCCXhQK.png)

Lista obrazów w repozytorium:

``curl -k -X GET -u username:password https://localhost:443/v2/_catalog``

![lsit](https://i.imgur.com/18FKHCB.png)

Pobranie obrazu z rejestru

``docker pull localhost:443/ubuntu``

![pull](https://i.imgur.com/egKa0uB.png)
