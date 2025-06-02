# proxy

# Cruise Ship Proxy System

## Overview

In an effort to reduce internet costs on the cruise ship **Royal Caribs**, a new proxy-based network design was proposed. The goal is to **minimize TCP connections** from the ship to the offshore internet by handling all HTTP/HTTPS traffic through a **single persistent TCP connection**.

Instead of making individual TCP connections for each HTTP request, all browser traffic from the ship is routed through a **Ship Proxy (Client)** that forwards it over a single TCP connection to an **Offshore Proxy Server**, which then relays the requests to the actual internet.

---

## 🌐 Architecture

     +-------------------+
     |     Browser       |
     +-------------------+
               |
            HTTP/S
               |
     +-----------------------+
     |   Ship Proxy Client   | (Runs inside ship network)
     +-----------------------+
               |
   Persistent TCP connection
               |
     +-----------------------+
     | Offshore Proxy Server | (Runs on land/offshore)
     +-----------------------+
               |
            HTTP/S
               |
           INTERNET





---

## ✅ Problem Statement

- Design and implement:
  - A **proxy client** (Ship Proxy).
  - A **proxy server** (Offshore Proxy).
- All HTTP requests from browsers should be routed through the proxy client.
- The proxy client must forward all requests through **one persistent TCP connection** to the proxy server.
- **Sequential Handling**: If multiple requests come in simultaneously, the proxy must process them **one by one**.
- The ship proxy should be configurable in browsers (e.g., Chrome via proxy settings).

---

## 🚀 Expected Output

- Functional proxy system: browser requests through `Ship Proxy` to the `Offshore Server`.
- Requests must be processed and responded to **sequentially**, regardless of arrival time.
- Proxy client should expose **port 8080** for incoming requests.
- Support for:
  - macOS:  
    ```bash
    curl -x http://localhost:8080 http://httpforever.com/
    ```
  - Windows:  
    ```bash
    cur.exe -x http://localhost:8080 http://httpforever.com/
    ```

---

## 🐳 Docker Requirements

- Docker images should be created and published for both the **client** and **server**.
- Provide Docker commands to run each service.

---

## 🔧 Installation & Setup

### Clone the Repository

```bash
git clone https://github.com/gokulmelath/proxy.git
cd proxy
