# How to Install GoAccess on Fedora/RedHat/CentOS 

### System Update
<code>
sudo yum -y install epel-release
sudo yum -y update
sudo shutdown -r now
</code>

### Install Dependencies 

<code>
sudo yum -y install ncurses-devel gcc
sudo yum -y install geoip-devel 
</code>

### Install GoAccess 
<code>
wget http://tar.goaccess.io/goaccess-1.2.tar.gz
tar -xzvf goaccess-1.2.tar.gz

cd goaccess-1.2
sudo ./configure --enable-utf8 --enable-geoip=legacy
sudo make
sudo make install
</code>

#### creating softlink 
<code>
sudo ln -s /usr/local/bin/goaccess /usr/bin/goaccess
</code>

### Using GoAccess 

sudo goaccess /var/log/access.log --log-format=COMBINED


#### To generate HTML report 

<code>sudo goaccess /var/log/httpd/access_log --log-format=COMBINED -a -o /var/www/html/report.html </code>

### Bibliography
[official Resource](https://goaccess.io/download) <br>
[Resource1](https://www.vultr.com/docs/how-to-install-goaccess-on-centos-7) <br >
[Resource2](https://www.youtube.com/watch?v=RY6kK1iwTb8) <br>


# Connect to the server 

ssh username@serverIP 

eg researcher@192.168.56.100 

putty 


# Some useful commands

how to extract the .gz file? 
	gunzip -k file.gz 

- ls : Display the list of files and directories in the current folder
- cat : prints the content of a file in Terminal Window 
- grep: searches and filters based on patterns
- awk: cant sort each row into fields and display only what is needed 
	awk -F'[ ]' '{print $1}' soyala.net-May-2020
	awk -F'[ ]' '{print $1 "\t" $7}' soyala.net-May-2020
	[more link1](https://www.shellhacks.com/awk-print-column-change-field-separator-linux-bash/) <br>
	[more link2](https://stackoverflow.com/questions/12204192/using-multiple-delimiters-in-awk)<br>
- sed: performs find and replace functions 
	- sed -i 's/old-text/new-text/g' input.txt
- sort: arranges output into order
- uniq: compares adjacent lines and can report, filter or provide a count of duplicates 
- wc: word count (c,l)
- head: 
- tail: 






Developer: 
	error.log  dmesg mail 
	access.log 

servers: 
	apache2 
	nginx 
	litespeed  



# Let us build a simple tool to automate our work.

geoiplookup -f /usr/share/GeoIP/GeoLiteCity.dat 80.153.137.92 | cut -d " " -f4-12 | cut -d "," -f1-7;
geoiplookup 80.153.137.92 | cut -d " " -f5   
















