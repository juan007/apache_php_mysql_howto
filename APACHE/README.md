# APACHE INSTALLATION AND SITE CONFIGURATION - WINDOWS 10
Apache version for this tutorial: 2.4.52

---

## DOWNLOAD THE FILES


1. From [Apache VS16 binaries and modules](https://www.apachelounge.com/download/) download (apachelounge.com) download latest version of Apache x.x.X Win64 (For this tutorial we are going to use the 2.4.52 version).
- ![download](/images/apache_1.png)

2. Once the download is done go to the Downloads folder, extract the files and copy the Apache24 folder to c:/Apache24

---

## INSTALL


1. Open the Command Prompt as administrator
- ![download](/images/apache_2.png)

2. In the command prompt go to the Bin folder by typing: `cd c:\Apache24\Bin`
- ![download](/images/apache_3.png)
3. Once in the Bin folder, type: `httpd.exe -k install`
- ![download](/images/apache_4.png)
4. After the installation is done the command prompt should look like this:
- ![download](/images/apache_5.png)

---

## START THE SERVICE


1. In the windows search bar type services.msc and press enter.
- ![download](/images/apache_6.png)
    
    - The following screen should open:
    - ![download](/images/apache_7.png)
3. Locate the Apache2.4 service and right click over it, choose start.
- ![download](/images/apache_8.png)
4. If the service started correctly it should read “Running” under the status column.
- ![download](/images/apache_9.png)
5. To test Apache open a web browser of your choice and go to `http://localhost`.  The following default page should be shown:
- ![download](/images/apache_10.png)
---

## CONFIGURE 2 SITES
Now that Apache is running lets configure 2 sites, the names of the sites can be anything you want, but for this tutorial we are going to create the sites mysite.jr and mysecondsite.jr

1. In the file explorer Go to `C:\Apache24\conf` and open the file httpd.conf
2. In that file find the text `# Include conf/extra/httpd-vhosts.conf`.  Erase the # to uncomment the line.  Save your changes.  We do this so that the server looks for additional configurations on the httpd-vhosts.conf file.
- ![download](/images/apache_11.png)