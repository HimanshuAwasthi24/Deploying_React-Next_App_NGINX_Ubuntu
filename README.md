# Deploying_React-Next_App_NGINX_Ubuntu
Deploying ReactJs/NextJs on VM Intances using NGINX on Linux
=======
# Getting Started with Create React App

This project was bootstrapped with [Create React App](https://github.com/facebook/create-react-app).

Clone This Repo [Github](https://github.com/HimanshuAwasthi24/Deploying_React-Next_App_NGINX_Ubuntu.git)

## Make sure you have node and npm installed on your system

1) ### `git clone Gitub_Repo_URL`

2) ### `cd project_directory`

3) ### `npm install`

4) ### `npm run build`

5) ### `sudo mv project_directory /var/www/`

6) ### `cd /etc/nginx/sites-available`

7) creating virtual host 
    ### `vim filename.conf`


server {
        listen 80;
        server_name domain_name.com www.domain_name.com; # !!! - change to your domain name 
      gzip on;
        gzip_proxied any;
        gzip_types application/javascript application/x-javascript text/css text/javascript;
        gzip_comp_level 5;
        gzip_buffers 16 8k;
        gzip_min_length 256;

    location /_next/static/ {
                alias /var/www/yourProject/build; # !!! - change to your app name
                expires 365d;
                access_log off;
        }

    location / {
                proxy_pass http://127.0.0.1:3000; # !!! - change to your app port
                proxy_http_version 1.1;
                proxy_set_header Upgrade $http_upgrade;
                proxy_set_header Connection 'upgrade';
                proxy_set_header Host $host;
                proxy_cache_bypass $http_upgrade;
        }
}

8) ### `sudo ln -s /etc/nginx/site-available/filename.conf /etc/nginx/sites-enabled/` 

9) ### `cd ../..`

hostname alias creation
10) ### `vim hosts`
     ### 127.0.0.1          your_domain

11) ### `npm install pm2 -g`

12) ### `cd /var/www/your_project`
    ### `pm2 start npm --name "project_name" -- start `
![Screenshot from 2023-11-23 13-06-09](https://github.com/HimanshuAwasthi24/Deploying_React-Next_App_NGINX_Ubuntu/assets/83570704/c48564b6-1caf-4e95-8de3-503177b5e49d)

13) hit your domain_name on browser you should be able see the UI of your app

14) ![Screenshot from 2023-11-23 13-05-40](https://github.com/HimanshuAwasthi24/Deploying_React-Next_App_NGINX_Ubuntu/assets/83570704/161d3782-30ad-485b-a091-a842fd2a391f)







