# Lessons and review questions

## Motivation

The owner built this lab to extend a passion for building computers into understanding how everyday services work. That motivation was confirmed directly during documentation.

## What the inspection demonstrates

**Infrastructure has multiple capacity layers.** The host reports ZFS pool sizes while the NAS guest has separately configured allocations. The two large mounts total 32000G as configured; network-share usable capacity was not measured. Distinguishing those layers avoids overstating storage.

**A directory entry is not a deployment inventory.** Homepage lists many services, but Portainer exposes four containers on one host. Sonarr independently reports Docker hosting outside that four-container list. Service discovery needs corroborating evidence from the actual management interfaces.

**State is not a complete health test.** A container can report running while an application remains uninspected or blocked by authentication. Vaultwarden's container was healthy while its browser tab remained at a loading screen. The inventory deliberately records both signals.

**Evidence should bound operational claims.** Built-in graphs and task history are useful, but they do not establish alerting, completed backups or tested recovery. This project makes those gaps visible instead of assigning unverified reliability metrics.

These are conclusions from documenting the observed environment. They are not claims that the owner personally encountered and solved a particular outage.

## Owner review

| Topic | Confirmation or evidence needed |
| --- | --- |
| Design choices | Reasons for placing storage and routing in LXC and splitting the two VM roles |
| Engineering story | A specific build, migration, integration or troubleshooting challenge personally completed |
| Media hosting | Exact placement of Jellyfin, Seerr, Bazarr and the other media applications; mapping to the media VM |
| Storage sharing | Export protocol, Samba configuration, share permissions and application mount relationships |
| Capacity | Whether “32 TB” refers to guest allocations, advertised disk capacity or desired usable capacity |
| Recovery | Any backup mechanism outside the inspected Proxmox schedule, destinations, retention and restore-test evidence |
| Connectivity | A successful remote-access test and intended access scope |
| DNS and security | LAN resolver arrangement, external DNS ownership, proxy authentication mechanism and policy intent |
| Monitoring | Any external alerting, log retention or monitoring service not linked in the inspected dashboard |

Unconfirmed details are excluded from architecture claims and deployment relationships.

## Evidence and update policy

All observations originate from the real Home Lab dashboard and linked browser interfaces inspected November 19, 2026. No sample infrastructure, generated screenshots or configuration files were substituted.

The eight screenshot assets are faithful captures with crops and opaque redactions. The Jellyfin crop excludes user activity, devices and media counts; Proxmox crops exclude task logs; Docker and proxy captures remove network and domain details. Original JPEGs and the local sanitization helper are outside the repository.

For a future update:

1. Inspect the actual service without making configuration changes.
2. Record the date and distinguish a UI state from a tested workflow.
3. Update service placement only when the hosting relationship is verified.
4. Sanitize screenshots outside the repository and visually review every output.
5. Scan text and diagrams for credentials, addresses and internal endpoints.
6. Validate relative links and image paths; stage only intended documentation.
7. Verify the GitHub destination is private and submit changes through a review branch.

No deployment scripts or service secrets are required for this documentation project.
