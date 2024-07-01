
---

## Hosting MySQL Database with MySQL Workbench

This guide will help you set up a MySQL database on an EC2 Ubuntu instance and connect to it using MySQL Workbench. Let's get started! 🚀

### 1. Create an EC2 Ubuntu Instance

First, you'll need to create an EC2 Ubuntu instance in your AWS console. Follow the usual steps to launch a new instance with Ubuntu as the OS.

### 2. Install MySQL on the EC2 Ubuntu Instance

Once your EC2 instance is up and running, connect to it via SSH. Then, install MySQL using the following commands:

```bash
sudo apt update
sudo apt install mysql-server
sudo systemctl start mysql
sudo systemctl enable mysql
```

### 3. Enable Port 3306 in the EC2 Instance

To allow remote connections, you'll need to enable port 3306 in your security group settings:

- Go to the EC2 dashboard.
- Select your instance and click on the "Security" tab.
- Click on the security group associated with your instance.
- Click "Edit inbound rules."
- Add a new rule:
  - Type: MySQL/Aurora
  - Protocol: TCP
  - Port Range: 3306
  - Source: Anywhere (0.0.0.0/0, ::/0)

### 4. Configure MySQL to Allow Remote Connections

Edit the MySQL configuration file to allow connections from any IP address:

```bash
sudo nano /etc/mysql/mysql.conf.d/mysqld.cnf
```

Find the line that begins with `bind-address` and change its value to `0.0.0.0`:

```ini
bind-address = 0.0.0.0
```

Save the file and exit the editor. Then, restart the MySQL service:

```bash
sudo systemctl restart mysql
```

### 5. Create a New MySQL User

Log into the MySQL shell and create a new user that can connect from any IP address:

```bash
sudo mysql -u root
```

```sql
CREATE USER 'pratik'@'%' IDENTIFIED WITH mysql_native_password BY '123456';
GRANT ALL PRIVILEGES ON *.* TO 'pratik'@'%';
FLUSH PRIVILEGES;
EXIT;
```

### 6. Configure Connection in MySQL Workbench

Finally, open MySQL Workbench on your local machine and configure a new connection:

- Click on the "+" icon to add a new connection.
- Fill in the connection details:
  - **Connection Name:** [Your Connection Name]
  - **Connection Method:** Standard (TCP/IP)
  - **Hostname:** [Your EC2 Public IP]
  - **Port:** 3306
  - **Username:** pratik
  - **Password:** 123456
- Click "Test Connection" to ensure everything is set up correctly.
- If the connection is successful, click "OK" to save the connection.

🎉 You're all set! You've successfully hosted a MySQL database on an EC2 Ubuntu instance and connected to it using MySQL Workbench.

---
