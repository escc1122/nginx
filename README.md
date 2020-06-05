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
     
