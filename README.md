

# Fluig Proxy Cluster Template 🚀

![Fluig](https://img.shields.io/badge/Plataforma-Fluig-blue)
![NGINX](https://img.shields.io/badge/Proxy-NGINX-brightgreen)
![HTTPS](https://img.shields.io/badge/HTTPS-Configurações-green)
![WildFly](https://img.shields.io/badge/Servidor-WildFly-lightgrey)
![PostgreSQL](https://img.shields.io/badge/Database-PostgreSQL-blueviolet)
![DevOps](https://img.shields.io/badge/DevOps-Automatização-critical)

> A complete and functional guide and template to deploy Fluig with NGINX as a reverse proxy, supporting HTTPS, local or public domains, load balancing, cloud deployment, and DevOps practices!

---

# 📋 Scenario Index

| Ordem | Cenário |
|------|---------|
| A | Deploy basic standalone Fluig |
| B | Deploy simple reverse proxy (no domain, no certificate) |
| C | Deploy reverse proxy with load balancing (no domain, no certificate) |
| D | Reverse proxy with local domain (no certificate) |
| E | Reverse proxy with local HTTPS (localhost, no domain) |
| F | Reverse proxy with local domain + local HTTPS (using mkcert) |
| G | Reverse proxy with real domain + real HTTPS (Let's Encrypt) |

---

# 📖 Detailed Scenarios

## Scenario A – Deploy Basic Fluig (Standalone Local)

### ![Fluig](https://img.shields.io/badge/Plataforma-Fluig-blue) ![Modo-Standalone](https://img.shields.io/badge/Modo-Standalone-green)

**Goal:** Run a standalone Fluig instance on WildFly.

**Passos Windows:**
```bash
cd C:\fluig\server\bin
standalone.bat
```

**Passos Linux:**
```bash
cd ~/fluig/server/bin
./standalone.sh
```

**Pontos de Atenção:**
- Java JDK instalado
- Porta 8080 liberada
- Banco de dados operacional

**Teste:**
Acesse `http://localhost:8080` e veja o login do Fluig.

---

## Scenario B – Simple Reverse Proxy (no domain, no certificate)

### ![NGINX](https://img.shields.io/badge/Proxy-NGINX-brightgreen)

**Goal:** Redirect `localhost:80` → `localhost:8080` via NGINX.

**Passos Windows/Linux:**
```nginx
server {
    listen 80;
    server_name localhost;
    location / {
        proxy_pass http://localhost:8080;
    }
}
```
Restart o NGINX.

**Test:**
Access `http://localhost`.

---

## Scenario C – Reverse Proxy with Load Balancing (no domain, no certificate)

### ![Cluster](https://img.shields.io/badge/Cluster-2xFluig-blue)

**Goal:** Load balance between two Fluig instances.

**Steps:**
- Duplicate Fluig (C:\fluig → C:\fluig2)
- Change the second to use port 8081

**CNGINX Configuration:**
```nginx
upstream fluig_cluster {
    server localhost:8080;
    server localhost:8081;
}
server {
    listen 80;
    server_name localhost;
    location / {
        proxy_pass http://fluig_cluster;
    }
}
```

**Test:**
Refresh the browser and observe switching between instances.

---

## Scenario D – Reverse Proxy with Local Domain (no HTTPS)

### ![Domínio](https://img.shields.io/badge/Domínio-fluig.localhost-blue)

**Goal:** Access Fluig via `fluig.localhost`.

**Steps:**
- Add to `/etc/hosts`:
```
127.0.0.1 fluig.localhost
```
- Configure NGINX to recognize `fluig.localhost`.

**Test:**
Access `http://fluig.localhost`.

---

## Scenario E – Local HTTPS Proxy without Domain (using mkcert)

### ![HTTPS](https://img.shields.io/badge/HTTPS-local-yellow)

**Goal:** HTTPS on `localhost`.

**Steps:**
- Generate certificate:
```bash
mkcert localhost
```
- Configure NGINX to use SSL.

**Test:**
Access `https://localhost` (trusted certificate).

---

## Scenario F – Reverse Proxy with Local Domain + Local HTTPS (using mkcert)

### ![HTTPS](https://img.shields.io/badge/HTTPS-local-green)

**Goal:** HTTPS on `fluig.localhost`.

**Steps:**
- Add `/etc/hosts` to `fluig.localhost`
- Generate certificate: `mkcert fluig.localhost`
- Configure NGINX for SSL and HTTP to HTTPS redirection.

**Test:**
Access `https://fluig.localhost`.

---

## Cenário G – Proxy com Domínio Real + HTTPS Real (Let's Encrypt)

### ![Let's Encrypt](https://img.shields.io/badge/SSL-Let's%20Encrypt-success)

**Objetivo:** Deploy real em servidor cloud com HTTPS real.

**Passos:**
- Configurar DNS para apontar para VPS
- Instalar NGINX e certbot
- Rodar:
```bash
sudo certbot --nginx -d fluig.seudominio.com.br
```

**Teste:**
Acesse `https://fluig.seudominio.com.br` com cadeado seguro.

---

# 🛠️ Stack Utilizada

- WildFly / JBoss
- NGINX
- PostgreSQL
- mkcert (SSL local)
- Let's Encrypt (SSL real)
- VPS (Oracle Cloud, DigitalOcean, AWS)
- DevOps (Automação de infraestrutura)

---

© 2025 – Template de Infraestrutura para Fluig.


---

# 🎯 Stacks e Conhecimentos Adquiridos com este Template

Este repositório te guia no aprendizado prático das seguintes tecnologias:

<div align="center">

![Fluig](https://img.shields.io/badge/Plataforma-Fluig-blue)
![NGINX](https://img.shields.io/badge/Proxy-Reverso-brightgreen)
![HTTPS](https://img.shields.io/badge/HTTPS-Configuração-green)
![WildFly](https://img.shields.io/badge/Servidor-WildFly-lightgrey)
![PostgreSQL](https://img.shields.io/badge/Database-PostgreSQL-blueviolet)
![mkcert](https://img.shields.io/badge/Certificados-Locais-yellow)
![Let's Encrypt](https://img.shields.io/badge/SSL-Público-success)
![Docker](https://img.shields.io/badge/Contêinerização-Docker-informational)
![Cloud](https://img.shields.io/badge/Cloud-Deploy-lightblue)
![DevOps](https://img.shields.io/badge/DevOps-Integração_e_Entrega_contínua-critical)
![GitHub Actions](https://img.shields.io/badge/CI/CD-GitHub_Actions-blue)
![Linux](https://img.shields.io/badge/Sistema-Linux-important)
![Windows](https://img.shields.io/badge/Sistema-Windows-brightgreen)

</div>

---

