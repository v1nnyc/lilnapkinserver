# Steps taken for HW1 
creating our lil-napkin server

## Setting up Apache and Nginx
1. SSH into our droplet and install the servers.
    - [nginx source](https://www.digitalocean.com/community/tutorials/how-to-install-nginx-on-ubuntu-16-04)
    - [apache source](https://www.digitalocean.com/community/tutorials/how-to-install-the-apache-web-server-on-ubuntu-16-04)
2. Set up the firewall with permission to use port 8081 and 8082.
3. For Apache to listen on a different port, edit the config file and the ports config file
    - edit the /etc/apache2/ports.conf with Listen 8081
    - edit /etc/apache2/sites-enabled/lil-napkin.config with <VirtualHost *:8081>
4. For Nginx to listen on 8082 edit /etc/nginx/sites-enabled/default with server { listen 8082; ...}
   - [nginx source](https://stackoverflow.com/questions/10829402/how-to-start-nginx-via-different-portother-than-80)

## Employ password protection
1. Create a passwords file using the apache2-utils
   - For this use command:
    `sudo htpasswd -c /etc/nginx/.htpasswd alex`
     - This creates a the file and saves the user alex and asks for the password to be used
     - Replace nginx with apache2 for the other server
2. Create a custom sites-available file for your site's configuration for **Apache**
   - `vim /etc/apache2/sites-available/lil-napkin.conf`
   - `a2ensite lil-napkin.conf`
   - add lines to this for password authentication
   - For **Nginx** edit the default sites-enabled file with code for authentication
   - [apache source](https://www.digitalocean.com/community/tutorials/how-to-set-up-password-authentication-with-apache-on-ubuntu-14-04)
   - [nginx source](https://www.digitalocean.com/community/tutorials/how-to-set-up-password-authentication-with-nginx-on-ubuntu-14-04)
   
## Have a static team page that indicates your name and/or team members, emails, etc.
1. For Apache and Nginx the html file is located at `/var/www/html/index.html`
    - create your team page here and add more files to build the website
    - link a css page for styling
    
## Use custom error pages
1. Write the html pages used for 404 and 403 errors which can be placed inside `/var/www/html`
2. For Apache link these pages to be used for these errors in `/etc/apache2/sites-enabled/lil-napkin.config`
3. For Nginx link these pages to be used for these errors in `/etc/nginx/sites-enabled/default`
  - [source](https://www.digitalocean.com/community/tutorials/how-to-configure-nginx-to-use-custom-error-pages-on-ubuntu-14-04)

## Have a favicon
1. Create a directory of all favicon icons
2. Used an online favicon converter to change images to icons
3. Linked to the directory in the head tags of the index.html and other html pages for the site
  - [converter](https://www.favicon-generator.org/)

## Have a robots.txt file
1. Used a robots.txt generator to create the file
2. Put the file in the root directory
  - [generator](http://tools.seobook.com/robots-txt/generator/)

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
 1. For **Apache** this is configured using mod_deflate which was already set up by default
 2. For **Nginx** this is automatically configured with gzip 

## Obscure server identity
 1. For **Apache** we installed a mod to change but not remove the server header
 2. Change the header to something confusing
    - [source](https://www.tecmint.com/change-apache-server-name-to-anything-in-server-headers/)
 3. For **Nginx** we installed nginx extras
 4. Then we changed the nginx config file and turned off server tokens and set the headers
    - [source](https://stackoverflow.com/questions/246227/how-do-you-change-the-server-header-returned-by-nginx)

## Run PHP
 1.Change the config files 
 2.For **Apache** we downloaded an extra package to help it run

## Deliver Clean URLS
 1. For **Apache** in the file `/etc/apache2/sites-enabled/lil-napkin.config` we turned the rewrite engine on and created a rule to hide the .php
 [source](https://support.hostgator.com/articles/apache-mod_rewrite-and-examples)
 2. For **Nginx** in the config file, `/etc/nginx/sites-enabled/default` we added a rewrite line to hide the .php
 [source](https://www.codesmite.com/article/clean-url-rewrites-using-nginx)

