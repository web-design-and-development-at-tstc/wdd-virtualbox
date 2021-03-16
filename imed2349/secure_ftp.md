# Secure FTP with TLS

If you recall when you first logged into FileZilla, you received a dialog box warning you that the server didn't support FTP over TLS and that your password and files would be sent in the clear over the Internet. By default, when using FTP, your connection and anything you transfer is not encrypted. To address this, you should connect to FTP using FTPS (FTP over SSL/TLS).

## Create SSL Certificate

To begin, we need to create a new certificate using the openssl tool.  To verify the tool is installed, run the command `openssl version` and if you see output similar to `OpenSSL 1.1.1i  8 Dec 2020` then the tool is installed and you are ready to go.

Run the command `sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/ssl/private/vsftpd.pem -out /etc/ssl/private/vsftpd.pem`

You will be asked to enter some details (like country). You can either enter the information or just hit enter to leave it at the default value.

Now that we have created our private key, we need to make some additional changes to our vsftpd configuration file. Open the file by running the command `sudo nano /etc/vsftpd.conf`

First, we'll want to enable SSL. Press Ctrl+W and type `ssl_enable`. Then press Enter. This will go to the place in the file where this directive is set. Set the variable to `YES` instead of the default `NO`.

Beneath that variable add the following directives:

```shell
rsa_cert_file=/etc/ssl/private/vsftpd.pem
rsa_private_key_file=/etc/ssl/private/vsftpd.pem
allow_anon_ssl=NO
force_local_data_ssl=YES
force_local_logins_ssl=YES
ssl_tlsv1=YES
ssl_sslv2=NO
ssl_sslv3=NO
require_ssl_reuse=NO
ssl_ciphers=HIGH
```

Save the file and exit by pressing Ctrl+X, then type `Y`, and hit Enter.

Finally, for these changes to take effect, we need to restart vsftpd. To do this, run the command `sudo systemctl restart vsftpd`

## Testing FTP with TLS
To make sure that our FTP server now utilizes FTP over SSL/TLS, we are going to log in with the user we created earlier.

Open up FileZilla and in the Quickconnect bar, enter your server's IP address for the Host, ftpuser for the username, and WDDrules20 for the password (if you didn't use this one, then you should use the password you set when you created the ftpuser account).

You should see a dialog box similar to the one below saying the server's certificate is unknown. Near the bottom, there is a checkbox to "Always trust certificate in future sessions." Go ahead and check this checkbox and then click OK.

![Example Dialog Box for Unknown Certificate in FileZilla](https://inspiringweb.org/vm_images/Filezilla_unknown_certificate_dialog.png)

Try uploading, creating, and editing folders and files within the web root directory (/var/www/html) to ensure everything is still working correctly.

Once you have finished testing, close your FileZilla.