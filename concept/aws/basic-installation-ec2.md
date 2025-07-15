# Basic Installation(/Setup) for Applications on EC2

## Index
1. [`Amazon Linux`](#amazon-linux)
   1. [Installing Java 11](#1-installing-java-11-on-amazon-linux)
   2. [Installing MariaDB](#2-installing-mariadb-on-amazon-linux-2023)
   3. [Creating a User with All Privileges in MariaDB and Deleting a User](#3-creating-a-user-with-all-privileges-in-mariadb-and-deleting-a-user)
   4. [Installing Redis 6 (Amazon Linux 2023 Default Package)](#4-installing-redis-6-amazon-linux-2023-default-package)

---

## Amazon Linux

### 1. Installing Java 11 on Amazon Linux
To install Java 11 on Amazon Linux, you can follow these steps:

#### Step 1: Update your system

First, make sure your system is up-to-date with the latest packages:

```bash
sudo yum update -y
```

#### Step 2: Install OpenJDK 11

Amazon Linux comes with OpenJDK available from the default repositories. To install OpenJDK 11, run:

```bash
sudo yum install -y java-11-openjdk-devel
```

#### Step 3: Verify Java installation

Once the installation is complete, verify that Java is installed correctly by checking the version:

```bash
java -version
```

You should see output similar to this:

```
openjdk version "11.0.10" 2021-01-19
OpenJDK Runtime Environment (build 11.0.10+9)
OpenJDK 64-Bit Server VM (build 11.0.10+9, mixed mode)
```

#### Step 4: Set the default Java version (Optional)

If you have multiple versions of Java installed, you can set Java 11 as the default using the `alternatives` command.

```bash
sudo alternatives --config java
```

This will prompt you to select the Java version. Choose the number corresponding to Java 11.

#### Step 5: Set JAVA\_HOME environment variable (Optional)

You may want to set the `JAVA_HOME` environment variable for Java 11. You can add it to your `~/.bashrc` or `/etc/profile` file.

Edit `~/.bashrc` (or `/etc/profile` for system-wide):

```bash
nano ~/.bashrc
```

Add the following line at the end of the file:

```bash
export JAVA_HOME=$(dirname $(dirname $(readlink -f $(which java))))
export PATH=$JAVA_HOME/bin:$PATH
```

Then, source the file to apply the changes:

```bash
source ~/.bashrc
```

Verify the `JAVA_HOME`:

```bash
echo $JAVA_HOME
```

---


### 2. Installing MariaDB on Amazon Linux 2023

#### 1. System Update
First, update the system packages to the latest version:
```bash
sudo dnf update -y
```

#### 2. Install MariaDB
Install MariaDB 10.5 from the default Amazon Linux 2023 repository:
```bash
sudo dnf install -y mariadb105-server mariadb105
```
- `mariadb105-server`: MariaDB server package
- `mariadb105`: MariaDB client and utilities

To verify the installed packages:
```bash
dnf info mariadb105-server
```

#### 3. Start and Enable MariaDB Service
Start the MariaDB service and enable it to run on system boot:
```bash
sudo systemctl start mariadb
sudo systemctl enable mariadb
```

Check the service status:
```bash
sudo systemctl status mariadb
```

#### 4. Secure MariaDB Installation
Run the following to enhance MariaDB security:
```bash
sudo mysql_secure_installation
```
- Set a root password (initially empty, so press Enter).
- Follow prompts to remove anonymous users, disable remote root login, remove test databases, etc., selecting 'Y' for recommended settings.

#### 5. Test MariaDB Connection
Connect to MariaDB to verify it is working:
```bash
mysql -u root -p
```
Enter the root password to access the MariaDB prompt:
```
Welcome to the MariaDB monitor.  Commands end with ; or \g.
MariaDB [(none)]>
```
To list databases:
```sql
SHOW DATABASES;
```

---

### 3. Creating a User with All Privileges in MariaDB and Deleting a User

Below are the steps to create a user with all privileges in MariaDB and to delete a user along with their privileges, tailored for the Amazon Linux 2023 environment with MariaDB 10.5.

#### 1. Connect to MariaDB
Log in to MariaDB as the root user:
```bash
mysql -u root -p
```
Enter the root password set during `mysql_secure_installation`.

#### 2. Create a New User
Create a new user account. For example, a user named `app_user` with the password `your_secure_password`:
```sql
CREATE USER 'app_user'@'localhost' IDENTIFIED BY 'your_secure_password';
```
- `'localhost'`: Restricts access to the local host. For remote access, use `'%'` instead (e.g., `'app_user'@'%'`).

#### 3. Grant All Privileges
Grant all privileges on all databases to the new user:
```sql
GRANT ALL PRIVILEGES ON *.* TO 'app_user'@'localhost' WITH GRANT OPTION;
```
- `*.*`: Applies to all databases and tables.
- `WITH GRANT OPTION`: Allows the user to grant privileges to others.

For remote access:
```sql
GRANT ALL PRIVILEGES ON *.* TO 'app_user'@'%' WITH GRANT OPTION;
```

#### 4. Apply Privileges
Apply the privilege changes:
```sql
FLUSH PRIVILEGES;
```

#### 5. Verify the User and Privileges
Check the created user and their privileges:
```sql
SELECT user, host FROM mysql.user;
SHOW GRANTS FOR 'app_user'@'localhost';
```
For a remote access user, check `'app_user'@'%'`.

#### 6. Delete a User and Their Privileges
To delete the user and revoke all their privileges:
```sql
DROP USER 'app_user'@'localhost';
```
For a remote access user:
```sql
DROP USER 'app_user'@'%';
```
This removes the user and all associated privileges from the MariaDB server.

#### 7. Verify User Deletion
Confirm the user has been deleted:
```sql
SELECT user, host FROM mysql.user;
```
The deleted user (`app_user`) should no longer appear in the list.

#### 8. Test Connection (Before Deletion)
Before deleting, test the new user’s connection:
```bash
mysql -u app_user -p
```
Enter `your_secure_password` to confirm access to the MariaDB prompt.

#### 9. Create a Database (Optional)
If your application requires a specific database, create one (e.g., `jonaslog_db`):
```sql
CREATE DATABASE jonaslog_db;
```
The `app_user` already has full privileges, so no additional grants are needed.

#### 10. Exit MariaDB
Exit the MariaDB prompt:
```sql
EXIT;
```



---


### 4. Installing Redis 6 (Amazon Linux 2023 Default Package)

Amazon Linux 2023 provides the `redis6` package in its default repository, making installation straightforward.

#### 1.1 System Update
Update system packages to the latest version:
```bash
sudo dnf update -y
```

#### 1.2 Install Redis 6
Install the `redis6` package:
```bash
sudo dnf install -y redis6
```

#### 1.3 Start and Enable Redis Service
Start the Redis service and enable it to run on system boot:
```bash
sudo systemctl start redis6
sudo systemctl enable redis6
```

Check the service status:
```bash
sudo systemctl status redis6
```

#### 1.4 Set Client Name and Password
Configure Redis to set a client name and password for enhanced security and identification.

1. **Edit Redis Configuration**:
   Open the Redis configuration file:
   ```bash
   sudo vi /etc/redis6/redis6.conf
   ```

2. **Set Password**:
   Add or uncomment the `requirepass` directive and set a secure password:
   ```
   requirepass your_redis_password
   ```
   Replace `your_redis_password` with a strong password.

3. **Set Client Name (Optional)**:
   Redis does not have a direct "client name" setting in the configuration file, but you can identify clients by setting a name in the client application (e.g., Redisson in your Java application) or by using the `CLIENT SETNAME` command during a session. For example, in `redis6-cli`:
   ```bash
   redis6-cli
   ```
   Inside the CLI:
   ```
   CLIENT SETNAME my_app_client
   ```
   To verify:
   ```
   CLIENT LIST
   ```
   This shows the client name (`name=my_app_client`) in the output.

   For persistent client naming, configure it in your application (e.g., Redisson, as shown later).

4. **Apply Changes**:
   Restart Redis to apply the configuration:
   ```bash
   sudo systemctl restart redis6
   ```

#### 1.5 Verify Installation and Configuration
Check the Redis version:
```bash
redis6-server --version
```
Example output: `Redis server v=6.2.14`

Test the connection with the password:
```bash
redis6-cli -a your_redis_password ping
```
Output: `PONG`

Verify client name (if set in CLI):
```bash
redis6-cli -a your_redis_password
CLIENT LIST
```