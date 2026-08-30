# Remediation validation status

This is the exhaustive acceptance checklist for every role currently edited in
the Saltbox and Sandbox worktrees. A checked role has completed its applicable
focused checks, normal Ansible gates, and real Saltbox VM lifecycle. An unchecked
role is not validated, even when one focused failure-path probe has passed.

Test platform unless otherwise stated: Ubuntu 26.04 minimal VM with Saltbox
installed normally, followed by `sb install core`. Core containers are retained
between application-role tests; each non-core application container is removed
after acceptance because the VM is memory constrained.

## Saltbox roles

- [x] `arr_db` — user-validated real role run, supplemented by sequential Sonarr/Radarr full-task and Whisparr filename probes.
- [x] `asshama` — scoped acceptance completed as requested: a labeled dummy `plex` container was discovered, stopped, and restarted with the same container ID; Plex application behavior was not claimed.
- [x] `authelia` — fresh core lifecycle completed the file-backend hash extraction, generated configuration, created the container, and reached healthy status.
- [x] `authentik` — clean full lifecycle completed user/rule setup and the server plus instance-scoped PostgreSQL dependency were both observed healthy before removal; the argv-form PostgreSQL healthcheck passed.
- [x] `authentik_worker` — exercised through Authentik's real import path; the worker was observed healthy before removal.
- [x] `autobrr` — normal first-install lifecycle completed, the generated user path ran, the container was observed running, and it was removed.
- [x] `autoscan` — clean first-install generated its config, the container was observed running with zero restarts, and it was removed.
- [x] `backup` — normal local backup plus a two-VM SFTP lifecycle completed: container and host PostgreSQL stop/start handling passed, the fixture tar and configuration tree uploaded through rclone, all remote hashes matched, Restore Service encryption/upload completed, and the temporary Restore Service record was deleted after acceptance.
- [x] `backup2` — local-only normal backup lifecycle completed without rescue or warnings after disabled-rclone guards; container stop/restart and prior-backup replacement passed.
- [x] `bazarr` — normal first-install lifecycle completed, the container was observed running, and it was removed.
- [x] `btop` — normal host-tool install fetched, unpacked, installed, and cleaned the current release without failures.
- [x] `cloudplow` — a disposable playbook exercised the edited existing-config path with and without a SABnzbd config: recursive JSON updates preserved unrelated and nested values, the API key updated only when present, the missing-file case preserved the old key, the upgrade command received exactly `update_config`, and malformed JSON failed visibly at `from_json`.
- [x] `common` — normal core role passed; additionally, the real Btrfs task file created a child on a loopback Btrfs filesystem, detected `btrfs`, executed `chattr +C`, and `lsattr` confirmed the NOCOW flag before cleanup.
- [x] `crowdsec` — user-validated.
- [x] `ctop` — normal core installation fetched, installed, parsed, and displayed ctop 0.7.7 using the native command result.
- [x] `custom` — the Ubuntu-22.04-gated pip path was exercised in a disposable playbook with the exact role task and a controlled 22.04 fact boundary; `/usr/bin/pip install --help` completed through argv without installing a package, while the normal APT and empty custom package paths also passed.
- [x] `ddns` — formatting-only validation; the edited defaults expression changes line layout only and does not change the rendered value.
- [x] `deluge` — full first-install and native JSON post-install settings lifecycle completed; the restarted container was observed running and then removed.
- [x] `diag` — normal diagnostic role run gathered and filtered mount data and rendered the complete diagnostic variable report.
- [x] `diun` — normal first-install lifecycle rendered its configuration, the container was observed running, and it was removed.
- [x] `docker` — prior discovery-failure and version-boundary probes plus a fresh Ubuntu 26.04 minimal-to-core installation completed the full applicable Docker role without failures.
- [x] `dozzle` — normal install created both Dozzle and its instance-scoped socket proxy; Dozzle was observed running and both non-core containers were removed.
- [x] `emby` — clean first-install and settings lifecycle completed, the restarted container was observed running, and it was removed.
- [x] `gluetun` — user-validated.
- [x] `grafana` — normal first-install lifecycle completed, the container was observed running, and it was removed.
- [x] `hetzner` — normal preinstall/core lifecycles exercised the non-failing native Intel VGA PCI query; an exact GRUB-subtask fixture slurped and parsed an ordered kernel command line, removed every `nomodeset`, preserved remaining order, invoked a safely shadowed `grub-mkconfig`, and set the reboot-required state. The minimal shell-to-argv reboot conversion was not deliberately rebooted.
- [x] `hetzner_vlan` — the real deploy and remove tags passed on two Ubuntu 26.04 guests attached to Hetzner VLAN 4000. Netplan created `ens18.4000` at `192.168.100.2/24` and `.3/24`, bidirectional pinned-interface pings passed 3/3 with 0% loss, both remove runs passed, and the VLAN YAML plus kernel links were verified absent afterward.
- [x] `iperf3` — normal host build/install completed and the converted native version parse displayed iperf3 3.21+.
- [x] `jackett` — normal first-install lifecycle completed, the container was observed running, and it was removed.
- [x] `jellyfin` — after deleting prior appdata, one clean install remained active while the current Jellyfin startup API completed the wizard; the same first-install settings block resumed, updated system/network XML, restarted successfully, and the container was removed.
- [x] `kernel` — the applicable Ubuntu 26.04 kernel-role lifecycle completed during the fresh minimal-to-core installation; conditional repair and reboot paths remained correctly unneeded.
- [x] `lidarr` — clean first-install authentication settings completed, the restarted container was observed running, and it was removed.
- [x] `lldap` — exercised through its real Authelia LDAP-backend import and reset lifecycle; role_var-backed paths rendered config, LLDAP reached healthy, and Authelia also reached healthy before the file backend was restored.
- [x] `mariadb` — clean LSIO 10.6.13 install and normal migration to `mariadb:10`; rows, grants, special-character data, dump retention, cleanup, explicit timeouts, and nonzero handling validated.
- [x] `mongodb` — offline FTDC detection identified restored MongoDB 6.0.21 data without a running database. Production-shaped acceptance passed standalone `6.0 -> 7.0 -> 8.0`, authenticated `4.4 -> 5.0 -> 6.0 -> 7.0 -> 8.0`, and `rs0` `6.0 -> 7.0 -> 8.0 -> 8.2` upgrades with records preserved and binary/FCV verified at every hop. Forced failure restored a byte-identical WiredTiger file, retained the cold backup, and left no failed container; same-target reruns, backup refusal, image/layout checks, custom-repository bypass, and effective-volume rejection also passed.
- [x] `motd` — the Python MOTD path generated a real config, then migrated a controlled Cloudbox/null-disk fixture; assertions confirmed the Saltbox banner, preserved unrelated data, and exact disk replacement semantics.
- [x] `netdata` — existing temp-container removal, forced copy-failure cleanup, normal config copy, healthy application startup, and post-test non-core container cleanup validated on Ubuntu 26.04.
- [x] `nginx` — normal first-install lifecycle completed, the container was observed running, and it was removed.
- [x] `node_exporter` — normal host install completed and `node_exporter.service` was confirmed active before being stopped to conserve guest memory.
- [x] `notify` — a real Apprise JSON notification reached a disposable local HTTP receiver with `$HOME`, `$()`, quotes, and spaces preserved exactly as one argv message; the shell-expression sentinel path was not created, and the receiver container was removed.
- [x] `nvidia` — scoped as requested to the edited nvtop output path: Ubuntu 26.04 nvtop emitted `nvtop version 3.2.0`, and the exact Ansible parsing expression resolved and asserted `3.2.0`; driver/kernel/purge behavior is not claimed.
- [x] `nzbget` — clean first-install settings and script lifecycle completed, the restarted container was observed running, and it was removed.
- [x] `nzbhydra2` — clean first-install settings lifecycle completed, the restarted container was observed running, and it was removed.
- [x] `nzbthrottle` — normal first-install imported its default configuration, the container was observed running, and it was removed.
- [x] `organizr` — normal first-install lifecycle completed, the container was observed running, and it was removed.
- [x] `overseerr` — normal first-install lifecycle completed, the container was observed running, and it was removed.
- [x] `permissions` — the normal `fix-permissions` tag executed all three converted recursive ownership commands successfully.
- [x] `petio` — normal first-install lifecycle completed with its instance-scoped `petio-mongo` dependency, Petio was observed running, and both non-core containers were removed.
- [x] `plex` — user-validated.
- [x] `plex_db` — user-validated.
- [x] `plex_extra_tasks` — user-validated.
- [x] `plex_fix_futures` — user-validated.
- [x] `portainer` — clean first-install container and setup/user creation completed, the container was observed running, and it was removed.
- [x] `postgres` — normal first-install resolved the edited defaults, created the database container, passed the PostgreSQL wait check, and the running container was removed.
- [x] `postgres_host` — fresh Ubuntu 26.04 minimal-to-core acceptance completed package installation without deadlock, removed only the package-default cluster, created the custom `seed` cluster at `/opt/postgresql/17/data`, rendered the standard systemd template, held `postgresql-17`, and preserved a real database row across a second full role run.
- [x] `pre_tasks` — both successful core passes exercised the native Git configuration lookup and safe-directory management paths before all other roles.
- [x] `prometheus` — normal install completed Prometheus plus its cAdvisor and node-exporter dependencies; Prometheus was observed running, both non-core containers were removed, and node-exporter was stopped.
- [x] `prowlarr` — clean first-install authentication settings completed, the restarted container was observed running, and it was removed.
- [x] `python` — normal role execution verified Ubuntu 26.04 system Python, installed Python 3.8 through uv, and verified the installed interpreter.
- [x] `qbittorrent` — native host-version lookup installed and ran qBittorrent v5.2.3 as a systemd service; Docker mode also installed and ran, and both test workloads were cleaned up.
- [x] `radarr` — clean first-install authentication settings completed, the restarted container was observed running, and it was removed.
- [x] `rclone` — the fresh core lifecycle completed binary discovery, extraction, installation, manpage handling, and the intentionally disabled configuration path.
- [x] `reboot` — user-approved validation for the minimal `shell: reboot` to literal `command.argv` conversion; an intentional VM reboot was not required.
- [x] `redis` — the role_var-backed path resolved in the normal core lifecycle and the retained Authelia Redis container is running.
- [x] `remote` — a restored rclone SFTP configuration passed direct access, then the normal post-restore `sb install core` lifecycle configured FUSE before Remote, started the generated systemd mount, and exposed the uploaded backup tree at `/mnt/remote/restoretest`; the mounted tar was byte-identical to the local copy.
- [x] `restore` — on a fresh Ubuntu 26.04 minimal VM, the official installer and Restore Service recovered eight source-matching configuration files, `preinstall` imported the rclone config, and `sb install restore` as the configured user consumed the SFTP-uploaded tar from the local destination; the restored sentinel and imported inventory retained their source hashes.
- [x] `sabnzbd` — clean first-install settings completed through the role_var-backed config path, the restarted container was observed running, and it was removed; the alternate web task uses the same edited path contract.
- [x] `sandbox` — after the intentional empty-path setup boundary was corrected, the normal core role cloned Sandbox and ran its hook initializer with native argv.
- [x] `sanity_check` — the successful core run exercised the edited Ansible-version, Git branch/hash, and CPU flag parsing paths on Ubuntu 26.04.
- [x] `seerr` — normal first-install lifecycle completed, the container was observed running, and it was removed.
- [x] `shell` — core/default lifecycle and a legacy command string containing literal `$HOME` passed through the real argcomplete argv consumer without expansion.
- [x] `sonarr` — clean first-install authentication settings completed, the restarted container was observed running, and it was removed.
- [x] `system` — the fresh minimal-to-core lifecycle completed the applicable APT, CPU, device, network, PAM, sysctl, and timezone paths on Ubuntu 26.04.
- [x] `tautulli` — clean first-install config generation and settings completed, the restarted container was observed running, and it was removed.
- [x] `timescaledb` — exercised through its real Sandbox Traccar importer; the role_var-backed path and caller overrides created `traccar-postgres`, its argv healthcheck reached healthy, Traccar ran, and both non-core containers were removed.
- [x] `traefik` — the prior focused CrowdSec URI probe plus the fresh core lifecycle completed configuration rendering, role_var-backed paths, container creation, and running status.
- [x] `transfer` — normal install completed container creation plus host binary installation; the native output parser displayed transfer 1.1.1, the container was observed running, and it was removed.
- [x] `unionfs` — the normal `mounts` lifecycle captured the native running-container list, stopped the retained core containers, rebuilt the applicable mount layer, and restarted all three core containers successfully.
- [x] `user` — the fresh core lifecycle exercised native group lookups and created the ordinary Saltbox user with the resolved video/render group IDs.
- [x] `whisparr` — clean first-install authentication settings completed, the restarted container was observed running, and it was removed.
- [x] `yyq` — normal role execution parsed and displayed the existing yyq 4.44.1 version with the converted native command path.

Saltbox role count: 81. Fully validated: 81. Not yet validated: 0.

## Sandbox roles

- [x] `cherry`
- [x] `code_server`
- [x] `filebrowser`
- [x] `firefox`
- [x] `forgejo`
- [x] `gitea`
- [x] `jdownloader2`
- [x] `jellystat` — normal first-install lifecycle completed; Jellystat and its instance-scoped PostgreSQL dependency both reached healthy and were removed.
- [x] `karakeep` — normal first-install lifecycle completed; Karakeep reached healthy with Chrome and Meilisearch, then all three containers were removed.
- [x] `koel`
- [x] `koito_migrate` — formatting-only validation; the edited `role_depends_on` Jinja expression was split across source lines without changing the rendered value or control flow.
- [x] `linkwarden` — normal first-install lifecycle completed; Linkwarden and its instance-scoped PostgreSQL dependency both reached healthy and were removed.
- [x] `n8n` — normal first-install lifecycle completed with its runner and PostgreSQL dependency; all three containers ran and were removed.
- [x] `notifiarr` — clean config generation completed; the container was observed running with zero restarts and was removed.
- [x] `paperless_ngx` — normal first-install lifecycle completed; Paperless reached healthy with Tika, Gotenberg, PostgreSQL, and Redis, then all five containers were removed.
- [x] `plex_auto_languages` — user-validated as part of all edited Plex tasks.
- [x] `plex_meta_manager` — user-validated as part of all edited Plex tasks.
- [x] `plexshare` — user-validated as part of all edited Plex tasks.
- [x] `plextraktsync` — user-validated as part of all edited Plex tasks.
- [x] `profilarr` — normal first-install lifecycle completed; the container was observed running with zero restarts and was removed.
- [x] `rocketchat` — the full role passed with Rocket.Chat 8.7.1 connected to MongoDB 8.2.12, while a production-shaped `rs0` database preserved its record through the validated `6.0 -> 7.0 -> 8.0 -> 8.2` binary and FCV path. MongoDB finished primary at FCV 8.2, and Rocket.Chat reached `SERVER RUNNING`.
- [x] `rutorrent` — clean first-install and post-install settings completed; the restarted container was observed running with zero restarts and was removed.
- [x] `sanity_check` — edited Sandbox Ansible-version and repository checks ran successfully across every completed Sandbox role lifecycle on the current candidate.
- [x] `shelfmark` — normal first-install lifecycle completed; the container was observed running with zero restarts and was removed.
- [x] `silo` — normal first-install lifecycle completed; Silo, PostgreSQL, and Redis reached healthy/running state and all three were removed.
- [x] `slskd` — clean config generation completed; the container was observed running with zero restarts and was removed.
- [x] `sshwifty` — clean JSON config generation completed; the container was observed running with zero restarts and was removed.
- [x] `stash` — a normal role run used a controlled UI-generated `config.yml`, created the real container, resolved both role_var paths, completed both native `yyq` edits, and restarted Stash running with zero restarts before cleanup.
- [x] `tauticord` — the role's expected first-run lifecycle completed, displayed the documented user configuration notice, and the container ran with zero restarts before removal.
- [x] `telegraf` — normal config generation and container lifecycle completed; the container ran with zero restarts and was removed.
- [x] `tqm` — normal role acceptance used a real qBittorrent host endpoint and valid current config; TQM 1.20.0 downloaded, every role_var-backed path rendered, the oneshot service retrieved zero torrents and exited successfully, and the timer became active before cleanup.
- [x] `transmission`
- [x] `trilium` — normal first-install lifecycle completed; the container ran with zero restarts and was removed.
- [x] `tubearchivist` — normal first-install lifecycle completed; TubeArchivist, Elasticsearch, and Redis all ran with zero restarts and were removed.
- [x] `unifi_network_application` — the full role passed after the final MongoDB bind validation change. Its authenticated MongoDB container finished on 8.0 with FCV 8.0, the UniFi container was recreated successfully, and the local HTTPS endpoint returned `302`.
- [x] `varken` — the role now fails before dependency or container changes when the MaxMind key required by the bundled image is empty, while CI explicitly skips the hard failure. The edited config task also queried a real Ombi-shaped SQLite row with native `sqlite3` JSON extraction and rendered the expected API key into `varken.ini`.
- [x] `vaultwarden` — a fresh Ubuntu 26.04 minimal-to-core lifecycle generated the Admin token with the configured Vaultwarden 1.37.2 image, stored only its Argon2id PHC hash in the upstream-aligned env, displayed the plaintext once, and authenticated it successfully at `/admin`. Vaultwarden was healthy with Rocket and Traefik on port 80; a repeat role run skipped token/env generation, preserved the env SHA-256 exactly, displayed no token, and retained successful Admin authentication.
- [x] `wireguard` — normal first-install network/container lifecycle completed; the privileged container ran with zero restarts and was removed.
- [x] `wizarr` — a genuine 4.2.0 container database and invitation passed the implemented bridge migration through pinned 2025.6.1 and current v2026.7.1. The role retained the timestamped original DB, verified bridge revision `56b33a2ca88e`, resumed cleanly after an interrupted validation step, reached current revision `20260401_repair` healthy with zero restarts, preserved the invitation, restored recursive `seed` ownership, removed the bridge container, and passed an idempotent repeat run without creating another backup.
- [x] `ytdl_sub` — normal first-install lifecycle completed; the container ran with zero restarts and was removed.

Sandbox role count: 40. Fully validated: 40. Not yet validated: 0.

## MongoDB upgrade completion

- The generic role derives the last MongoDB binary version from restored FTDC
  metadata without starting the old database or requiring callers to supply a
  source version.
- The validated matrix is `4.4 -> 5.0 -> 6.0 -> 7.0 -> 8.0 -> 8.2`. Every hop
  deploys the normal container, waits for a writable standalone or replica-set
  primary, applies the required FCV, and verifies both binary and FCV.
- Cross-series upgrades retain one cold `<data path>_backup`, refuse to
  overwrite it, restore it after an Ansible-caught failure, and require manual
  removal before another cross-series upgrade.
- The role rejects unknown paths, downgrades, unsafe kernels, image series or
  layout drift, partial root credentials, path symlinks, and effective data
  bindings that do not match `mongodb_role_paths_location`.
- The final full static gates and production-shaped MongoDB, Rocket.Chat, and
  UniFi acceptance passed. The independent focused review reported no remaining
  issues.

## Shared work and final gates

- [x] Saltbox shared `resources/` changes
- [x] Saltbox inventory changes
- [x] Saltbox linter and `.ansible-lint` changes
- [x] Sandbox `.ansible-lint` changes
- [x] Saltbox full linter, Ansible lint, syntax, and `git diff --check` gates.
- [x] Sandbox full linter, Ansible lint, syntax, and `git diff --check` gates.
- [x] Final edited-role list recounted from both worktrees and reconciled with this file
- [x] Final VM state inspected after MongoDB acceptance — `test-a`, `test-b`, and `proxmox-runner` are absent.
