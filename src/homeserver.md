# NAS / Home Server Setup

For the past few years I’ve wanted a small home server to store data, run some self-hosted services and generally have more control over my own infrastructure.
Cloud services are convenient, but I prefer owning the hardware and the data whenever possible.

So I finally built a small NAS / home server that sits quietly in the corner of my room and runs 24/7.

<picture>
  <img src="/images/nas1.png" alt="nas">
</picture>

The build itself is intentionally simple and power efficient. I didn’t want anything complicated or noisy — just something reliable that can store data and run a few containers.

The motherboard I’m using is the **Topton N100 NAS board**, which I had to import from China.
It comes with an Intel N100 CPU and, most importantly, **six SATA ports** directly on the board which is rare for low-power mini-ITX systems.
It also has 2 M.2 ports, one of which can be extended to have an additional 6 SATA ports which is insane!

For the case I went with the **Fractal Design Node 304**. It’s a compact mini-ITX case specifically designed for NAS builds and can hold **up to six 3.5" HDDs** while still having room for a **full-sized PSU**, which makes the build much easier compared to cases that require SFX power supplies.

Full hardware summary:

- **Motherboard**: Topton N100 NAS board
- **Case**: Fractal Design Node 304
- **RAM**: 16GB DDR4
- **Drives**: 4 × 2TB WD Red HDDs
- **PSU**: Full-size MSI PSU

The N100 is extremely power efficient while still being more than powerful enough for NAS workloads and a handful of containers.

---

## Storage

For the OS I’m running **TrueNAS Core**<sup>[2]</sup>, mainly because it provides a clean interface for managing ZFS and requires very little maintenance.

My storage pool is a **ZFS RAIDZ1 (similar to RAID5)** built from the four 2TB WD Red drives. This gives me redundancy against a single disk failure while still keeping reasonable usable capacity.

<picture>
  <img src="/images/nas2.png" alt="nas">
</picture>

ZFS brings a lot of nice features out of the box:

- checksumming and data integrity
- snapshots
- compression
- easy disk replacement

It’s probably overkill for a small home server, but it’s extremely reliable and well tested.

---

## Backups

Even with redundancy, **RAID is not a backup**.

All important data from the NAS is backed up to **Backblaze B2**<sup>[3]</sup>.
This ensures that even in the worst case scenario (disk failure, filesystem corruption, house burning down, etc.), the data still exists somewhere else.

The backup jobs run periodically and only sync the datasets that actually matter.

---

## Self-Hosted Applications

The NAS also runs a bunch of services that I prefer hosting myself.

Instead of using the TrueNAS app system, I simply run everything with **Docker Compose**.
My full setup is available on my git repo<sup>[1]</sup>.

All application data is stored in docker volumes, and those volumes are backed up to **Backblaze B2** separately as well.

The services I currently host are:

- **Vaultwarden** – password manager
- **Miniflux** – RSS reader
- **Baikal** – CalDAV / CardDAV server
- **Microbin** – pastebin
- **Memos** – note taking
- **Paperless-ngx** – document management
- **Jellyfin** – media server
- **qBittorrent** - sailing the seven seas
- **Immich** – photo backup similar to google photos

<picture>
  <img src="/images/nas3.png" alt="nas">
</picture>

Most of these services are fairly lightweight, so the N100 handles them easily.

---

## Remote Access

I don’t expose any of these services directly to the internet.

Instead I run a **self-hosted Headscale server**<sup>[4]</sup>, which provides a **mesh VPN** similar to Tailscale.
All my devices join the network and can securely access the NAS from anywhere.

This keeps things simple:

- no open ports
- no reverse proxies
- no dealing with certificates

Everything just works once the device joins the mesh network.

---

Sources:

- `[1]`: <https://github.com/mananapr/nas>
- `[2]`: <https://www.truenas.com/>
- `[3]`: <https://www.backblaze.com/b2/cloud-storage.html>
- `[4]`: <https://github.com/juanfont/headscale>

<br>
<center><i>
comments and questions can be left [here](https://github.com/mananapr/mananapr.github.io/issues)
</i></center>
