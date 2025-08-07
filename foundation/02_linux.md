
### **Q1: Why is the execute (`x`) permission essential for navigating into a directory, even if you only want to read files within it?**

**Answer:**
In Linux, the `x` (execute) permission has a special meaning for directories. It allows you to **traverse** the directory — i.e., use `cd` to enter it and access its contents.
Even if a directory has read (`r`) permission, you **cannot open or read files inside it** unless you also have execute (`x`) permission. The `x` permission is essential to:

* `cd` into the directory.
* Use commands like `ls -l`, `cat`, or `open` on files inside it.
* Access subdirectories.

Without execute permission, the directory contents are effectively **inaccessible**, even if file permissions are open.

---

### **Q2: What’s the risk of giving a file or directory 777 permissions (`rwxrwxrwx`), especially on a web server?**

**Answer:**
Using `chmod 777` gives **everyone full access** — read, write, and execute. On a web server, this is dangerous because it allows:

* **Anyone to modify or replace the file.**
* **Malicious users to upload and execute harmful scripts.**

#### Example Scenario:

A PHP file in `/var/www/html/` is given 777 permissions:

```bash
chmod 777 upload.php
```

An attacker can:

* Inject malicious PHP code (webshells, backdoors).
* Execute commands on the server.
* Read or delete sensitive files.
* Compromise databases and steal data.

This could lead to **complete control** of the web server.

**Safer alternatives:**

* Files: `644` (rw-r--r--)
* Directories: `755` (rwxr-xr-x)

---

### **Q3: Why is using symbolic mode (e.g., `chmod g+x file.txt`) better than octal when making small permission changes?**

**Answer:**
Symbolic mode (like `chmod g+x`) changes **only what you specify**. It's safer and easier for **modifying specific bits** without affecting others.

#### Example:

A file has current permissions:

```
-rwx-w-r--
```

You want to **add group execute** permission:

```bash
chmod g+x file.txt
```

This command **only adds** execute permission for the group — nothing else is touched.

If you tried to do this using octal, you’d need to:

* Convert permissions manually.
* Risk accidentally changing read/write/execute bits for other users.

**Symbolic mode = less error-prone + more readable.**

---

### **Q4: What happens if you accidentally type `sudo rm -rf / temp_files/` instead of `sudo rm -rf ./temp_files/`?**

**Answer:**
This is a **catastrophic mistake**.

* The command `sudo rm -rf / temp_files/` is interpreted as:

  1. `rm -rf /` → **Deletes the entire root directory (`/`)**.
  2. `rm -rf temp_files/` → Tries to delete this file/folder *after* your system is already being wiped.

Because it's run with `sudo`, the system gives you **full administrative power**, and `rm -rf /` can:

* **Erase all files**, system-wide.
* **Destroy the operating system.**
* Make the system unbootable.
* Cause **permanent data loss.**



