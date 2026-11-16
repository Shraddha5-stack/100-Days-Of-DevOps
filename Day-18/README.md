# Day 18 – Install and Configure MariaDB Server

## 📌 Task Overview

The objective of this task was to install and configure MariaDB Server on the Nautilus Database Server in the Stratos Datacenter.

### Requirements

1. Install and configure MariaDB Server.
2. Create a database named `kodekloud_db5`.
3. Create a user named `kodekloud_aim`.
4. Set the required password for the user.
5. Grant full privileges to the user on `kodekloud_db5`.

## 🖥️ Environment Details

| Component        | Details                     |                                                                                                                                                                                                                                                                                                                                                                                                                                                 |      |       |
| ---------------- | --------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---- | ----- |
| Server           | stdb01                      |                                                                                                                                                                                                                                                                                                                                                                                                                                                 |      |       |
|                  | LinkedIn window that opens. | 🚀 Another task down in the 100 Days of DevOps challenge on KodeKloud Engineer! Task: Day 18: Install and Configure DB Server Solving real-world tasks in a live environment is by far the fastest way I have found to build practical skills — one task at a time. 💪 Want to take on the challenge too? Start here 👉 [https://engineer.kodekloud.com](https://engineer.kodekloud.com) #KodeKloud #KodeKloudEngineer #100DaysOfDevOps #DevOps | User | peter |
| Operating System | CentOS Stream 9             |                                                                                                                                                                                                                                                                                                                                                                                                                                                 |      |       |
| Database Server  | MariaDB                     |                                                                                                                                                                                                                                                                                                                                                                                                                                                 |      |       |
| MariaDB Version  | 10.5.29                     |                                                                                                                                                                                                                                                                                                                                                                                                                                                 |      |       |
| Database Name    | kodekloud_db5               |                                                                                                                                                                                                                                                                                                                                                                                                                                                 |      |       |
| Database User    | kodekloud_aim               |                                                                                                                                                                                                                                                                                                                                                                                                                                                 |      |       |

## ⚙️ Implementation Steps

### Step 1: Install MariaDB Server

Installed MariaDB Server using the DNF package manager.

```bash
sudo dnf install mariadb-server -y
```

### Step 2: Enable and Start MariaDB

Enabled MariaDB to start automatically at boot and started the service.

```bash
sudo systemctl enable --now mariadb
```

Verified the service status:

```bash
sudo systemctl status mariadb
```

**Result:** MariaDB service was active and running.

### Step 3: Connect to MariaDB

Logged in to the MariaDB database server:

```bash
sudo mysql
```

### Step 4: Create the Database

Created the required database:

```sql
CREATE DATABASE kodekloud_db5;
```

**Result:** `Query OK`

### Step 5: Create the Database User

Created the required database user:

```sql
CREATE USER 'kodekloud_aim'@'%' IDENTIFIED BY '<TASK_PASSWORD>';
```

> Security note: The actual task password is intentionally excluded from this public repository.

### Step 6: Grant Full Database Privileges

Granted all privileges on the specified database to the user:

```sql
GRANT ALL PRIVILEGES ON kodekloud_db5.* TO 'kodekloud_aim'@'%';
```

Applied privilege changes:

```sql
FLUSH PRIVILEGES;
```

**Result:** Both commands executed successfully.

## 🔍 Verification

### 1. Verify Database Creation

```sql
SHOW DATABASES LIKE 'kodekloud_db5';
```

**Result:** The `kodekloud_db5` database was displayed successfully.

### 2. Verify User Creation

```sql
SELECT User, Host FROM mysql.user WHERE User='kodekloud_aim';
```

**Result:**

| User          | Host |
| ------------- | ---- |
| kodekloud_aim | %    |

### 3. Verify User Permissions

```sql
SHOW GRANTS FOR 'kodekloud_aim'@'%';
```

The output confirmed the following database-level privilege:

```sql
GRANT ALL PRIVILEGES ON `kodekloud_db5`.* TO `kodekloud_aim`@`%`;
```

**Result:** Full privileges were successfully granted on the required database.

## 📸 Screenshots

### Solution 01 – MariaDB Installation and Service



### Solution 02 – Database and User Creation



### Solution 03 – Granting Database Privileges



### Solution 04 – Verification



## 📚 Key Learnings

- Installing MariaDB Server using DNF.
- Managing database services using systemd.
- Connecting to MariaDB through the MySQL client.
- Creating databases and database users.
- Granting database-level privileges.
- Verifying database users and permissions.
- Understanding basic MariaDB administration commands.

## ✅ Final Result

Successfully installed and configured MariaDB Server on `stdb01`, created the `kodekloud_db5` database, created the `kodekloud_aim` user, and granted full privileges on the specified database.

**Task Status: Completed Successfully!**

