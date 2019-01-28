# Steps taken for HW1 
creating our lil-napkin server

## Setting up Apache and Nginx
1. SSH into our droplet and install the servers.
2. Set up the firewall with permission to use port 8081 and 8082.
3. For Apache to listen on a different port, edit the config file and the ports config file
    - edit the /etc/apache2/ports.conf with Listen 8081
    - edit /etc/apache2/sites-enabled/lil-napkin.config with <VirtualHost *:8081>
4. For Nginx to listen on 8082 edit /etc/nginx/sites-enabled/default with server { listen 8082; ...}

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
