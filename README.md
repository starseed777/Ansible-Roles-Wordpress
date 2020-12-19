This is full documentation of debugging our ansible roles, links used for solution:
- https://www.wpbeginner.com/beginners-guide/how-to-edit-wp-config-php-file-in-wordpress/
- https://dotlayer.com/how-to-use-an-ansible-playbook-to-install-wordpress/
- https://docs.ansible.com/ansible/2.5/modules/copy_module.html

- first I went into apache-setup/defaults/main.yml and changed our custom_port to 80
 
- I then ran apache-playbook.yml so that our apache2 service will be running on port 80 because wordpress uses this port

- Next I went into the roles directory and changed the playbook.yml by adding "become: true" + deleting the python2 install task

- The reason I deleted the task is because our ubuntu target server already has python3 installed and when doing this the playbook sucessfully passes

- I then ran the playbook.yml in the cli with this command: ansible-playbook playbook.yml -u ansadmin -K (this prompts for password after)

- The playbook passes

- Wordpress loads but throws a db connection error (solution coming together slowly!)

- I then manually go into the ubuntu target server and cd into /var/www/wordpress and edit wp-config.php and add the database credentials because it threw a db connection error
- Next I refresh the page in my browser that has the ubuntu public ip and wordpress index page is there after MANUALLY adding the credentials but we're devops man screw manualintervention!!!

- I took the existing wp-config.php file and thought hmm what if we just copied this file from the controller to target servers so this can be automated

- So after creating a replica of that config file in the controller server I decided to tweak the playbook by using the ansible copy module - refer to the playbook + screenshots to see 

- Now time to test does this automatically load up wordpress with no manual intervention involved? 

- I made another debian target server and ran the playbook and voila no db connection error, playbook passes, wordpress index sucessfully loads!!! :)

Exit criteria met - refer to screenshots
