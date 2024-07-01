# Hosting MySQL Database with MySQL Workbench

This guide will help you set up a MySQL database on an EC2 Ubuntu instance and connect to it using MySQL Workbench. Let's get started! 🚀

## 1. Create an EC2 Ubuntu Instance

First, you'll need to create an EC2 Ubuntu instance in your AWS console. Follow the usual steps to launch a new instance with Ubuntu as the OS.

## 2. Install MySQL on the EC2 Ubuntu Instance

Once your EC2 instance is up and running, connect to it via SSH. Then, install MySQL using the following commands:

```bash
sudo apt update
sudo apt install mysql-server
sudo systemctl start mysql
sudo systemctl enable mysql
