# Steps taken for HW1 
creating our lil-napkin server

## Setting up Apache and Nginx
1. SSH into our droplet and install the servers.
2. Set up the firewall with permission to use port 8081 and 8082.
3. For Apache to listen on a different port, edit the config file and the ports config file
    - edit the /etc/apache2/ports.conf with Listen 8081
    - edit /etc/apache2/sites-enabled/lil-napkin.config with <VirtualHost *:8081>
4. For Nginx to listen on 8082 edit /etc/nginx/sites-enabled/default with server { listen 8082; ...}
  - [ngix source](https://stackoverflow.com/questions/10829402/how-to-start-nginx-via-different-portother-than-80)

## Employ password protection
1. Create a passwords file using the apache2-utils
   - For this use command:
    `sudo htpasswd -c /etc/nginx/.htpasswd alex`
     - This creates a the file and saves the user alex and asks for the password to be used
     - Replace nginx with apache2 for the other server
2. Create a custom sites-available file for your site's configuration for *apache*
   - `vim /etc/apache2/sites-available/lil-napkin.conf`
   - `a2ensite lil-napkin.conf`
   - add lines to this for password authentication
   - For *nginx* edit the default sites-enabled file with code for authentication
   
## Have a static team page that indicates your name and/or team members, emails, etc.
1. For Apache and Nginx the html file is located at `/var/www/html/index.html`
    - create your team page here and add more files to build the website
    - link a css page for styling
    
## Use custom error pages
1. Write the html pages used for 404 and 403 errors which can be placed inside `/var/www/html`
2. For Apache link these pages to be used for these errors in `/etc/apache2/sites-enabled/lil-napkin.config`
3. For Nginx link these pages to be used for these errors in `/etc/nginx/sites-enabled/default`

## Have a favicon
1. Place in the head tags of the index.html and other html pages for the site

## Have a robots.txt file

## Deploy from Github
1. Create a user for the server with sudo privileges and make them a directory `sudo mkdir /var/www/.ssh`
2. SSH to that user and generate an ssh public key
  - `sudo -Hu user ssh-keygen -t rsa`
    - this command generates the key pair and the public key is found at `/var/www/.ssh/id_rsa.pub`
3. On github set up a repo and create a php script that will perform git pulls for your website
4. Add the ssh public key from the user of your droplet to github and set up service hook
 - [source](https://gist.github.com/oodavid/1809044)

## Log Properly
1. Install GoAccess and follow the tutorial to set it up
2. We chose the `Combined Log Format`
3. GoAccess created a dashboard for us to see the various stats from our website
   - we can see our unique visitors per day, amount of valid/total requests, static requests sorted by hits, our sites visitors and IPs, etc..
   - this dashboard is visible at http://104.248.219.235:8082/report.html
  - [source](https://goaccess.io/get-started)

## Compress Textual Content

## Obscure server identity

## Run PHP

## Deliver Clean URLS

