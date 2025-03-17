## Linux Package Manager  

### Command 1: Check APT Version  
```bash
apt --version
```  
**Result:** `apt 2.7.14 (amd64)`  

---

### Command 2: Update Package Lists  
```bash
sudo apt update
```  
**Explanation:**  
This command updates the package index, ensuring the system has the latest information on available packages. It is necessary before upgrading to check if newer versions are available.  

---

### Question: What is the difference between `apt update` and `apt upgrade`?  

**Answer:**  
- `apt update`: Refreshes the list of available packages and their versions.  
- `apt upgrade`: Installs the latest versions of all currently installed packages based on the updated package list.  

---

### Command 4: List Upgradable Packages  
```bash
apt list --upgradable
```  
**Result:**  
Lists all installed packages that have a newer version available. Example output:  
```
base-files/noble-updates 13ubuntu10.2 amd64 [upgradable from: 13ubuntu10.1]
bpftrace/noble-updates 0.20.2-1ubuntu4.3 amd64 [upgradable from: 0.20.2-1ubuntu4.2]
...
```  

---

### Command 6: Show Package Details  
```bash
apt show gimp
```  
**Result:**  
Displays information about the `gimp` package, including dependencies, version, and description.  

---

### Command 8: Check If a Package Is Installed  
```bash
apt list --installed | grep gimp
```  
**Result:**  
Shows installed packages related to `gimp`, confirming its installation status.  
```
gimp/noble-updates,now 2.10.36-3ubuntu0.24.04.1 amd64 [installed]
gimp-data/noble-updates,now 2.10.36-3ubuntu0.24.04.1 all [installed,automatic]
...
```  

---

### Question: What is the difference between `remove` and `purge`?  

**Answer:**  
- `apt remove <package>`: Uninstalls the package but keeps configuration files.  
- `apt purge <package>`: Completely removes the package along with its configuration files.  

---

### Question: Why is `sudo apt autoremove` important?  

**Answer:**  
`autoremove` removes unnecessary packages that were installed as dependencies but are no longer required. This helps free up disk space and keep the system clean.  

---

### Question: What does `sudo apt clean` do?  

**Answer:**  
`apt clean` clears the local cache of downloaded `.deb` package files, freeing up space without affecting installed packages.  

---

### Command 13: View Repository Sources  
```bash
cat /etc/apt/sources.list
```  
**Explanation:**  
This command displays the list of repositories where APT looks for packages. It helps identify active package sources for updates and installations.  
