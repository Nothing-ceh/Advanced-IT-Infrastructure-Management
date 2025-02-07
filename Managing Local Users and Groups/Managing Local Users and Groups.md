### **Managing Local Users and Groups in RHEL 9 (RH124)**

Managing users and groups is crucial for security and access control in RHEL 9. This guide covers essential commands, tools, use cases, real-world examples, and a step-by-step practice lab.

---

## **1. Understanding Users and Groups in Linux**

### **1.1 Types of Users**

- **Root User (`UID 0`)** → Superuser with full system control.
- **Regular Users (`UID 1000+`)** → Normal users with limited permissions.
- **System Users (`UID 1-999`)** → Used for system processes and services.

### **1.2 Types of Groups**

- **Primary Group:** A user’s default group when creating files.
- **Secondary Group:** Additional groups a user belongs to for permissions.

---

## **2. Managing Users in RHEL 9**

### **2.1 Creating a New User**

### **Using `useradd` (Default Method)**

```bash

sudo useradd shib
sudo passwd shib

```

- **Use Case:** Creating a new user with a home directory.
- **Benefit:** Provides controlled system access.

### **Using `adduser` (Interactive Method)**

```bash

sudo adduser shib

```

- **Use Case:** Easier alternative that automatically creates a home directory.

---

### **2.2 Modifying User Accounts**

### **Change User Home Directory**

```bash

sudo usermod -d /newhome/shib shib

```

- **Use Case:** Moving user data to a different directory.

### **Add a User to a Secondary Group**

```bash

sudo usermod -aG wheel shib

```

- **Use Case:** Granting additional privileges.

### **Change Username**

```bash

sudo usermod -l newname oldname

```

- **Use Case:** Renaming a user without deleting their account.

---

### **2.3 Deleting Users**

### **Delete User Account**

```bash

sudo userdel shib

```

- **Use Case:** Removing inactive accounts.

### **Delete User and Home Directory**

```bash

sudo userdel -r shib

```

- **Use Case:** Completely removing a user and their files.

---

## **3. Managing Groups in RHEL 9**

### **3.1 Creating a Group**

```bash

sudo groupadd developers

```

- **Use Case:** Organizing users for permission management.

### **3.2 Adding Users to a Group**

```bash

sudo usermod -aG developers shib

```

- **Use Case:** Granting access to shared resources.

### **3.3 Viewing Group Membership**

```bash

groups shib

```

- **Use Case:** Checking which groups a user belongs to.

### **3.4 Deleting a Group**

```bash

sudo groupdel developers

```

- **Use Case:** Removing unused groups.

---

## **4. Checking User and Group Information**

### **4.1 List All Users**

```bash

cat /etc/passwd

```

- **Use Case:** Checking all system users.

### **4.2 List All Groups**

```bash

cat /etc/group

```

- **Use Case:** Viewing existing groups.

### **4.3 Display User Details**

```bash

id shib

```

- **Use Case:** Checking a user’s UID and groups.

---

## **5. Securing User Accounts**

### **5.1 Enforcing Strong Passwords**

```bash

sudo chage -M 90 shib

```

- **Use Case:** Forcing users to change passwords every 90 days.

### **5.2 Locking and Unlocking User Accounts**

### **Lock Account**

```bash

sudo usermod -L shib

```

### **Unlock Account**

```bash

sudo usermod -U shib

```

- **Use Case:** Temporarily disabling accounts without deleting them.

---

## **6. Real-World Example: Managing Team Access**

### **Scenario:**

A system administrator needs to create a group for developers, add users, and grant them sudo access.

### **Step 1: Create a Group**

```bash

sudo groupadd developers

```

### **Step 2: Add Users to the Group**

```bash

sudo useradd -m alice
sudo useradd -m bob
sudo usermod -aG developers alice
sudo usermod -aG developers bob

```

### **Step 3: Grant Sudo Access**

```bash

sudo usermod -aG wheel alice

```

### **Step 4: Verify Group Membership**

```bash

groups alice

```

---

## **7. Step-by-Step Practice Lab**

### **Objective:**

Practice creating, modifying, and deleting users and groups.

### **Lab Steps:**

1. **Create a user named `john` with a home directory.**
    
    ```bash
    
    sudo useradd -m john
    sudo passwd john
    
    ```
    
2. **Create a group named `testgroup` and add `john` to it.**
    
    ```bash
    
    sudo groupadd testgroup
    sudo usermod -aG testgroup john
    
    ```
    
3. **Verify user and group details.**
    
    ```bash
    
    id john
    groups john
    
    ```
    
4. **Change `john`'s shell to `/bin/bash`.**
    
    ```bash
    
    sudo usermod -s /bin/bash john
    
    ```
    
5. **Lock `john`’s account.**
    
    ```bash
    
    sudo usermod -L john
    
    ```
    
6. **Delete `john`’s account and home directory.**
    
    ```bash
    
    sudo userdel -r john
    
    ```
    

---

## **8. Summary Table**

| Task | Command | Example |
| --- | --- | --- |
| Create User | `useradd` | `sudo useradd shib` |
| Set Password | `passwd` | `sudo passwd shib` |
| Modify User | `usermod` | `sudo usermod -aG wheel shib` |
| Delete User | `userdel` | `sudo userdel -r shib` |
| Create Group | `groupadd` | `sudo groupadd developers` |
| Add User to Group | `usermod -aG` | `sudo usermod -aG developers shib` |
| Lock User | `usermod -L` | `sudo usermod -L shib` |
| Unlock User | `usermod -U` | `sudo usermod -U shib` |

[Chapter 2.1](https://www.notion.so/Chapter-2-1-1935512c772680809072ec25cb2435d0?pvs=21)
