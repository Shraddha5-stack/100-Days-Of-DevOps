# Day 10 – Bash Script for Website Archiving

## 📌 Task Description

The production support team at xFusionCorp Industries required a Bash script to automate the archiving of static website content hosted on App Server 1 in the Stratos Datacenter.

The objective was to create a ZIP archive of the ecommerce website, store it locally, and transfer a copy to the Nautilus Storage Server without requiring an interactive password.

### Requirements

- Create a Bash script named `ecommerce_archive.sh`.
- Store the script under `/scripts` on App Server 1.
- Compress `/var/www/html/ecommerce` into `xfusioncorp_ecommerce.zip`.
- Save the archive under `/archives` on App Server 1.
- Copy the archive to `/archives` on the Nautilus Storage Server.
- Configure passwordless SSH authentication.
- Allow the application server user to execute the script.
- Do not use `sudo` inside the script.

---

## 🖥️ Server Details

| Component | Details |
|---|---|
| Jump Host | `jump-host` |
| App Server | `stapp01` |
| App Server User | `tony` |
| Storage Server | `ststor01` |
| Storage Server User | `natasha` |
| Website Directory | `/var/www/html/ecommerce` |
| Script Location | `/scripts/ecommerce_archive.sh` |
| Local Archive | `/archives/xfusioncorp_ecommerce.zip` |
| Remote Archive | `/archives/xfusioncorp_ecommerce.zip` |

---

## 🔧 Implementation Steps

### 1. Verify ZIP Installation

Checked whether the ZIP utility was installed:

```bash
zip -v
which zip
```

ZIP 3.0 was already installed on App Server 1.

### 2. Configure Passwordless SSH Authentication

Generated an RSA SSH key pair as the `tony` user:

```bash
ssh-keygen -t rsa -b 4096
```

Copied the public key to the Storage Server:

```bash
ssh-copy-id natasha@ststor01
```

Tested passwordless SSH connectivity:

```bash
ssh natasha@ststor01
```

Successfully connected without entering a password.

### 3. Verify Storage Directory

Checked remote archive directory permissions:

```bash
ssh natasha@ststor01 'ls -ld /archives'
```

The directory was writable by the Storage Server user.

### 4. Create the Bash Script

Created the script:

```bash
cat > /scripts/ecommerce_archive.sh <<'EOF'
#!/bin/bash

SOURCE_DIR="/var/www/html/ecommerce"
ARCHIVE_DIR="/archives"
ARCHIVE_NAME="xfusioncorp_ecommerce.zip"

REMOTE_USER="natasha"
REMOTE_HOST="ststor01"
REMOTE_DIR="/archives"

# Create archive
zip -r "${ARCHIVE_DIR}/${ARCHIVE_NAME}" "${SOURCE_DIR}"

# Copy archive to Storage Server
scp "${ARCHIVE_DIR}/${ARCHIVE_NAME}" "${REMOTE_USER}@${REMOTE_HOST}:${REMOTE_DIR}/"

echo "Archive created and copied successfully!"
EOF
```

### 5. Set Executable Permissions

```bash
chmod +x /scripts/ecommerce_archive.sh
```

Verified script permissions:

```bash
ls -l /scripts/ecommerce_archive.sh
```

The script was owned by `tony` and had executable permissions.

### 6. Execute the Script

Executed the script as the application server user:

```bash
/scripts/ecommerce_archive.sh
```

The

