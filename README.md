# nginx

### 9200整個根目錄導到9100
     server {
          listen 9200;
          server_name aaaa.bbbbb.com;

          location ^~ / {
          proxy_pass http://aaaa.bbbbb.com:9100;
          }

     }
     
     
     
### 指向某個位置
     server {
          listen 80;
          server_name aaaa.bbbbb.com;

          location / {
               root /home/test/;
          }

     }
     


### 在本地3306建立一個服務 實際上是導到外面的mysql
     stream {
         server {
             listen 3306;
             proxy_pass 192.168.0.1:3306;
         }
     }
     
     
     
### nginx 301導向
     location / {
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
		
        return 301 http://127.0.0.1$request_uri;
      }


### wss ws 同 port
https://www.nginx.com/blog/running-non-ssl-protocols-over-ssl-port-nginx-1-15-2/

	stream {
	    upstream wss {
		server 127.0.0.1:9997;
	    }

	    upstream ws {
		server 127.0.0.1:9998;
	    }

	    map $ssl_preread_protocol $upstream {
		default wss;
		"" ws;
	    }

	    server {
		listen 9999;
		proxy_pass $upstream;
		ssl_preread on;
	    }
	}
     
