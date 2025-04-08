
# 📊 Profiling a Spring Boot Application Using VisualVM

This guide walks you through downloading, installing, and using **VisualVM** to profile a **Spring Boot** application with enhanced JVM flags for better profiling support.

---

## 🧰 Prerequisites

- Java JDK (8 or higher)
- Spring Boot project (Maven-based)
- Maven (`mvn`) installed
- VisualVM

---

## 🔽 Step 1: Download and Install VisualVM

1. Visit: [https://visualvm.github.io](https://visualvm.github.io)
2. Download the version for your OS:
   - Windows: `.zip` or `.exe`
   - macOS: `.dmg`
   - Linux: `.tar.gz`
3. Extract and run:
   - Windows: `visualvm.exe`
   - macOS/Linux: `./bin/visualvm`

> 📌 VisualVM may also be included in your JDK as `jvisualvm`.

---

## ⚙️ Step 2: Add Spring Boot Actuator (Optional but Recommended)

To expose runtime metrics in your Spring Boot app, add this to your `pom.xml`:

```xml
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>
```

---

## 🚀 Step 3: Run Spring Boot with JVM Profiling Flags

Use the following Maven command to run your Spring Boot app with JVM options enabled for profiling, in Linux:

```bash
MAVEN_OPTS="-Dcom.sun.management.jmxremote \
            -Dcom.sun.management.jmxremote.port=9010 \
            -Dcom.sun.management.jmxremote.local.only=false \
            -Dcom.sun.management.jmxremote.authenticate=false \
            -Dcom.sun.management.jmxremote.ssl=false \
            -Djava.rmi.server.hostname=127.0.0.1" \
mvn spring-boot:run
```
For Windows, use the following command: 

```cmd
set MAVEN_OPTS=-Dcom.sun.management.jmxremote ^
 -Dcom.sun.management.jmxremote.port=9010 ^
 -Dcom.sun.management.jmxremote.local.only=false ^
 -Dcom.sun.management.jmxremote.authenticate=false ^
 -Dcom.sun.management.jmxremote.ssl=false ^
 -Djava.rmi.server.hostname=127.0.0.1
mvn spring-boot:run
```

These flags allow:
- `-Dcom.sun.management.jmxremote`: Enables JMX (Java Management Extensions)
- `-Dcom.sun.management.jmxremote.port=9010`: The port VisualVM connects to
- `-Dcom.sun.management.jmxremote.local.only=false`: Allows non-local connections (optional if local only)
- `-Dcom.sun.management.jmxremote.authenticate=false`: No username/password required
- `-Dcom.sun.management.jmxremote.ssl=false`: No SSL needed
- `-Djava.rmi.server.hostname=127.0.0.1`: Ensure correct RMI binding (important if issues occur)

---

## 🔍 Step 4: Connect to the App in VisualVM

1. Launch **VisualVM**
2. Look under **"Local"** for your Spring Boot process
3. Double-click to view monitoring info

---

## 📈 Step 5: Start Profiling

Navigate to the tabs:

- **Monitor** – CPU, heap, GC, threads
- **Sampler** – Low-overhead profiling
- **Profiler** – Detailed method-level analysis (more resource-intensive)

### Example:
1. Click **Profiler** → **CPU** → **Start**
2. Use your app normally
3. Click **Stop** to analyze performance

---

## 🧠 Step 6: Analyze Results

Check for:
- Hot methods (high CPU usage)
- Memory usage by class
- Thread contention
- GC overhead

Use insights to refactor and optimize performance.

---

## 🌐 Optional: Access Spring Boot Metrics

Add this to `application.properties`:

```properties
management.endpoints.web.exposure.include=*
management.endpoint.metrics.enabled=true
```

Then access:

```
http://localhost:8080/actuator/metrics
```

Example sub-metric (e.g. JVM memory):
👉 http://localhost:8080/actuator/metrics/jvm.memory.used

---

## ✅ Summary

| Step | Description |
|------|-------------|
| 1 | Install VisualVM |
| 2 | Add Actuator (optional) |
| 3 | Run Spring Boot with JVM flags |
| 4 | Connect to app using VisualVM |
| 5 | Profile using Sampler/Profiler tabs |
| 6 | Analyze and optimize code |

---

