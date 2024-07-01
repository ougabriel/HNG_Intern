###Stage Zero - HNG Task (Static Website Deployment)

Deploying a static website on Azure using NGINX involves similar steps to those for AWS. Below is a detailed guide I used in order to help you set up your static website on Azure:

### Step-by-Step Guide for Static Website Deployment on Azure

#### Prerequisites:
1. **Azure Account**: Ensure you have an active Azure account.
2. **Static Website Files**: Prepare your static website (HTML, CSS, Javascript). Ensure it includes your name, username, and email.
3. **SSH Client**: Install an SSH client (e.g., PuTTY for Windows, Terminal for macOS/Linux).

### Step 1: Create an Azure Virtual Machine

1. **Login to Azure Portal**:
   - Go to the [Azure Portal](https://portal.azure.com/).
   - Sign in with your Azure account.

2. **Create a New Virtual Machine**:
   - Navigate to "Virtual machines" and click "Create".
   - Select "Azure Virtual Machine" and choose your subscription and resource group.
   - Fill in the instance details:
     - **Image**: Ubuntu Server 20.04 LTS
     - **Size**: Standard B1s (suitable for testing, adjust based on your needs)
     - **Authentication type**: SSH public key
     - **Username**: Choose a username
     - **SSH public key**: Paste your SSH public key

3. **Configure Networking**:
   - Under "Networking", ensure that the "Inbound port rules" allow HTTP (port 80) and SSH (port 22).

4. **Review and Create**:
   - Review the settings and click "Create". Wait for the deployment to complete.

### Step 2: Connect to Your Azure Virtual Machine

1. **Connect via SSH**:
   - Open your terminal (or PuTTY on Windows).
   - Connect to your instance using SSH:
     ```sh
     ssh -i "path-to-your-private-key" username@your-vm-public-ip
     ```

### Step 3: Install NGINX on Your Azure Virtual Machine

1. **Update Packages**:
   ```sh
   sudo apt update -y
   ```

2. **Install NGINX**:
   ```sh
   sudo apt install nginx -y
   ```

3. **Start NGINX**:
   ```sh
   sudo systemctl start nginx
   ```

4. **Enable NGINX to Start on Boot**:
   ```sh
   sudo systemctl enable nginx
   ```

### Step 4: Upload Your Static Website Files

1. **Create a Directory for Your Website**:
   ```sh
   sudo mkdir -p /var/www/html/your-website
   ```

2. **Copy Your Static Files to the Directory**:
   - You can use SCP (secure copy) to upload files from your local machine to the VM:
     ```sh
     scp -i "path-to-your-private-key" -r /path/to/your/static/files/* username@your-vm-public-ip:/var/www/html/your-website
     ```

### Step 5: Configure NGINX to Serve Your Website

1. **Edit the NGINX Configuration File**:
   ```sh
   sudo nano /etc/nginx/sites-available/default
   ```
   - Modify the configuration to point to your website directory:
     ```nginx
     server {
         listen 80 default_server;
         listen [::]:80 default_server;

         root /var/www/html/your-website;
         index index.html index.htm;

         server_name _;

         location / {
             try_files $uri $uri/ =404;
         }
     }
     ```

2. **Test the NGINX Configuration**:
   ```sh
   sudo nginx -t
   ```

3. **Reload NGINX**:
   ```sh
   sudo systemctl reload nginx
   ```

### Step 6: Verify Your Website Deployment

1. **Access Your Website**:
   - Open your web browser and navigate to `http://your-vm-public-ip`.
   - Ensure your static website loads correctly.

### Step 7: Submission

1. **Double-Check Requirements**:
   - Ensure your website includes your name, username, email, and mentions HNG Internship.
   - Include a link to https://hng.tech.

2. **Submit the Task**:
   - Fill out the submission form with the required details.
   - Provide the public IP address of your deployed website.

### Example of the Static Website HTML

Here’s a simple example of what your `index.html` could look like:

```html
xheck repo to the see the code
```

By following these steps, you should be able to successfully deploy your static website on an Azure VM using NGINX, and meet all the requirements of the task.

###The END.