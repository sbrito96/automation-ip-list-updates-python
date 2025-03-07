# Automating IP Allow List Updates with Python

## 📌 Project Overview

At an organization, access to restricted content is controlled through an **allow list** of IP addresses stored in a file named `allow_list.txt`. A separate **remove list** identifies IP addresses that should no longer have access. 

To automate the process of updating the allow list, I created a Python script that:<br/>
✅ Reads the current allow list.<br/>
✅ Compares it against the remove list.<br/>
✅ Removes IPs that should no longer have access.<br/>
✅ Updates the allow list file with the revised list.<br/>

---

## **1️⃣ Opening and Reading the Allow List**

To begin, the script opens `allow_list.txt` and reads its contents:

```python
import_file = "allow_list.txt"

with open(import_file, "r") as file:
    ip_addresses = file.read()
```

🔹 The `with` statement ensures the file is properly closed after reading.  
🔹 The `.read()` method converts the file content into a **string**.

---

## **2️⃣ Converting the String to a List**

Since IP addresses are stored as a string, I converted them into a list using the `.split()` method:

```python
ip_addresses = ip_addresses.split()
```

🔹 This allows easier removal of specific IP addresses.  
🔹 The `.split()` method separates elements by whitespace and returns a list.

---

## **3️⃣ Iterating Through the Remove List**

I used a **for loop** to iterate through the `remove_list` and check if each IP address exists in `ip_addresses`:

```python
remove_list = ["192.168.1.10", "203.0.113.25", "10.0.0.5"]  # Example IPs to remove

for ip in remove_list:
    if ip in ip_addresses:
        ip_addresses.remove(ip)
```

🔹 The loop checks if each IP in `remove_list` is present in `ip_addresses`.  
🔹 If found, it is removed using `.remove(ip)`.  
🔹 This ensures that only valid entries are deleted, preventing errors.

---

## **4️⃣ Updating the File with the Revised List**

To finalize the process, I converted the updated list back into a string and wrote it to `allow_list.txt`:

```python
with open(import_file, "w") as file:
    file.write("\n".join(ip_addresses))
```

🔹 The `.join()` method combines list elements into a **newline-separated string**.  
🔹 The `"w"` mode in `open()` overwrites the file with the updated allow list.

---

## **5️⃣ Example: Before and After the Update**

### **Before Running the Script (`allow_list.txt`):**
```
192.168.1.10
203.0.113.25
10.0.0.5
172.16.0.1
192.168.0.50
```

### **Remove List (`remove_list`):**
```
192.168.1.10
203.0.113.25
10.0.0.5
```

### **After Running the Script (`allow_list.txt`):**
```
172.16.0.1
192.168.0.50
```

🔹 The script successfully removed the IPs listed in `remove_list`, leaving only the allowed addresses.

---

## **🔹 Summary**

Through this script, I automated the process of **removing unauthorized IP addresses** from the allow list. <br/>
The script:<br/>
✅ **Reads and processes IPs from `allow_list.txt`**  <br/>
✅ **Removes specific IPs from the list**  <br/>
✅ **Updates the allow list file automatically**  <br/>

This automation reduces manual work and enhances security by ensuring outdated or unauthorized IPs are promptly removed from the allow list.
