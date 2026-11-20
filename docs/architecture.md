# Architecture

Inspected November 19, 2026 through authenticated browser interfaces. Names below are role aliases; internal hostnames, guest identifiers and administrative endpoints are intentionally omitted.

## Compute layout

One Proxmox VE 9.2.10 node reported an Intel Core i5-14400, 16 logical CPUs, 15.34 GiB RAM and EFI Secure Boot. Two QEMU VMs and two LXC containers were running.

| Role alias | Virtualization | Observed resources | Evidence and limits |
| --- | --- | --- | --- |
| NAS guest | LXC, Ubuntu, unprivileged | 4 cores; 3.02 GiB RAM; 1 GiB swap; 20G configured root disk | Proxmox Summary and Resources; storage mounts described separately |
| Routing guest | LXC | 1 CPU in resource inventory | Same guest name appears as Ubuntu 22.04 in NetBird and as the network routing peer |
| Media VM | QEMU | 6 CPUs; 8 GiB RAM; 42 GiB boot disk | Proxmox Summary; no guest agent configured; individual media-app placement unresolved |
| Docker host VM | QEMU | 4 CPUs; approximately 2.98 GiB RAM; 64 GiB boot disk | Proxmox Summary; matching hostname and 4 CPUs in Portainer host details |

Portainer identifies the Docker host as Ubuntu 26.04 LTS, Linux x86_64, with Docker Engine 29.7.2. The hostname and CPU correspondence support the VM-to-container-host mapping; a guest-agent network identity was not independently checked.

## Application organization

The inspected Portainer environment is local and uses the Docker socket. It lists four containers: Homepage, Vaultwarden, Portainer and the NetBird reverse proxy. Homepage, Vaultwarden and the reverse proxy are associated with three named stacks in the container table; Portainer is not assigned to a stack there.

Sonarr's System page independently reports Docker: Yes and a LinuxServer.io package. It is not listed among the four containers in this Portainer environment. Therefore the four-container inventory is scoped to this Docker host, not to the entire lab.

Jellyfin, Seerr, Sonarr, Bazarr and the other media-related links share an endpoint address in the dashboard. That fact does not independently prove their guest, container network, or shared storage configuration. This documentation does not draw an unverified dependency from those applications to the NAS.

## Diagram

The main [README](../README.md#infrastructure-architecture) renders the architecture in Mermaid. The editable source is [architecture.mmd](../assets/diagrams/architecture.mmd). Solid relationships express confirmed UI configuration or hosting, rather than packet paths. Matching names support the Docker VM correlation as described above.

There is no standalone monitoring node or DNS-server node in the diagram because neither was confirmed. Resource monitoring is shown as a Proxmox capability in use. The NetBird DNS views listed no custom nameservers or zones.

## Failure boundaries

Only one hypervisor node was visible. VM and NAS summaries reported HA state none, and the NetBird network view reported High Availability inactive. The layout does not establish redundant hosting or automatic failover.

At inspection the host reported roughly 90% RAM usage and nonzero swap use. That is a point-in-time resource observation, not a diagnosis of memory pressure; cache use, workload trends and pressure metrics would need additional investigation.
