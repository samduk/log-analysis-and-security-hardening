# log-analysis-and-security-hardening
Organized by Envision (https://www.empoweringvision.org/)



# Day 01: Training


	 1. Download Resources  
		[link](http://tcert.net/wp-content/uploads/lab.ova)

	 2. How to install extenion in virtualbox (virtualbox.org)

	 3. How to import virtual appliance
				NAT internet  
				bridget internet

				host-only no internet


	Terminal
		ssh username@serverIP
		ssh researcher@192.168.56.100

	 4. How to setup NAT and Host only Adapters


	 5. How to connect server using SSH (or PUTTY for window)


### Connect to the server

			ssh username@serverIP

			eg researcher@192.168.56.100

			[putty](https://www.putty.org/)


	 6. Preview of live log on Notepad (or any editor)

Example of different logs:

	- error.log (very useful for developer)
  - kern.log
  - mysql.log
  - sys.log
  - auth.log  
	-	access.log (our focus)

Example of few web servers that commonly used in Tibetan Community:

		apache2
		nginx
		litespeed  


	 7. Some useful commands

			how to extract the .gz file?

				gunzip -k file.gz

			 ls : Display the list of files and directories in the current folder
		   cat : prints the content of a file in Terminal Window
			 grep: searches and filters based on patterns
			 awk: cant sort each row into fields and display only what is needed

					awk -F'[ ]' '{print $1}' soyala.net-May-2020
					awk -F'[ ]' '{print $1 "\t" $7}' soyala.net-May-2020
					[more link1](https://www.shellhacks.com/awk-print-column-change-field-separator-linux-bash/) <br>
					[more link2](https://stackoverflow.com/questions/12204192/using-multiple-delimiters-in-awk)<br>

			 sed: performs find and replace functions

				 sed -i 's/old-text/new-text/g' input.txt

			 sort: arranges output into order
			 uniq: compares adjacent lines and can report, filter or provide a count of duplicates
			 wc: word count (c,l)
			 head:
			 tail:


	 8. Log Analysis using commands


	 9. How to trace an IP address ?


			 yum install geoip


		 	 geoiplookup 99.106.76.40


	Class work:

		wget https://mirrors-cdn.liferay.com/geolite.maxmind.com/download/geoip/database/GeoLiteCity.dat.xz

			xz --decompress GeoLiteCity.dat.xz
			sudo mv GeoLiteCity.dat /usr/share/GeoIP/



			geoiplookup -f /usr/share/GeoIP/GeoLiteCity.dat 80.153.137.92

	[resource](https://mirrors-cdn.liferay.com/geolite.maxmind.com/download/geoip/database/)


			Question1. Which country this IP address belong ?
			Question2: City?
			Question3: Longittute and Latitude ?



	 10. Let us build a simple tool to automate our work.


## Program and save it has tool.sh


\#!/bin/bash


	geoiplookup -f /usr/share/GeoIP/GeoLiteCity.dat $1 | cut -d " " -f4-11 | cut -d "," -f1-6;
	geoiplookup $1 | cut -d " " -f5





# Day 02:

## Block bad people

1. Summary of what we did yesterday

2. How to block the culprit? (using firewalld or iptables)

		<br />
	-> How to block people by IP <br />
	-> How to block people by port (or particular services) (assignment)<br />
	-> How to unblock people by IP<br />
	-> How to unblock people by port (or delete the RULE)  (assignment)<br />

For Reading: <br >
	[Resource 1](https://www.hostingswift.com/how-to-block-or-unblock-an-ip-address-on-a-linux-server) <br>
	[Resource 2](https://www.e2enetworks.com/help/knowledge-base/how-to-block-ip-address-on-linux-server/)<br>
	[Resource 3](https://www.cyberciti.biz/faq/how-do-i-block-an-ip-on-my-linux-server/) <br>



3. How to automate it using fail2ban ?

# Hardening:

	MySQL Hardening
		1. Drop the Test database
		2. Remove all anonymous accounts
		3. Change default port mappings
		4. Alter which hosts have access to MySQL
		5. Do not run MySQL with root level privileges
		6. Remove and disable the MySQL history file
		7. Disable remote logins
		8. Limit or disable SHOW DATABASES
		9. Disable the use of LOAD DATA LOCAL INFILE command
		10. Obfuscate the root account
		11. Set the proper file permissions



		Demo:   mysql_secure_installation (command)

	PHP version:
		Demo

	Server:
		Demo

	Force HTTPS:
		RewriteEngine On
		RewriteCond %{HTTPS} !=on
		RewriteRule ^(.\*)$ https://%{HTTP_HOST}%{REQUEST_URI} [L,R=301,NE]


	WordPress: Security Check Lists

<br>
	[sFTP 1](https://help.one.com/hc/en-us/articles/115005585709-How-do-I-connect-to-an-SFTP-server-with-FileZilla-) <br>
	[sFTP 2](https://www.liquidweb.com/kb/using-sftp-and-scp-instead-of-ftp/)


# Introduct a Game to improve command line skill

	* [bandit](https://overthewire.org/wargames/bandit/) <br>

		-> If you can't solve the game, few walk-through is available [here](https://github.com/samduk/bandit)	
