# genie

A monolithic, "compose-as-infrastructure" homelab deployment secured behind a zero-trust Tailscale network with automated SSL via Split-DNS.

## Architecture 

genie is designed for simplicity, security, and portability. It runs on a single Oracle Cloud instance, utilizing a centralized data structure to make backups and migrations frictionless. 

**Key Security Features:**
* **Zero Exposed Ports:** All services are bound exclusively to a private Tailscale IP. The public internet cannot see or ping this server.
* **Split-DNS:** Uses Cloudflare DNS challenges to generate valid wildcard SSL certificates for private IPs, ensuring local browser trust (no HTTPS warnings) without exposing services.
* **Centralized Secrets:** Environment variables are strictly kept out of the compose file and stored in a hidden `.env/` directory.

## Core

Current active stack:
* **[Nginx Proxy Manager](https://nginxproxymanager.com/)** - Reverse proxy handling routing and Let's Encrypt DNS challenges.
* **[Portainer](https://www.portainer.io/)** - Container management and inspection.
* **[Vaultwarden](https://github.com/dani-garcia/vaultwarden)** - Self-hosted Bitwarden-compatible password manager.
* **[2FAuth](https://github.com/Bubka/2FAuth)** - Web-based Two-Factor Authentication (TOTP) manager.

## Directory

The repository is structured to separate configuration from persistent data.

```text
~/GenieInfra/
├── docker-compose.yml       # The master monolithic infrastructure file
├── .env/                    # (Not in version control) App-specific secrets
│   └── 2fauth.env
└── data/                    # (Not in version control) Persistent app data
    ├── 2fauth/
    ├── npm/
    ├── portainer/
    └── vaultwarden/
