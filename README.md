🧩 1. Launch an Amazon Linux EC2 Instance
Log in to AWS Console → EC2 → Launch Instance

Choose Amazon Linux 2 AMI (free tier eligible).

Select instance type: t2.micro (for testing).

Create or use an existing key pair.

Allow inbound traffic:

HTTP (80)

HTTPS (443)

Custom TCP 3000 (optional, for testing)

SSH (22)

Launch the instance.

🧠 2. Connect to Your Server
In your terminal:

ssh -i "your-key.pem" ec2-user@<public-ip>
⚙️ 3. Update the System
sudo yum update -y
🟢 4. Install Node.js and npm
Amazon Linux 2 comes with Node.js in repositories:

sudo yum install -y nodejs npm
✅ Check versions:

node -v
npm -v
If you need the latest version:

curl -fsSL https://rpm.nodesource.com/setup_20.x | sudo bash -
sudo yum install -y nodejs
📦 5. Clone Your Project from GitHub
If your code is on GitHub:

sudo yum install -y git
git clone https://github.com/<your-username>/<your-repo>.git
cd <your-repo>
📁 6. Install Project Dependencies
Inside your project directory:

npm install
▶️ 7. Run Your App
For testing:

node app.js
If your app runs on port 3000, open:

http://<ec2-public-ip>:3000
⚡ 8. Use PM2 for Continuous Running
Install PM2 (process manager):

sudo npm install -g pm2
Start your app:

pm2 start app.js
pm2 status
pm2 startup
pm2 save
This ensures your Node app restarts automatically after a reboot.

🌐 9. Set Up Nginx as a Reverse Proxy
Install Nginx:

sudo amazon-linux-extras install nginx1 -y
Edit config:

sudo nano /etc/nginx/nginx.conf
Replace the server block with:

server {
    listen 80;
    server_name _;

    location / {
        proxy_pass http://127.0.0.1:3000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
}
Restart Nginx:

sudo systemctl enable nginx
sudo systemctl restart nginx
Now your app is live on:

http://<ec2-public-ip>/
🔒 10. (Optional) Enable SSL using Certbot
If you have a domain:

sudo amazon-linux-extras install epel -y
sudo yum install certbot python3-certbot-nginx -y
sudo certbot --nginx
✅ Your Node.js App is Now Live!

--------------------------------
Author:-
   Avinash D Zalke
   Linkedin: https://www.linkedin.com/in/
   Email:avinashzalake2@gmail.com



No file chosenNo file chosen
ChatGPT can make mistakes. Check important info. See .
