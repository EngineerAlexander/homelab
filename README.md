# Homelab Repository

This repository contains the setup instructions and **Docker Compose files** I use to run self-hosted applications on my home server. Everything in here is driven by Docker Compose **except** for:

- **Samba** → used as a network share drive
- **Docker** → the container runtime itself
- **SSH** → for secure remote management
- **Tailscale** → to connect securely to my server from anywhere

The collection is expanding as my homelab grows, so feel free to use this repo as a **starting point for your own homelab** and customize it for your needs.

---

## ⚙️ How to Use

### Environment Variables
All Docker Compose files reference **environment variables** using the `${VARIABLE_NAME}` syntax.  
These must be defined in a `.env` file in the same directory so Docker Compose can substitute them correctly.

Example `.env`:
```env
POSTGRES_USER=admin
POSTGRES_PASSWORD=supersecret
APP_PORT=8080
```

### Running a service
From inside any service directory:
```bash
docker compose up -d
```

---

## 🌐 Networking & Access

- My server’s **landing page** is a self-hosted “homelab page,” which I use as my browser homepage to quickly access services.
- I purchased the domain **[bijanlab.com](https://bijanlab.com)** through **Cloudflare**, which I recommend because it integrates smoothly with SSL certificate management.
- SSL certificates are obtained through **NGINX with Let’s Encrypt**.
- Once SSL is set up, you only need to open **HTTP (80)** and **HTTPS (443)** to the internet. NGINX acts as a reverse proxy and forwards requests internally to the right service.

### Secure exposure strategy
- If you don’t want to expose a service to the public internet, set the Cloudflare DNS record to point to your server’s **Tailscale address** instead. NGINX will then forward to the internal port securely over the tailnet.
- For services that **must** be accessed without being on the same tailnet (e.g., mobile apps that don’t support Tailscale), you may open ports directly. **Be cautious**—especially with services that are not protected by authentication or login.

---

## 🔒 Security Notes
- Prefer Tailscale + reverse proxy instead of directly exposing ports.
- Always use SSL certificates for encrypted traffic.
- Only expose what you absolutely need to the open internet.

---

## 🚀 Future Growth
This repository will continue to evolve as I add more services to my homelab. Treat it as a living project and adapt it to your own needs.

---

## 📖 Inspiration
Homelabbing is highly personal—your setup may differ, but this repo shows one approach:  
- Docker Compose for service management  
- Tailscale for private networking  
- NGINX + Cloudflare for secure, SSL-enabled public access  
- Samba for simple file sharing

Feel free to fork, modify, and expand on this foundation.
