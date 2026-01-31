

# 🐹 Go Application – Multi-Stage Docker Build

This pratical demonstrates how to build and run a Go (Golang) application using a **multi-stage Dockerfile** to produce a lightweight, secure, production-ready container image.

---

## 🚀 Why Multi-Stage Docker Build?

Multi-stage builds allow you to:

✅ Compile the Go app in a full environment
✅ Run it in a minimal container
✅ Remove build tools from final image
✅ Reduce image size drastically

---

## 📦 Dockerfile Overview

```dockerfile
###########################################
# BASE IMAGE (BUILD STAGE)
###########################################

FROM ubuntu AS build

RUN apt-get update && apt-get install -y golang-go

ENV GO111MODULE=off

COPY . .

RUN CGO_ENABLED=0 go build -o /app .

############################################
# MULTI-STAGE RUNTIME IMAGE
############################################

FROM scratch

COPY --from=build /app /app

ENTRYPOINT ["/app"]
```

---

## 🧱 Stage 1 — Build Stage

### 📌 Purpose:

Compile the Go application into a single binary.

### 🔧 What happens:

* Ubuntu OS is used as base
* Go compiler is installed
* Source code is copied
* App is compiled into `/app` binary

### ⚙ Important flags:

| Option             | Meaning               |
| ------------------ | --------------------- |
| `CGO_ENABLED=0`    | Creates static binary |
| `go build -o /app` | Outputs executable    |

---

## 🚀 Stage 2 — Runtime Stage

### 📌 Purpose:

Run only the compiled Go binary in a minimal image.

### 🧊 `scratch` image:

* Completely empty
* No OS packages
* Ultra-lightweight

Only the compiled Go binary is copied into it.

---

## 📊 Image Size Comparison

| Build Type   | Size   | Security |
| ------------ | ------ | -------- |
| Single stage | 600MB+ | ❌ Low    |
| Multi-stage  | 5–15MB | ✅ High   |

---

## 🛠 Build the Docker Image

```bash
docker build -t go-multistage-app .
```

---

## ▶ Run the Container

```bash
docker run go-multistage-app
```

---

## 🎯 Key Benefits

✔ Faster deployments
✔ Minimal attack surface
✔ Production-ready container
✔ Best DevOps practice

---



---



---

## 👨‍💻 Author

**Dhiraj Nimkande**
Cloud & DevOps Engineer

---



Just say 👍
