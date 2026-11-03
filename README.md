# Adrenaline CNA Loader

This repository contains only the custom Cobalt Strike Aggressor Script (`.cna`) loader.

The Adrenaline project and its BOF source/binaries are **not included**. The BOFs, project structure, and associated functionality belong to [atomiczsec/Adrenaline](https://github.com/atomiczsec/Adrenaline). Obtain those files from the upstream project and place them alongside this loader using the expected relative paths.

## Loading

1. Obtain and build/download the required Adrenaline BOFs from the upstream repository.
2. Keep the BOFs in the directory structure expected by the CNA script.
3. In Cobalt Strike, open **Script Manager → Load** and select the CNA file.
4. Run `ad_help` in a Beacon console to display the command summary.

The loader selects the BOF matching the Beacon architecture (`.x86.o` or `.x64.o`) and reports missing files in Beacon output.

## Commands

### Collection and user data

```text
ad_ai_surface
ad_clipboard_grab
ad_ide_extension_surface
ad_powershell_history
ad_window_handles_enum
ad_notepad_grab run
ad_notepad_grab <title_filter>
ad_session_view
ad_window_list titles
ad_window_list /pid
ad_tray_scout normal
ad_tray_scout verbose
ad_user_idle
ad_wallpaper_enum
```

### Discovery and host configuration

```text
ad_app_count
ad_applocker_policy
ad_amsi_etw_detect
ad_asr_status
ad_bitlocker_status
ad_mdm_policy_artifacts
ad_netjoin_query
ad_power_state
ad_proxy_enum
ad_wef_detect
ad_win_version
ad_wsc_status
ad_schtask_enum local
ad_schtask_enum <server>
```

### Credential and token-related checks

```text
ad_certstore_loot all
ad_certstore_loot <store_name> <location>
ad_cicd_credential_hunt presence
ad_cicd_credential_hunt verbose
ad_process_tokens_list all
ad_process_tokens_list [pid|process_name] [/debug|/enablesebug]
ad_cloud_metadata_check full
ad_cloud_metadata_check presence [-aud arm|graph|other:<resource>|other <resource>]
```

### Networking, services, and execution

```text
ad_net_use list [target]
ad_net_use add <unc_share> [username] [password] [device] [persist] [require_privacy]
ad_net_use delete <target> [persist] [force]
ad_com_probe <CLSID> [IID]
ad_firewall_rule list
ad_firewall_rule query <name>
ad_firewall_rule remove <name>
ad_firewall_rule add <name> <dir> <action> <protocol> [localport] [remoteport] [profile]
ad_port_scan <target> [ports] [protocol] [timeout_ms]
ad_service_control query [service_name]
ad_service_control create <service_name> <bin_path> [display_name] [start_type] [service_type] [error_control]
ad_service_control start <service_name>
ad_service_control stop <service_name>
ad_service_control delete <service_name>
ad_service_control failure <service_name> <reset_seconds> [reboot_msg] [command] [actions]
```

Run an argument-aware command without arguments, or pass `help`, `-h`, `--help`, `/h`, `/?`, or `?`, to display its syntax card.

## Examples

### Display the command summary

```text
beacon> ad_help
[Adrenaline] Available commands:
  ad_win_version
  ad_process_tokens_list
  ad_firewall_rule
  ad_service_control
  ...
```

### Query the Windows version

```text
beacon> ad_win_version
[Adrenaline] Windows version information:
  Product name : Windows 11 Enterprise
  Version      : 10.0.22631
  Build        : 22631
  Architecture : x64
```

### List firewall rules

```text
beacon> ad_firewall_rule list
[Adrenaline] Firewall rules:
  Name                         Direction  Action  Enabled  Profile
  -----------------------------------------------------------------
  Core Networking - DNS (UDP)  Inbound    Allow   Yes      All
  File and Printer Sharing     Inbound    Allow   No       Domain
```

Output varies by Beacon architecture, Windows version, local policy, and the
command arguments supplied. The examples above show representative output.

## Scope and authorization

Use this loader and the upstream Adrenaline BOFs only on Beacons and systems for which you have explicit authorization. Several commands can expose credentials or sensitive data, or change firewall, service, and network configuration.

## Disclaimer

For educational and authorized testing only. Use only with explicit permission. The authors assume no liability for misuse.

---

## Author

- 💀 **B5null**
