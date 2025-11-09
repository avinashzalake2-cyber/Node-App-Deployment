🟢 Node.js Application Deployment using AWS EC2 & Nginx

🚀 Project Overview:
This project demonstrates how to deploy a Node.js web application on an AWS EC2 instance. It covers end-to-end steps from local development to live deployment with continuous availability.

🧩 Key Steps Involved:

Developed and tested the Node.js app locally.

Launched an EC2 instance (Ubuntu Server).

Installed Node.js, npm, and Git on the server.

Cloned the project repository using Git.

Installed all dependencies using npm install.

Used PM2 to keep the app running continuously.

Configured Nginx as a reverse proxy for better performance and security.

Accessed the app using a custom domain and public IP.

🛠️ Tech Stack:

Node.js

Express.js

AWS EC2

PM2

Nginx
3. Launch a Server (e.g., AWS EC2)

Choose Ubuntu instance.

Connect via SSH:

ssh -i key.pem ubuntu@<your-public-ip>


Update packages:

sudo apt update && sudo apt upgrade -y

4. Install Node.js, npm, and Git
sudo apt install nodejs npm git -y


Check versions:

node -v
npm -v

5. Clone Your GitHub Repository
git clone https://github.com/<username>/<repo-name>.git
cd <repo-name>

6. Install Dependencies
npm install

7. Run the App
node app.js


or

npm start


Check in the browser:
http://<your-server-public-ip>:<port>

8. Keep App Running (Using PM2)
sudo npm install -g pm2
pm2 start app.js
pm2 startup
pm2 save


This ensures the app restarts automatically if the server reboots.

9. (Optional) Set Up Nginx Reverse Proxy

To serve your app on port 80 (default HTTP port):

sudo apt install nginx -y
sudo nano /etc/nginx/sites-available/default


Replace content with:

server {
    listen 80;
    server_name _;

    location / {
        proxy_pass http://localhost:3000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
}


Then restart Nginx:

sudo systemctl restart nginx

✅ Now your Node.js app is live!

You can access it using your server IP or domain name.
✅ Deployment Complete!

Your Node.js app is now live and accessible via your server IP or domain name 🎉

💡 Author

Avinash D Zalke

GitHub: @avinash dhanraj zalke
Linkedin: https://www.linkedin.com/
email-ID: avinashzalake2@gmail.com
