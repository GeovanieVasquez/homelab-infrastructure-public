# Service inventory and access results

Observed November 19, 2026. “Rendered” means the interface responded during inspection. “Running” and “healthy” are the state labels shown by the relevant platform; they do not prove all application functions work.

| Service | Purpose | Verified hosting or relationship | Inspection and state evidence |
| --- | --- | --- | --- |
| Homepage | Service directory and resource widgets | Docker image from gethomepage; Homepage stack on the inspected Docker host | Dashboard rendered; container healthy |
| Proxmox VE | Virtualization and host administration | One host with two QEMU VMs and two LXC guests | Version 9.2.10; host and all four guests running |
| Portainer CE | Container administration | Portainer Docker container; local Docker-socket environment | CE 2.45.0 LTS; one environment up; Docker 29.7.2 |
| NetBird | Client connectivity and routed LAN access | Hosted management dashboard; routing LXC peer | Four peers listed; desktop and routing peer last seen just now; laptop and phone had older last-seen values |
| NetBird reverse proxy | HTTPS application-service routing | netbirdio/reverse-proxy image on Docker host | Container running; two configured HTTPS entries for Jellyfin and Vaultwarden; remote access not exercised |
| NAS | Storage role | Running unprivileged Ubuntu LXC with ZFS-backed mounts | Summary and Resources inspected in Proxmox; dashboard links to a file share, not a NAS web console |
| Jellyfin | Media serving | Guest/container placement not independently verified; NetBird HTTPS entry exists | Library UI and admin dashboard rendered; server/web/build version 10.11.11; playback not tested |
| Seerr | Discovery and media requests | Dashboard calls this Jellyseerr; destination identifies itself as Seerr | Interface rendered; Stable 3.4.1; no request submitted or integration configuration inspected |
| Sonarr | Series organization and automation | System page explicitly reports Docker, LinuxServer.io package, .NET and SQLite | Version 4.0.19.2979; populated UI; one update warning; workflows and client integrations not tested |
| Bazarr | Subtitle management | Separate linked endpoint; hosting not verified | Populated series interface rendered; no subtitle job run |
| Vaultwarden | Password management | vaultwarden/server image, dedicated stack, NetBird HTTPS entry | Docker healthy; existing browser tab showed a Vaultwarden loading screen only; no vault or credential records opened |
| Radarr | Movie organization and automation | Dashboard-linked endpoint only | Login form rendered; configuration and workload unavailable |
| Lidarr | Music organization and automation | Dashboard-linked endpoint only | Authentication configuration requirement blocks inspection; no settings changed |
| Prowlarr | Indexer management | Dashboard-linked endpoint only | Login form rendered; configuration and integrations unavailable |
| qBittorrent | Download client | Dashboard-linked endpoint only | WebUI login rendered; jobs and storage configuration unavailable |
| NZBGet | Download client | Dashboard-linked endpoint only | Browser reported invalid authentication credentials during navigation; application contents unavailable |

## Scope and dependencies

The dashboard groups services by purpose, while Portainer confirms placement for four infrastructure containers. Sonarr independently confirms Docker hosting. No claim is made that all media applications belong to the inspected Docker environment.

NetBird confirms a routing-peer relationship and two HTTPS service entries. The target fields were counted by the interface but backend destination settings were not opened. The documented app associations come from the service names in those entries; end-to-end routing and authentication behavior remain untested.

NAS export implementation, Samba configuration, application media mounts, download-client integrations and request-automation connections require further evidence. The dashboard's NAS icon does not verify a TrueNAS deployment.

## Access boundaries

Existing authenticated sessions were reused for infrastructure inspection. No passwords, browser profiles, cookies, saved credentials, tokens, vault entries or API-key pages were accessed. Login/setup prompts were left unchanged. No application settings, services or guest states were modified.
