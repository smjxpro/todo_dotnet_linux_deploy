# Todo.NET

### This is an example ASP.NET project deployment on Linux VPS using postgres, nginx.

**1. `Local:` Clone the repo**

**2. `Local:` Install DotNet SDK**

**3. `Local:` Prepare the project for publishing**

`dotnet publish -c release`

**4`Local:` Upload the content of `TodoApi/bin/release/net6.0/publish` into the server's `/var/www/todoapi` directory**

**5`Server:` Update the `appsettings.Production.json` file to the right connection string**

**6`Server:` Update the database by running SQL commands from the file `Deployment/postgres.sql` file**

**7. `Server:` Install dotnet-sdk using snap**

`sudo snap install dotnet-sdk --classic`

**8`Server:` Create a systemd service**

`sudo nano /etc/systemd/system/todoapi.service` 

and replace its content with `Deployment/todoapi.service` and update the user

**9 `Server:` Enable the service**

`sudo systemctl enable todoapi.service`

**10. `Server:` Start the service**

`sudo systemctl start todoapi.service`

**11. `Server:` Check the status of the service**

`sudo systemctl status todoapi.ervice`

**12. `Server:` Create a nginx configuration for virtual host**

`sudo nano /etc/nginx/sites-available/todoapi` 

and replace its content with `Deployment/todoapi-nginx.conf` and update the domains

**13. `Server:` Create a symlink of the newly created nginx virtual host configuration file**

`sudo ln -S /etc/nginx/sites-available/todoapi /etc/nginx/sites-enabled/todoapi`

**14. `Server:` Test the nginx configuration**

`sudo nginx -t`

**15. `Server:` Restart nginx**

`sudo systemctl restart nginx`

**16. `Local:` Test the api url: `your-domain/api/todo-items`**
