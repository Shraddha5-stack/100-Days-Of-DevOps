# Day 09 – Fix MariaDB Service Failure

## 📌 Task Description

A production issue was reported in the Stratos Datacenter because the MariaDB 10.5 database service was failing to start on the database server.

**Requirements:**
- Investigate why the MariaDB service is failing.
- Identify and fix the root cause.
- Ensure the MariaDB service starts successfully.

**Server:** `stdb01`  
**User:** `peter`  
**Service:** `mariadb`

---

## 🔍 Troubleshooting Steps

### 1. Check MariaDB Service Status

```bash
sudo systemctl status mariadb
```

Initially, the MariaDB service was inactive and failed to start.

### 2. Inspect MariaDB Logs

```bash
sudo cat /var/log/mariadb/mariadb.log
```

The logs revealed the following error:

```text
Can't create/write to file '/run/mariadb/mariadb.pid'
(Errcode: 13 "Permission denied")
```

### 3. Check Runtime Directory Permissions

```bash
sudo ls -ld /run/mariadb
```

The directory was owned by `root:mysql`, which prevented the MariaDB process from creating its PID file.

### 4. Fix Directory Ownership

Changed the ownership of the MariaDB runtime directory:

```bash
sudo chown mysql:mysql /run/mariadb
```

Verified the updated ownership:

```bash
sudo ls -ld /run/mariadb
```

Expected ownership:

```text
drwxr-xr-x 2 mysql mysql
```

### 5. Start MariaDB Service

```bash
sudo systemctl start mariadb
```

### 6. Verify Service Status

```bash
sudo
