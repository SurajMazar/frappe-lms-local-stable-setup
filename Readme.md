# Local Setup for Frappe LMS

For more configurations, visit the [official Frappe LMS repository](https://github.com/frappe/lms).

This guide explains how to set up Frappe LMS locally **with persistent files and images**, so that uploaded content is not lost when the container restarts.

---

## Steps

### 1. Clone the repository

```bash
git clone <repo-url>
cd <repo-directory>
```

---

### 2. Prepare Docker Compose

Open the Docker Compose file:

```
docker/docker-compose.yml
```

**Comment out** the following line temporarily:

```yaml
- ./frappe-bench:/home/frappe/frappe-bench
```

This allows the container to **initialize the necessary folder structure internally**.

---

### 3. Start the container

Run:

```bash
docker compose -f docker/docker-compose.yml up
```

This will create the required Frappe LMS directories inside the container at:

```
/home/frappe/frappe-bench
```

---

### 4. Copy the initialized files to your host

Once the container has initialized, copy the contents to your local directory for persistence:

```bash
docker cp lms-frappe-1:/home/frappe/frappe-bench ./docker/frappe-bench
```

---

### 5. Restore Docker Compose mount

Uncomment the line in `docker/docker-compose.yml`:

```yaml
- ./frappe-bench:/home/frappe/frappe-bench
```

This ensures that **Frappe uses your local folder** for all future runs, preserving uploads and configuration.

---

### 6. Start Frappe LMS

Use the helper script:

```bash
./start.sh
```

Frappe LMS will be available at: [http://localhost:8000](http://localhost:8000)

---

### 7. Stop Frappe LMS

Use the helper script:

```bash
./stop.sh
```

---

### ✅ Notes

* This setup ensures **persistent storage** for site files and images.
* For any additional configuration, refer to the [official Frappe LMS repository](https://github.com/frappe/lms).
* Ensure you have Docker and Docker Compose installed before starting.
