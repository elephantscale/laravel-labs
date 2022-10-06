# Setup MySQL Database

### STEP 1) Install MySQL Server package


```bash
sudo apt update
```

```bash
sudo apt install mysql-server
```

Ensure that the server is running using the systemctl start command:

```bash
sudo systemctl start mysql.service
```

### STEP 2) Configure MySQL 

First, open up the MySQL prompt:

```bash
sudo mysql
```

The following example changes the authentication method to mysql_native_password:

```bash
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
```

After making this change, exit the MySQL prompt:

```bash
exit
```

Run the security script with sudo:

```bash
sudo mysql_secure_installation
```

```bash
Output

Securing the MySQL server deployment.

Connecting to MySQL using a blank password.

VALIDATE PASSWORD COMPONENT can be used to test passwords
and improve security. It checks the strength of password
and allows the users to set only those passwords which are
secure enough. Would you like to setup VALIDATE PASSWORD component?

Press y|Y for Yes, any other key for No: Y

There are three levels of password validation policy:

LOW    Length >= 8
MEDIUM Length >= 8, numeric, mixed case, and special characters
STRONG Length >= 8, numeric, mixed case, special characters and dictionary                  file

Please enter 0 = LOW, 1 = MEDIUM and 2 = STRONG:
 0
 
```

As this app is a demo app please use 0 as the validation policy.
In productive environments please use 2 is highly recommended.

```bash
Output

Please set the password for root here.


New password:

Re-enter new password:

```

Please use the following as the MySql Password for the root user

```bash
Laravel1234!
```
```bash
Output

Estimated strength of the password: 100
Do you wish to continue with the password provided?(Press y|Y for Yes, any other key for No) : Y
```

Exit from the MySql console

```bash
exit
```

### STEP 3) Create Database

Access to the MySql console with the root user

```bash
mysql -u root -p
```

Use the password configured in the step 2.

Run the following text to create 

```bash
CREATE Database laravel_course
```

```bash
Output

Query OK, 1 row affected (0.01 sec)
```

Exit MySQL console

```bash
exit;
```
