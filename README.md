server {
	  listen       80;
    	  server_name  cp.netmera-dev.com;
     	  #charset koi8-r;
    	  #access_log  /var/log/nginx/log/host.access.log  main;
	
	  location / {
     	    proxy_set_header   X-Real-IP $remote_addr;
     	    proxy_set_header   Host      $http_host;
  	    proxy_pass         http://127.0.0.1:8080;
    	    add_header         X-Robots-Tag noindex always;
            add_header Cache-Control no-cache;
            expires off;
            sendfile  off;
      	    }
      	   
      	    #admin sayfasi icin gerekli olan config
  	    location ~ ^/nmadmin/((js|views|css|img)/.*)$ {
            alias /home/nurselincanturk/netmera/nova/modules/gui/modules/gui-admin/src/main/webapp/$1;
            }
            #gui-panel sayfasi icin gerekli config
            location ~ ^/((js|views|css|img)/.*)$ {
            alias /home/nurselincanturk/netmera/nova/modules/gui/modules/gui-panel/src/main/webapp/$1;
            }
