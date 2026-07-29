# Self-Hosted GitLab VPS Complete Guide: How Much RAM Does GitLab Need? Which VPS Plan Fits Your Team? Evoxt Plan Recommendations and Cost Breakdown (With Performance Tuning and Setup Walkthrough)

If you've ever winced at a per-seat SaaS invoice, you already know why "gitlab vps" keeps climbing the search charts. Developers and small teams are quietly migrating their code, CI/CD pipelines, and project management off metered cloud plans and onto a single VPS they actually own. This guide walks through the full picture—what GitLab really needs to run well, how the math compares to GitLab.com Premium, and which Evoxt VPS plans map cleanly onto each team size—so you can deploy once and stop renting access to your own source code.

## Why Self-Host GitLab on a VPS in the First Place

GitLab is not just a Git server with a web UI bolted on. It is a full DevOps platform—repository management, merge requests, issue boards, CI/CD pipelines, a container registry, monitoring, and integrations—all running as one Rails application stack (Puma, PostgreSQL, Redis, Sidekiq, Gitaly, Workhorse, Nginx, and Prometheus). That richness is exactly why people self-host: you get the platform without the per-user metering.

The usual reasons teams give for moving to a self-hosted gitlab vps setup:

- **Data control** — repositories, merge requests, and secrets stay on hardware you control, which matters for compliance-heavy industries and proprietary code.
- **No per-seat tax** — GitLab Community Edition (CE) is free. You pay for the server, not for each developer who logs in.
- **Unlimited CI minutes** — run your own GitLab Runners on the same flat-rate VPS instead of paying metered CI minutes on the SaaS side.
- **Customization** — private runners, custom integrations, LDAP/SAML auth wired into your identity provider, internal-only registries.

The honest tradeoff is that you also own the maintenance. But for most small teams that maintenance shakes out to roughly an hour a month—an automated nightly backup, a documented monthly upgrade, and OS patching via unattended-upgrades. It is not zero, but it is nowhere near the cost of three SaaS Premium seats.

## How Much RAM and CPU Does GitLab Actually Need

This is the question that decides everything else, and it is also the question most people get wrong. GitLab's own reference architecture is blunt about it: for up to 1,000 users or 20 requests per second, plan for **8 vCPU and 16 GB of RAM**. The documentation does list a memory-constrained floor of 2.5 GB RAM plus 1 GB swap, but it labels that explicitly as a "tinkering" configuration—not something a real team should depend on.

Here is how those official numbers translate into practical team sizes:

| Team / Workload | RAM | CPU | Disk (NVMe/SSD) | Use Case |
| --- | --- | --- | --- | --- |
| Solo / lab, 1 user, light Git | 4 GB (8 GB safer) | 1–2 vCore | 40 GB+ | Personal projects, learning |
| Small team, up to ~25 users, occasional CI | 8 GB | 2–4 vCore | 60–80 GB | Startup, small agency |
| Active team + regular CI/CD pipelines | 16 GB | 4–8 vCPU | 80–100 GB | Daily shipping team |
| 1,000 users / 20 req/s (GitLab official) | 16 GB | 8 vCPU | Scaled to repos | Reference architecture |

Disk matters more than people expect. GitLab explicitly warns that slow storage drags down the entire instance, so plan for **SSD or NVMe** rather than HDD. A bare installation eats roughly 10 GB before you add a single repository; with backups, registries, and CI artifacts, 40 GB disappears fast.

## The Real Cost: Self-Hosted GitLab CE vs GitLab.com Premium

This is where a gitlab vps stops being a hobbyist preference and becomes a budget decision. GitLab.com's hosted Premium tier lists at **$29 per user per month, billed annually**—that is **$348 per user per year**. Self-hosted GitLab Community Edition is **$0**. The only thing you pay for is the server it runs on.

Run the math for a 10-person team:

| Scenario (10-person team) | Annual Cost | What You Get |
| --- | --- | --- |
| GitLab.com Premium SaaS | $3,480/yr ($29/user/mo × 10) | Managed, but metered CI minutes and storage add-ons |
| Self-hosted GitLab CE on a mid-tier VPS | ~$288/yr ($23.99/mo VPS) | Unlimited users, unlimited CI on your own runners, full data ownership |
| **Your savings** | **~$3,192/yr** | Plus no per-seat license and no metered CI upcharges |

The break-even is brutal for SaaS. A single mid-tier VPS costs less per year than one Premium seat. Add developers and the gap only widens, because self-hosted CE has no per-seat license—ten developers or fifty, the server bill does not move.

The honest caveat: CE is not Premium. You give up merge-request approval rules, advanced CI features, code-quality scanning, and security testing. For most small teams that ship code daily, plain CE covers the core—Git hosting, issues, CI/CD pipelines, container registry—and the missing features are convenience, not necessity.

## Evoxt VPS Plans: Full Lineup for Hosting GitLab

Evoxt runs high-clock-frequency virtual machines (cores up to 6.0 GHz) across three network tiers—Standard, Premium, and Premium Plus—each available in 11 plan sizes. Every plan includes **weekly offsite backups at no extra cost**, a 1 Gbps port, full root access, and both Linux and Windows templates. Billing runs from monthly up to 3 years, and you can prepay with account credits.

The Standard network covers nine regions (United States, United Kingdom, Canada, Germany, Poland, Amsterdam, Japan/Tokyo, Malaysia, Australia). Premium covers Hong Kong and Osaka. Premium Plus is a Malaysia premium tier with lower transfer allowances but premium routing.

Below is the complete Evoxt Standard lineup—the tier most teams pick for a GitLab host—followed by the Premium and Premium Plus variants. Prices are current monthly rates.

### Evoxt Standard Network Plans (US, UK, Canada, Germany, Poland, Amsterdam, Tokyo, Malaysia, Australia)

| Plan | CPU | RAM | Storage | Monthly Transfer | Backup | Price | Deploy |
| --- | --- | --- | --- | --- | --- | --- | --- |
| VM-0.5 | 1 core (up to 6.0 GHz) | 512 MB | 5 GB | 500 GB | Weekly | $2.99/mo | [Deploy VM-0.5](https://console.evoxt.com/aff.php?aff=1168&plan=VM-0.5) |
| VM-0.75 | 1 core (up to 6.0 GHz) | 1 GB | 10 GB | 750 GB | Weekly | $4.99/mo | [Deploy VM-0.75](https://console.evoxt.com/aff.php?aff=1168&plan=VM-0.75) |
| VM-1 | 1 core (up to 6.0 GHz) | 2 GB | 20 GB | 1000 GB | Weekly | $5.99/mo | [Deploy VM-1](https://console.evoxt.com/aff.php?aff=1168&plan=VM-1) |
| VM-1.5 | 2 cores (up to 6.0 GHz) | 2 GB | 20 GB | 1500 GB | Weekly | $6.95/mo | [Deploy VM-1.5](https://console.evoxt.com/aff.php?aff=1168&plan=VM-1.5) |
| VM-2 | 2 cores (up to 6.0 GHz) | 4 GB | 30 GB | 2000 GB | Weekly | $11.99/mo | [Deploy VM-2](https://console.evoxt.com/aff.php?aff=1168&plan=VM-2) |
| VM-3 | 4 cores (up to 6.0 GHz) | 4 GB | 30 GB | 3000 GB | Weekly | $14.99/mo | [Deploy VM-3](https://console.evoxt.com/aff.php?aff=1168&plan=VM-3) |
| VM-4 | 4 cores (up to 6.0 GHz) | 8 GB | 60 GB | 4000 GB | Weekly | $23.99/mo | [Deploy VM-4](https://console.evoxt.com/aff.php?aff=1168&plan=VM-4) |
| VM-6 | 8 cores (up to 6.0 GHz) | 8 GB | 60 GB | 5000 GB | Weekly | $29.99/mo | [Deploy VM-6](https://console.evoxt.com/aff.php?aff=1168&plan=VM-6) |
| VM-8 | 8 cores (up to 6.0 GHz) | 16 GB | 80 GB | 6000 GB | Weekly | $47.99/mo | [Deploy VM-8](https://console.evoxt.com/aff.php?aff=1168&plan=VM-8) |
| VM-12 | 16 cores (up to 6.0 GHz) | 16 GB | 80 GB | 8000 GB | Weekly | $60.95/mo | [Deploy VM-12](https://console.evoxt.com/aff.php?aff=1168&plan=VM-12) |
| VM-16 | 16 cores (up to 6.0 GHz) | 32 GB | 100 GB | 10 TB | Weekly | $95.99/mo | [Deploy VM-16](https://console.evoxt.com/aff.php?aff=1168&plan=VM-16) |

### Evoxt Premium Network Plans (Hong Kong, Osaka)

Same CPU, RAM, storage, and pricing as Standard, but with reduced monthly transfer suited to premium Asian routing. VM-0.5 ships 250 GB, VM-1 ships 500 GB, VM-4 ships 2000 GB, scaling up to VM-16 at 5000 GB. If your team is Asia-based and latency matters more than raw bandwidth, this is the tier to 👉 [deploy from](https://console.evoxt.com/aff.php?aff=1168&network=premium).

### Evoxt Premium Plus Network Plans (Malaysia Premium)

The premium Malaysian tier. VM-0.5 starts at $3.49/mo with 150 GB transfer; from VM-0.75 upward, pricing matches Standard and Premium ($4.99 to $95.99), but transfer allowances are the tightest of the three tiers (e.g., VM-4 at 1000 GB, VM-16 at 4000 GB). Best when you need premium Malaysian routing specifically. 👉 [Deploy Premium Plus](https://console.evoxt.com/aff.php?aff=1168&network=premium-plus).

### A La Carte Upgrades

One detail that makes Evoxt flexible for a growing GitLab install: you can scale individual resources without changing plans.

- Extra IP address: **$3/month**
- Extra vCore: **$3/month** (via VM Control Panel upgrade tab)
- Extra RAM: **$2/month per GB**
- Extra monthly transfer: Standard **$3/TB**, Premium **$12/TB**, Premium Plus **$24/TB**
- Paid backup plan: priced based on VM storage size, configurable from the Control Panel

This matters because a GitLab instance that starts lean often needs a RAM bump or an extra core months later—Evoxt lets you add exactly that without migrating to a new plan. 👉 [Start with a base plan and upgrade in-panel](https://bit.ly/EvoXt).

## Mapping Evoxt Plans to GitLab Team Sizes

Now that the full lineup is on the table, here is the practical mapping—built directly from GitLab's reference architecture and Evoxt's published specs.

### Solo / Lab GitLab: VM-2 ($11.99/mo) or VM-3 ($14.99/mo)

For a single user running GitLab as a personal code vault with the occasional CI job, the realistic floor is **4 GB RAM with 2–4 vCore and at least 30 GB NVMe**. On Evoxt, that lands on VM-2 (2 cores, 4 GB RAM, 30 GB, $11.99) or VM-3 (4 cores, 4 GB RAM, 30 GB, $14.99). The extra two cores on VM-3 are worth the $3 if you plan to run a GitLab Runner alongside the web app—CI jobs and the Rails stack fight each other on a 2-core box.

Do not try to run production GitLab on VM-0.5 or VM-1. It will technically boot on 512 MB or 2 GB, then spend the rest of its life swapping and timing out. Use those tiny plans for a reverse proxy, a monitoring node, or a runner, not for the GitLab app itself. 👉 [Deploy VM-3 for a lab GitLab](https://console.evoxt.com/aff.php?aff=1168&plan=VM-3).

### Small Team (up to ~25 users): VM-4 ($23.99/mo)

This is the sweet spot for most readers searching "gitlab vps." Four cores, 8 GB RAM, 60 GB storage, 4 TB transfer, weekly offsite backup included. It comfortably handles a small team with occasional CI, and the 8 GB RAM is the line where GitLab stops feeling sluggish under real Git and pipeline activity. At $23.99/month—less than a single GitLab.com Premium seat—this plan pays for itself the moment your second developer logs in. 👉 [Deploy VM-4 for a small-team GitLab](https://console.evoxt.com/aff.php?aff=1168&plan=VM-4).

### Active Team + Regular CI/CD: VM-8 ($47.99/mo)

When pipelines run daily and the team is shipping constantly, 16 GB RAM and 8 vCore become the dependable choice. VM-8 ships exactly that, with 80 GB storage and 6 TB transfer. This is also the plan that lines up with GitLab's official 1,000-user reference architecture for CPU and RAM—so you have headroom for growth without an immediate migration. 👉 [Deploy VM-8 for an active team](https://console.evoxt.com/aff.php?aff=1168&plan=VM-8).

### Larger Installations: VM-16 ($95.99/mo)

For teams pushing toward GitLab's larger reference architecture, VM-16 brings 16 cores, 32 GB RAM, 100 GB storage, and 10 TB transfer. At under $100/month it still costs dramatically less than a handful of SaaS Premium seats. 👉 [Deploy VM-16](https://console.evoxt.com/aff.php?aff=1168&plan=VM-16).

### Summary Pick

| Your Situation | Pick This Evoxt Plan | Monthly Cost |
| --- | --- | --- |
| Solo / lab GitLab | VM-3 (4 core, 4 GB) | $14.99 |
| Small team, ≤25 users | VM-4 (4 core, 8 GB) | $23.99 |
| Active team + regular CI | VM-8 (8 core, 16 GB) | $47.99 |
| Larger / heavy CI | VM-16 (16 core, 32 GB) | $95.99 |

## Step-by-Step: Install GitLab on an Evoxt VPS

The walkthrough below assumes Ubuntu 24.04 LTS on a VM-4 or larger. The same flow works for VM-3, VM-6, VM-8, and up—just tune the worker counts as described in the next section.

### 1. Prepare the Server

SSH in as root or a sudo user and update the base system:

bash
sudo apt-get update && sudo apt-get upgrade -y
sudo apt-get install -y curl openssh-server ca-certificates perl


Point your domain's A record at the Evoxt VM's IP before the next step, since GitLab's Let's Encrypt integration needs DNS to resolve during install.

### 2. Add the GitLab Repository and Install

For the free Community Edition:

bash
curl -fsSL https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.deb.sh | sudo bash
sudo EXTERNAL_URL="https://gitlab.yourdomain.com" apt-get install gitlab-ce


Setting `https://` in the external URL tells GitLab to request a Let's Encrypt certificate automatically during install. If you would rather start with Enterprise Edition (free up to a user threshold), swap `gitlab-ce` for `gitlab-ee` in both lines.

### 3. Open the Firewall

bash
sudo ufw allow OpenSSH
sudo ufw allow 80/tcp
sudo ufw allow 443/tcp
sudo ufw enable


### 4. First Login

Browse to `https://gitlab.yourdomain.com`. You will be prompted to set a root password. If you miss the prompt, retrieve the auto-generated one with:

bash
sudo cat /etc/gitlab/initial_root_password


That file auto-deletes after 24 hours, so set a permanent password on first login.

### 5. Apply Configuration Changes Anytime

Anything you change in `/etc/gitlab/gitlab.rb` only takes effect after:

bash
sudo gitlab-ctl reconfigure


## Performance Tuning for Smaller Evoxt Plans

If you deployed on VM-3 or VM-4 and want GitLab to feel snappier without immediately upgrading RAM, these tweaks reliably free 300–500 MB and reduce CPU contention. Edit `/etc/gitlab/gitlab.rb`, then run `sudo gitlab-ctl reconfigure`.

### Reduce Puma Workers

On a 4 GB plan, drop Puma workers and threads:

ruby
puma['worker_processes'] = 2
puma['min_threads'] = 1
puma['max_threads'] = 4


### Disable Built-in Monitoring (Saves ~300 MB)

If you do not need Prometheus, Grafana, Alertmanager, and node_exporter running in-process:

ruby
prometheus_monitoring['enable'] = false
grafana['enable'] = false
alertmanager['enable'] = false
node_exporter['enable'] = false


### Tune PostgreSQL for Low Memory

ruby
postgresql['shared_buffers'] = "256MB"
postgresql['work_mem'] = "8MB"
postgresql['maintenance_work_mem'] = "64MB"


### Reduce Sidekiq Concurrency

ruby
sidekiq['concurrency'] = 10


### Add Swap if You Skimped on RAM

Even on VM-4 with 8 GB, a 2 GB swap file is cheap insurance against the 502 Bad Gateway that appears when GitLab exhausts memory during boot:

bash
sudo fallocate -l 2G /swapfile
sudo chmod 600 /swapfile
sudo mkswap /swapfile
sudo swapon /swapfile
echo '/swapfile none swap sw 0 0' | sudo tee -a /etc/fstab


## Security Hardening and Backups

A gitlab vps is only as useful as it is recoverable. Three habits cover most of the risk.

**Mandatory defaults on a fresh install:**

- Enable 2FA for the root account and all admins (Admin → Settings → General → Sign-in restrictions).
- Disable public sign-ups unless you specifically want open registration.
- Require SSH keys for Git operations instead of passwords.
- Keep port 22, 80, and 443 as the only open inbound ports.

**Automated nightly backups:**

bash
echo "0 2 * * * root gitlab-backup create CRON=1" | sudo tee /etc/cron.d/gitlab-backup


Back up the configuration files separately—they are not included in the standard backup tarball:

bash
sudo cp /etc/gitlab/gitlab.rb /var/opt/gitlab/backups/
sudo cp /etc/gitlab/gitlab-secrets.json /var/opt/gitlab/backups/


Limit backup retention so the disk does not fill silently:

ruby
gitlab_rails['backup_keep_time'] = 604800


Evoxt already includes weekly offsite backup at the VM level, so you have two layers: Evoxt's snapshot for catastrophic VM loss, and GitLab's application-level backup for granular restores. 👉 [Deploy a GitLab-ready VPS with weekly offsite backup included](https://bit.ly/EvoXt).

## Common Problems and Quick Fixes

### 502 Bad Gateway Right After Install

Almost always means GitLab ran out of memory during Puma boot. Check status with `sudo gitlab-ctl status` and `sudo gitlab-ctl tail puma`. Fix by reducing Puma workers and adding swap (see above).

### `gitlab-ctl reconfigure` Hangs

Usually DNS or SSL. Verify DNS with `dig gitlab.yourdomain.com`, confirm ports 80 and 443 are open with `sudo ufw status`, and rerun with `sudo gitlab-ctl reconfigure --verbose` to see where it stalls.

### High Memory Usage in Steady State

Run `sudo gitlab-ctl status` and `sudo ps aux --sort=-%mem | head -20` to find the hog. Common fixes: disable Prometheus monitoring, reduce Puma workers, reduce Sidekiq concurrency, add swap.

### SSL Certificate Renewal Fails

Check expiry with `sudo openssl x509 -in /etc/gitlab/ssl/gitlab.yourdomain.com.crt -noout -dates`. Force renewal of built-in Let's Encrypt with `sudo gitlab-ctl renew-le-certs`. If you used certbot, run `sudo certbot renew --dry-run` to debug.

## Alternatives Worth Knowing About

GitLab is not the only path, and a quick comparison helps confirm whether it is the right one for you:

- **Gitea / Gogs** — lightweight Git hosting, a few hundred MB of RAM, ideal if you only need Git + issues and not CI/CD.
- **GitHub Enterprise Server** — on-prem GitHub for teams already invested in that ecosystem.
- **Bitbucket Data Center** — tight Jira/Confluence integration for Atlassian shops.

For most readers landing here on a "gitlab vps" search, GitLab CE on Evoxt is the configuration that gives the most platform per dollar—full CI/CD, container registry, issue boards, and unlimited users for the price of one VPS.

## Frequently Asked Questions

**How much RAM does self-hosted GitLab need?** GitLab's documentation recommends 16 GB for up to 1,000 users and notes it can run on 8 GB in lighter cases. For a solo or small instance, 4 GB is a workable minimum but 8 GB is far smoother once CI runs. Avoid the 2.5 GB memory-constrained floor for any production use.

**What is the cheapest Evoxt VPS that can run GitLab?** A 4 GB RAM plan like Evoxt's VM-2 ($11.99/mo) or VM-3 ($14.99/mo) is the realistic floor for a personal or lab GitLab instance. Anything smaller will boot but feel sluggish under real Git and CI activity. For team use, VM-4 ($23.99/mo, 8 GB) is the dependable choice.

**Is self-hosting GitLab cheaper than GitLab.com?** For most teams, yes. GitLab.com Premium lists at $29/user/month ($348/user/year), while self-hosted Community Edition is free—you pay only for the server. A 10-person team on a VM-4 ($23.99/mo) saves roughly $3,190/year compared to Premium SaaS, plus avoids metered CI and storage upcharges.

**What do I give up with GitLab Community Edition?** CE omits Premium/Ultimate features such as merge-request approval rules, advanced CI options, code-quality scanning, and security testing. The core—Git hosting, issues, CI/CD pipelines, container registry—is fully included and covers most small-team workflows.

**What payment methods does Evoxt accept?** Credit cards, debit cards, PayPal, Bitcoin, and USDt (Tron). Billing plans run from monthly up to 3 years, and you can prepay account credits to apply to future invoices.

**Does Evoxt include backups?** Yes. Every VPS plan ships with automatic weekly offsite backup at no extra cost. A paid daily backup plan is also available from the VM Control Panel for tighter RPOs.

**How long does deployment take?** Less than five minutes. Server deployment on Evoxt is fully automatic.

## Bottom Line

A self-hosted gitlab vps is one of the few infrastructure moves that simultaneously cuts your bill and increases your control. GitLab's official requirements—8 vCPU and 16 GB for 1,000 users—sound intimidating until you realize that Evoxt's VM-8 ($47.99/mo) ships exactly that configuration for less than the cost of two GitLab.com Premium seats. For a small team, VM-4 at $23.99/mo with 8 GB RAM and weekly offsite backup is the plan that turns "we should self-host GitLab someday" into "we self-hosted it this afternoon."

Pick the plan that matches your team size, deploy in under five minutes, and run GitLab CE on hardware you actually own. 👉 [Deploy your GitLab VPS on Evoxt now](https://bit.ly/EvoXt).
