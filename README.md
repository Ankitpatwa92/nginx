# nginx
How to install nginx on centos


### Download package form here =>
http://nginx.org/en/download.html


### Step2 

./configure --with-http_ssl_module 

#### Step 3
make install

#### Step4 
sudo vim /etc/ld.so.conf

Add following entry
/usr/local/lib64


#### Edit nginx config

    server {
         listen 444 ssl;
		 listen 8097;
         server_name  localhost;

		 ssl_protocols TLSv1.2 TLSv1.3;
		 
         ssl_certificate      D:/Tools/nginx-1.16.0/conf/certChain.pem;
         ssl_certificate_key  D:/Tools/nginx-1.16.0/conf/key.pem;

        ssl_session_cache    shared:SSL:1m;
        ssl_session_timeout  5m;

        ssl_ciphers  HIGH:!aNULL:!MD5;
        ssl_prefer_server_ciphers  on;


        location / {
            root   html;
            index  index.html index.htm;
			auth_basic   "Private Property";
            auth_basic_user_file   D:/Tools/nginx-1.16.0/conf/htpasswd;
            proxy_pass http://localhost:9200;
        }
    }


##### Step 6 Start nginx
./nginx


#### Step 7 create username  password file
sudo htpasswd -c /etc/nginx/.htpasswd sammy


//centos location /usr/local/nginx/conf
