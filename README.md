# wordpress-on-aws-lightsail

Deploy a WordPress blog on **AWS Lightsail**, a cost-effective and beginner-friendly platform that provides pre-configured virtual private servers (VPS), which makes it a good fit for hosting WordPress.

**Live site:** `http://jalgaaaara.duckdns.org` (free DuckDNS domain pointing at a Lightsail static IP)

---

## Project Overview

| Item | Details |
|---|---|
| Platform | Amazon Lightsail |
| Application | WordPress (Bitnami pre-configured image) |
| Instance name | `WordPress-1` |
| Region | Mumbai, Zone A (`ap-south-1a`) |
| Instance specs | 512 MB RAM, 2 vCPUs, 20 GB SSD |
| Networking | Dual-stack (IPv4 + IPv6), static IP attached |
| Domain | `jalgaaaara.duckdns.org` (DuckDNS) |
| Backup | Manual snapshot of the 20 GB system disk |

---

## Screenshots

### 1. WordPress Blog (Live)
The default "My Blog" site with the starter "Hello world!" post, served from the custom domain.

![WordPress blog](screenshots/wordpress-blog.png)

### 2. WordPress Admin Login
The admin login page at `/wp-admin/`.

![WordPress login](screenshots/wordpress-login.png)

### 3. Lightsail Instance and Networking
The `WordPress-1` instance running in Mumbai with a static IP, private IPv4 and public IPv6 addresses. Both status checks passed.

![Lightsail networking](screenshots/lightsail-networking.png)

### 4. Snapshot in Progress
A manual snapshot being created from the Snapshots tab.

![Snapshotting](screenshots/snapshot-in-progress.png)

### 5. Snapshot Completed
The snapshot of the 20 GB SSD system disk, created on October 30, 2026.

![Snapshot completed](screenshots/snapshot-completed.png)

---

## Deployment Steps

### 1. Sign in to AWS and open Lightsail
- Go to the [AWS Lightsail Console](https://lightsail.aws.amazon.com/).
- Click **Create instance** to set up a new server.

### 2. Choose an instance location
- Select the region closest to your target audience for better performance (this project uses **Mumbai, ap-south-1a**).

### 3. Select an instance image
- Choose **Apps + OS**, then select **WordPress** (pre-installed).
- Alternatively, choose **Linux/Unix + WordPress** if you want more customization.

### 4. Choose an instance plan
- Pick a plan based on your expected traffic.
- For a small blog, the entry-level plan is a good starting point.

### 5. Name and create the instance
- Give the instance a meaningful name (e.g. `my-wordpress-blog`; this project uses `WordPress-1`).
- Click **Create instance** and wait for AWS to provision it.

### 6. Access your WordPress site
- Once the instance is running, open the **Networking** tab in Lightsail.
- Copy the public IP address and paste it into your browser to open the site.

### 7. Retrieve the WordPress admin credentials
- Click **Connect using SSH** in Lightsail.
- Run the following command to get the admin password:

```bash
cat bitnami_application_password
```

- Log in at `http://<your-public-ip>/wp-admin/` (default username is `user`).

### 8. Configure a static IP (recommended)
- In the **Networking** tab, create a **Static IP** so the address does not change on reboot.
- Attach the static IP to your instance.

### 9. Configure a custom domain (optional)
- Register a domain with AWS Route 53 or any other provider (this project uses free **DuckDNS**).
- Point the domain's **A record** to your static IP.

### 10. Enable SSL for HTTPS (recommended)
Install a free Let's Encrypt certificate using the Bitnami tool:

```bash
sudo /opt/bitnami/bncert-tool
```

Follow the prompts to enable HTTPS.

> **Status:** In the screenshot above, the browser shows **"Not secure"** because HTTPS has not been enabled yet. Running the step above resolves this.

### 11. Secure and optimize WordPress
- Keep WordPress, themes and plugins updated.
- Use a security plugin such as **Wordfence**.
- Improve performance with a caching plugin such as **W3 Total Cache** or **LiteSpeed Cache**.

### 12. Back up your instance (recommended)
- In Lightsail, open the **Snapshots** tab and click **Create snapshot**.
- You can also enable **Automatic snapshots** to back up daily (the seven most recent are kept). In this project, automatic snapshots are currently disabled.

---

## Security Checklist

- [ ] Enable HTTPS with Let's Encrypt
- [ ] Change the default admin password after first login
- [ ] Restrict SSH access in the Lightsail firewall where possible
- [ ] Install a security plugin (Wordfence)
- [ ] Enable automatic snapshots
- [ ] Keep WordPress core, themes and plugins updated

---

## Final Thoughts

Deploying WordPress on AWS Lightsail is a fast and cost-effective way to start a blog. With a few additional steps, such as securing the site with SSL, setting up a static IP and using a custom domain, you can build a professional and reliable WordPress website.

---

## Tech Stack

`AWS Lightsail` · `WordPress` · `Bitnami` · `Let's Encrypt` · `DuckDNS`
