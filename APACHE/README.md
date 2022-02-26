
# APACHE INSTALLATION AND SITE CONFIGURATION - WINDOWS 10
- Apache version used in this tutorial: 2.4.52


## Table of Contents
1. [DOWNLOAD THE FILES](#download-the-files)
1. [INSTALL](#install)
3. [START THE SERVICE](#start-the-service)


---

## DOWNLOAD THE FILES


1. From [Apache VS16 binaries and modules](https://www.apachelounge.com/download/) download (apachelounge.com) download latest version of Apache x.x.X Win64 (For this tutorial we are going to use the 2.4.52 version).
- ![download](/images/apache/apache_1.png)

2. Once the download is done go to the Downloads folder, extract the files and copy the Apache24 folder to c:/Apache24

---

## INSTALL


1. Open the Command Prompt as administrator
- ![download](/images/apache/apache_2.png)

2. In the command prompt go to the Bin folder by typing: `cd c:\Apache24\Bin`
- ![download](/images/apache/apache_3.png)
3. Once in the Bin folder, type: `httpd.exe -k install`
- ![download](/images/apache/apache_4.png)
4. After the installation is done the command prompt should look like this:
- ![download](/images/apache/apache_5.png)

---

## START THE SERVICE


1. In the windows search bar type services.msc and press enter.
- ![download](/images/apache/apache_6.png)
    
    - The following screen should open:
    - ![download](/images/apache/apache_7.png)
3. Locate the Apache2.4 service and right click over it, choose start.
- ![download](/images/apache/apache_8.png)
4. If the service started correctly it should read “Running” under the status column.
- ![download](/images/apache/apache_9.png)
5. To test Apache open a web browser of your choice and go to `http://localhost`.  The following default page should be shown:
- ![download](/images/apache/apache_10.png)
---

## CONFIGURE 2 SITES
Now that Apache is running lets configure 2 sites, the names of the sites can be anything you want, but for this tutorial we are going to create the sites mysite.jr and mysecondsite.jr

1. In the file explorer Go to `C:\Apache24\conf` and open the file httpd.conf
2. In that file find the text `# Include conf/extra/httpd-vhosts.conf`.  Erase the # to uncomment the line.  Save your changes.  We do this so that the server looks for additional configurations on the httpd-vhosts.conf file.
- ![download](/images/apache/apache_11.png)
3. Now go to `C:\Apache24\conf\extra` and open the file httpd-vhosts
4. At the end of the file add the following bindings.  We are specifying that we want to add the sites under port 80, with an specific ServerName(mysite.jr and mysecondsite.jr) and the specified folder where the files of each site will be placed (Apache24/htdocs/mysite.jr and Apache24/htdocs/mysecondsite.jr).  To add the bindigs copy and paste the following:

    ```
    <VirtualHost *:80>
            <br> ServerName mysite.jr
            DocumentRoot "${SRVROOT}/htdocs/mysite.jr"
        </VirtualHost>

    <VirtualHost *:80>
        ServerName mysecondsite.jr
        DocumentRoot "${SRVROOT}/htdocs/mysecondsite.jr"
    </VirtualHost>`
    ```

    Afterwards the end of the file should look as follows, save the changes.

- ![download](/images/apache/apache_12.png)
5. Now we are going to modify our hosts file so that the browser knows what IP to look for when it tries to find our sites.  In this case it will be directed to localhost.  In order to do that lets open Notepad as an administrator.
- ![download](/images/apache/apache_13.png)
6. In Notepad lets go to the menu File->Open and lets navigate to the Path `C:\Windows\System32\drivers\etc` and select the option All Files in the dropdown located in the bottom right corner of the current window.
- ![download](/images/apache/apache_14.png)
7. Choose the file hosts and click open.
8. Lets add the following lines at the end of the file and save our changes.
```
127.0.0.1       mysite.jr
127.0.0.1       mysecondsite.jr
```
9. Next we have to create the folders were our sites files are going to be placed as specified in the httpd-vhosts file.  Lets navigate to `C:\Apache24` and create the folders for our sites.
- ![download](/images/apache/apache_16.png)
10. In order to test our sites lets create an index.html file in each of the 2 folders we created.  
- ![download](/images/apache/apache_17.png)
11. The html files can have the text of our choice inside.  We do this in each html file, the screen shots only show the procedure for mysite.jr.
- ![download](/images/apache/apache_18.png)
12. Now that everything is set up lets restart our server in order to see the final result.
- ![download](/images/apache/apache_19.png)
13. Once the server is restarted open your web browser and navigate to your sites.
- ![download](/images/apache/apache_20.png)
- ![download](/images/apache/apache_21.png)
---
## DISABLE DIRECTORY LISTENING
Finally lets disable directory listing because at the moment it is enabled.  We can verify it is enabled by changing the name of any od the index.html files and going to the corresponding site in the browser.
- ![download](/images/apache/apache_22.png)

1. Open the httpd.conf file under C:\Apache24\conf
2. Find the line with “Options Indexes FollowSymLinks”
3. Change that line to “Options FollowSymLinks”
- ![download](/images/apache/apache_23.png)
4. Restart Apache and browse to the site to verify directory listing is disabled.
- ![download](/images/apache/apache_24.png)
---
## CREATE A CERTIFICATE AND CONFIGURE SSL IN ONE OF THE SITES
1. Navigate to `c:\Apache24\conf`, copy the openssl.cnf file.
2. Paste the file in `c:\Apache24\bin`
- ![download](/images/apache/apache_25.png)
3. Open the command prompt as administrator and type `cd c:\Apache24\bin` to go to the bin folder.
4. Once there type te following command.
```
openssl req -config openssl.cnf -new -out htv.csr -keyout htv.pem
```
5. Enter the required information
    - ![download](/images/apache/apache_26.png)
    - This 2 files should be created (you can use the names you wish)
    - ![download](/images/apache/apache_27.png)
6. Type the following command in the command prompt.
```
openssl rsa -in htv.pem -out htv.key
```
7. Type the following command
```
openssl x509 -in htv.csr -out htv.crt -req -signkey htv.key -days 900
```
- ![download](/images/apache/apache_37.png)
8. The following files should appear:
- ![download](/images/apache/apache_28.png)
9.  Move the created files to the conf folder
- ![download](/images/apache/apache_29.png)
10. Open the httpd.conf file and uncomment the LoadModule line by deleting the # symbol.
- ![download](/images/apache/apache_30.png)
11. Go to the extra folder and open the file httpd-vhosts.conf file and add `Listen 443` so that the server listens to the 443 port.
- ![download](/images/apache/apache_31.png)
12. Add the following code to the end of the file to include ssl in the site.
```
<VirtualHost *:443>
    ServerName mysecondsite.jr
    DocumentRoot "${SRVROOT}/htdocs/mysecondsite.jr"
    SSLEngine on
    SSLCertificateFile "C:\Apache24\conf\htv.crt"
    SSLCertificateKeyFile "C:\Apache24\conf\htv.key"
</VirtualHost>
```
- ![download](/images/apache/apache_32.png)
13. In order for the server to redirect port 80 to port 443 include the following code in the port 80 configuration section.
```
Redirect permanent / https://mysecondsite.jr
```
- ![download](/images/apache/apache_33.png)
14. Restart Apache
15. Test your site in the browser of your choice, if promptet click Advanced.
- ![download](/images/apache/apache_34.png)
16. If prompted click continue
- ![download](/images/apache/apache_35.png)
17. The final result should look as follows:
- ![download](/images/apache/apache_36.png)
