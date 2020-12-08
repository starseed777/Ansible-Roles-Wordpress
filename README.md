This is full documentation of debugging our ansible roles, links used for solution:
- https://www.wpbeginner.com/beginners-guide/how-to-edit-wp-config-php-file-in-wordpress/
- https://dotlayer.com/how-to-use-an-ansible-playbook-to-install-wordpress/

- first I went into apache-setup/defaults/main.yml and changed our custom_port to 80 
- I then ran apache-playbook.yml so that our apache2 service will be running on port 80 because wordpress uses this port
- Next I went into the roles directory and changed the playbook.yml by adding "become: true" + deleting the python2 install task
- The reason I deleted the task is because our ubuntu target server already has python3 installed and when doing this the playbook sucessfully passes
- I then ran the playbook.yml in the cli with this command: ansible-playbook playbook.yml -u ansadmin -K (this prompts for password after)
- The playbook passes
- I then manually go into the ubuntu target server and cd into /var/www/wordpress and edit wp-config.php and add the database credentials because it threw a db connection error
- Next I re run the playbook.yml and refresh the page in my browser that has the ubuntu public ip and wordpress index page is there

Exit criteria met - refer to screenshots
