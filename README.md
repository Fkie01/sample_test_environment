
#  PCSA Assignment 2 – Docker Test Environment

This Docker environment simulates the grading system for **PCSA Assignment 2 (IC Web Server)**.

It allows you to test your project inside a controlled container with:

-  2GB Memory limit  
-  2 CPU cores  
-  Process limit (512 PIDs)  
-  No network access  
-  Isolated execution environment  

---

##  Requirements

- Docker (Docker Desktop recommended)

Check installation:

```bash
docker --version
````

---

##  Setup Guide

### 1️⃣ Clone This Repository

```bash
git clone https://github.com/Fkie01/sample_test_environment.git
cd sample_test_environment
```

---

### 2️⃣ Build the Docker Image

Make sure you are in the directory containing the `Dockerfile`.

```bash
docker build -t test-env .
```

If successful, you should see:

```
Successfully tagged test-env:latest
```

---

### 3️⃣ Run the Container

Replace `{ABSOLUTE_PATH_TO_YOUR_ASSIGNMENT}` with your real absolute path.

Example:

```
/Users/tiger01/developer/source/cs227/a02-ic-web-server-tiger01
```

Run:

```bash
docker run -it --name pcsa-env --rm \
  --memory=2g \
  --cpus=2.0 \
  --pids-limit=128 \
  --network=none \
  -v {ABSOLUTE_PATH_TO_YOUR_ASSIGNMENT}:/sandbox \
  -w /sandbox/projects/p2 \
  test-env \
  bash
```

---

## 📁 Expected Project Structure

Your assignment directory should look like:

```
a02-ic-web-server-<yourID>/
└── projects/
    └── p2/
        ├── Makefile
        ├── icws
        ├── source files
```

The container will start inside:

```
/sandbox/projects/p2
```

---

### 4️⃣ Open Another Shell (Optional)

If the container is already running and you want a second terminal:

```bash
docker exec -it pcsa-env bash
```

---

##  Inside the Container

Once inside, you can run:

```bash
make clean
make all
./icws --port 9000 --root ./samples
```

---

##  Troubleshooting

### Container name already exists

```bash
docker rm -f pcsa-env
```

---

### Volume mount not working

Check your absolute path:

```bash
pwd
```

Make sure you are not using `~` — use full absolute path.

---

### Docker not found

Install Docker Desktop from:

[https://www.docker.com/products/docker-desktop/](https://www.docker.com/products/docker-desktop/)

```
```
