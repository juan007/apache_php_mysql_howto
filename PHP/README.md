# PHP INSTALLATION - WINDOWS 10

PHP version used in this tutorial: PHP 8.1 (8.1.3)
<br>Prerequisite:  Install Apache
<br> Adapted from: [How to Install PHP on Windows 10](https://www.sitepoint.com/how-to-install-php-on-windows/)

---

## Table of Contents
1. [DOWNLOAD THE FILES AND RENAME](#download-the-files-and-rename)
1. [CONFIGURE ENVIROMENT VARIABLE](#configure-enviroment-variable)
3. [PHP MODULE AND DEFAULT PHP FILE](#php-module-and-default-php-file)
4. [TEST](#test)
---

## DOWNLOAD THE FILES AND RENAME
1. Download the PHP zip file from [here](https://windows.php.net/download#php-8.1), make sure to download the Thread Safe version.

2. Create a new folder: `C:\PHP`, extract all the content of the downloaded zip, copy and paste that content into the newly created folder.
- ![download](/images/php/php_1.png)

3. Make a copy of php.ini-development in the same PHP folder
- ![download](/images/php/php_2.png)
4. Rename the copy to php.ini
- ![download](/images/php/php_3.png)

---
## CONFIGURE ENVIROMENT VARIABLE
In order for the Operating System to find the PHP executable we need to change the PATH environment variable.
1. In the Windows search bar type “edit the” and open “Edit the system environment variables”.
2. Click the advanced tab and click Environmental Variables…
- ![download](/images/php/php_4.png)
3. In the System variables section click Path and click Edit…
- ![download](/images/php/php_5.png)
4. Click new, add `C:\php`, and click OK in the current prompt and the next 2 prompts below.
- ![download](/images/php/php_6.png)
---
## PHP MODULE AND DEFAULT PHP FILE
1. Next we are going to configure PHP as a PHP module. 
Add the following text at the end of the C:\Apache24\conf\httpd.conf file:
```
# PHP8 module
PHPIniDir "C:/php"
LoadModule php_module "C:/php/php8apache2_4.dll"
AddType application/x-httpd-php .php
```
The file should look as the following screenshot:
- ![download](/images/php/php_7.png)
2. In the same file add index.php under `<IfModule dir_module>` , next to DirectoryIndex so that the server also looks for this as a default file when hitting the root folder.  Save the changes.
- ![download](/images/php/php_8.png)
3. Restart Apache for the changes to take effect.
---
## TEST
1. To test the configuration is correct lets create an index.php file under `C:\Apache24\htdocs\mysite.jr`(or the site of your preference).
2. Let’s edit that file adding the following PHP code. 
```
<?php
phpinfo();
?>
```
- ![download](/images/php/php_9.png)
3. Finally let’s navigate to the site and test everything works correctly.  The browser must show a page similar to the following:
- ![download](/images/php/php_10.png)
---