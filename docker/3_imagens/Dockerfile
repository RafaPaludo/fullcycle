## Reference: https://docs.docker.com/reference/dockerfile/
FROM nginx:latest

COPY html/ /usr/share/nginx/html/

ENTRYPOINT ["/docker-entrypoint.sh"]

CMD ["nginx", "-g", "daemon off;"]