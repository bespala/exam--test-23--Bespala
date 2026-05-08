version: "3.8"

services:
  emqx:
    image: emqx/emqx:5
    container_name: exam-emqx
    restart: unless-stopped
    ports:
      - "1883:1883"
      - "8083:8083"
      - "18083:18083"
    volumes:
      - ./emqx.conf:/opt/emqx/etc/emqx.conf:ro

  web1:
    image: nginx:alpine
    container_name: exam-web1
    ports:
      - "8081:80"
    volumes:
      - ./src/web1:/usr/share/nginx/html:ro
    depends_on:
      - emqx

  web2:
    image: nginx:alpine
    container_name: exam-web2
    ports:
      - "8082:80"
    volumes:
      - ./src/web2:/usr/share/nginx/html:ro
    depends_on:
      - emqx
