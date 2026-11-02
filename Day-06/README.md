# Day 06 – Create a Cron Job

## 📌 Task Overview

As part of the 100 Days of DevOps Challenge on KodeKloud Engineer, I completed a Linux system administration task involving cron job configuration.

The objective was to install and configure cron on all Nautilus application servers in the Stratos Datacenter and schedule a recurring task.

## 🎯 Requirements

1. Install the `cronie` package on all application servers.
2. Start the `crond` service.
3. Configure a cron job for the root user.
4. Execute the following command every five minutes:

```bash
echo hello > /tmp/cron_text
```

## 🖥️ Servers

| Server | User |
|---|---|
| App Server 1 (`stapp01`) | `tony` |
| App Server 2 (`stapp02`) | `steve` |
| App Server 3 (`stapp03`) | `banner` |

## 🛠️ Implementation

### Step 1: Install Cronie

```bash
sudo yum install -y cronie
```

### Step 2: Start and Enable Cron Service

```bash
sudo systemctl start crond
sudo systemctl enable crond
```

### Step 3: Configure Root Cron Job

```bash
sudo crontab -e
```

Add this entry:

```cron
*/5 * * * * echo hello > /tmp/cron_text
```

Repeat these steps on all three application servers.

## 🔍 Verification

Check whether Cronie is installed:

```bash
rpm -q cronie
