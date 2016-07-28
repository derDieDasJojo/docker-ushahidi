FROM nginx
RUN apt-get update && apt-get install -y wget
WORKDIR /app 
RUN 	rm -rf /usr/share/nginx/html
RUN wget -O platform-client.tar.gz https://github.com/ushahidi/platform-client/releases/download/v3.4.7/ushahidi-platform-client-bundle-v3.4.7.tar.gz && tar -xvf platform-client.tar.gz &&\
	rm platform-client.tar.gz
RUN	mv /app/ushahidi-platform-client-bundle-v3.4.7 /usr/share/nginx/html
WORKDIR /usr/share/nginx/html
ADD config.js /usr/share/nginx/html/config.js
ADD setup.sh /app/setup.sh
#CMD /app/setup.sh	
