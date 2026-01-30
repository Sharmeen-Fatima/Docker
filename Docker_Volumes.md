# 📦 Docker Volumes

## 🔹 What is a Docker Volume?

A **Docker Volume** is a special storage area that Docker uses to **save data permanently**, even if the container stops or is deleted.

👉 Normally, when a container is removed, **all inside data is lost**.
👉 Volumes solve this problem by storing data **outside the container**.

**In simple words:**
A Docker volume is like a **separate hard drive** that containers can use to store important data safely.

---

## 🔹 Why Do We Need Docker Volumes?

Containers are **temporary by nature**. If a container crashes, stops, or is deleted, its internal data disappears.

But in real life, applications need to store data like:

* User accounts
* Passwords
* Uploaded files
* Database records
* Logs

That data must **not be deleted** when the container is removed.

✅ **Docker Volumes keep data safe and persistent.**

---

## 🔹 Real Life Example

### 🏫 Example: School Computer Lab

Imagine a school computer lab.

* Each student (container) uses a computer.
* If a student logs out and the system deletes everything, their files are gone 😢

So the school gives each student a **USB drive** to save their work.

💡 That **USB drive = Docker Volume**

Even if:

* The computer shuts down
* The system restarts
* The user logs out

👉 Their data in the USB (volume) is still safe.

---

## 🔹 How Docker Volume Works

1. Docker creates a volume.
2. The volume is connected (mounted) to a container folder.
3. The container reads and writes data into that folder.
4. Even if the container is deleted, the volume still exists.

So data lives in the **volume**, not inside the container itself.

---

## 🔹 Types of Data Storage in Docker

| Storage Type      | Data Safe After Container Delete? | Use Case                         |
| ----------------- | --------------------------------- | -------------------------------- |
| Container Storage | ❌ No                              | Temporary data                   |
| Bind Mount        | ✅ Yes                             | Link local folder with container |
| **Volume**        | ✅ Yes (Recommended)               | Databases, apps, production data |

---

## 🔹 Creating a Docker Volume

### Step 1: Create a Volume

```bash
docker volume create mydata
```

### Step 2: Run a Container with Volume

```bash
docker run -d -v mydata:/app/data nginx
```

Here:

* `mydata` = Volume name
* `/app/data` = Folder inside container

Anything saved in `/app/data` will stay safe in the volume.

---

## 🔹 Real World Example with Database

Databases **must never lose data**.

Example with MySQL:

```bash
docker run -d \
  --name mysql-container \
  -e MYSQL_ROOT_PASSWORD=1234 \
  -v mysql_data:/var/lib/mysql \
  mysql
```

📌 `/var/lib/mysql` is where MySQL stores all database data.
📌 `mysql_data` volume keeps the data safe even if the container is deleted.

---

## 🔹 Check Existing Volumes

```bash
docker volume ls
```

---

## 🔹 Inspect a Volume

```bash
docker volume inspect mydata
```

This shows where the data is stored on your system.

---

## 🔹 Delete a Volume

⚠ Only delete if you do not need the data!

```bash
docker volume rm mydata
```

---

## 🔹 Summary

✔ Docker volumes store data permanently
✔ Data remains safe even if container is deleted
✔ Very important for databases and real applications
✔ Works like an external storage device for containers

**One-line definition:**

> A Docker Volume is a persistent storage system that allows containers to save data safely outside the container.

