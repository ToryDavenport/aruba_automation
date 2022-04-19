# httpie example usage with AOSCX REST API

### Install HTTPie

```bash
apt install httpie
```

In this example I will use the rest API on the Aruba CX switch:

### LOGIN TO THE SWITCH VIA API

Here we issue a POST to the url using basic authentication.

--verify NO  --> Disable SSL verification

--session mysesh --> Store authentication in a session

```bash
http POST 'https://10.251.11.103/rest/v10.04/login?username=admin&password=aruba123' --verify NO --session mysesh
```

*Example Output*
```bash 
root@ubuntu:/home/student/TORY# http POST 'https://10.251.11.103/rest/v10.04/login?username=admin&password=aruba123' --verify NO --session mysesh
HTTP/1.1 200 OK
Connection: keep-alive
Content-Length: 0
Content-Security-Policy: script-src 'self' 'unsafe-inline'; object-src 'none'; font-src *; media-src 'none'; form-action 'self';
Date: Tue, 19 Apr 2022 16:51:52 GMT
Server: nginx
Set-Cookie: id=yuTYx9tAz_siupSro9MM7A==; Path=/; HttpOnly; Secure
Set-Cookie: user=eyJ1c2VyIjoiYWRtaW4iLCJsZXZlbCI6MTUsInR5cGUiOiJMT0NBTCIsIm1ldGhvZCI6IkxPQ0FMIn0=; Path=/; Secure
Strict-Transport-Security: max-age=31536000; includeSubdomains;
X-Content-Type-Options: nosniff
X-Frame-Options: SAMEORIGIN
X-XSS-Protection: 1; mode=block
```

### GET the list of VLANS
```bash
http GET https://10.251.11.103/rest/v10.04/system/vlans --verify NO --session mysesh
```

*Example use*
```bash
root@ubuntu:/home/student/TORY# http GET https://10.251.11.103/rest/v10.04/system/vlans --verify NO --session mysesh
HTTP/1.1 200 OK
Connection: keep-alive
Content-Length: 124
Content-Security-Policy: script-src 'self' 'unsafe-inline'; object-src 'none'; font-src *; media-src 'none'; form-action 'self';
Content-Type: application/json; charset=utf-8
Date: Tue, 19 Apr 2022 17:00:25 GMT
Etag: b29e01bbb1db3b228a5f040fd5388fed
Server: nginx
Strict-Transport-Security: max-age=31536000; includeSubdomains;
X-Content-Type-Options: nosniff
X-Frame-Options: SAMEORIGIN
X-XSS-Protection: 1; mode=block

{
    "1": "/rest/v10.04/system/vlans/1",
    "115": "/rest/v10.04/system/vlans/115",
    "116": "/rest/v10.04/system/vlans/116"
}
```

### POST a new VLAN to the config
First we will need to setup a file *payload.json* to contain the JSON request.

```json
{"id": 999,"name": "BLACKHOLE VLAN"}
```

Next we will issue POST and specify the file with the JSON we want to send using the < redirect, specifying json with -j

```bash
http POST https://10.251.11.103/rest/v10.04/system/vlans --verify NO --session mysesh -j < payload.json 
```

*Example use*
```bash
root@ubuntu:/home/student/TORY# http POST https://10.251.11.103/rest/v10.04/system/vlans --verify NO --session mysesh -j < payload.json
HTTP/1.1 201 Created
Connection: keep-alive
Content-Length: 0
Content-Security-Policy: script-src 'self' 'unsafe-inline'; object-src 'none'; font-src *; media-src 'none'; form-action 'self';
Date: Tue, 19 Apr 2022 17:05:09 GMT
Location: /rest/v10.04/system
Server: nginx
Strict-Transport-Security: max-age=31536000; includeSubdomains;
X-Content-Type-Options: nosniff
X-Frame-Options: SAMEORIGIN
X-XSS-Protection: 1; mode=block
```

### DELETE a VLAN
```bash
http DELETE https://10.251.11.103/rest/v10.04/system/vlans/999 --verify NO --session mysesh
```

*Example use*
```bash
root@ubuntu:/home/student/TORY# http DELETE https://10.251.11.103/rest/v10.04/system/vlans/999 --verify NO --session mysesh
HTTP/1.1 204 No Content
Connection: keep-alive
Content-Security-Policy: script-src 'self' 'unsafe-inline'; object-src 'none'; font-src *; media-src 'none'; form-action 'self';
Date: Tue, 19 Apr 2022 16:59:10 GMT
Server: nginx
Strict-Transport-Security: max-age=31536000; includeSubdomains;
X-Content-Type-Options: nosniff
X-Frame-Options: SAMEORIGIN
X-XSS-Protection: 1; mode=block
```

### GET All Interfaces
```bash
http GET https://10.251.11.103/rest/v10.04/system/interfaces --verify NO --session mysesh
```

*Example use*
```bash
root@ubuntu:/home/student/TORY# http GET https://10.251.11.103/rest/v10.04/system/interfaces --verify NO --session mysesh
HTTP/1.1 200 OK
Connection: keep-alive
Content-Length: 1686
Content-Security-Policy: script-src 'self' 'unsafe-inline'; object-src 'none'; font-src *; media-src 'none'; form-action 'self';
Content-Type: application/json; charset=utf-8
Date: Tue, 19 Apr 2022 17:08:08 GMT
Etag: 9ad9a79d143410de2319e79d5058b01a
Server: nginx
Strict-Transport-Security: max-age=31536000; includeSubdomains;
X-Content-Type-Options: nosniff
X-Frame-Options: SAMEORIGIN
X-XSS-Protection: 1; mode=block

{
    "1/1/1": "/rest/v10.04/system/interfaces/1%2F1%2F1",
    "1/1/10": "/rest/v10.04/system/interfaces/1%2F1%2F10",
    "1/1/11": "/rest/v10.04/system/interfaces/1%2F1%2F11",
    "1/1/12": "/rest/v10.04/system/interfaces/1%2F1%2F12",
    "1/1/13": "/rest/v10.04/system/interfaces/1%2F1%2F13",
    "1/1/14": "/rest/v10.04/system/interfaces/1%2F1%2F14",
    "1/1/15": "/rest/v10.04/system/interfaces/1%2F1%2F15",
    "1/1/16": "/rest/v10.04/system/interfaces/1%2F1%2F16",
    "1/1/17": "/rest/v10.04/system/interfaces/1%2F1%2F17",
    "1/1/18": "/rest/v10.04/system/interfaces/1%2F1%2F18",
    "1/1/19": "/rest/v10.04/system/interfaces/1%2F1%2F19",
    "1/1/2": "/rest/v10.04/system/interfaces/1%2F1%2F2",
    "1/1/20": "/rest/v10.04/system/interfaces/1%2F1%2F20",
    "1/1/21": "/rest/v10.04/system/interfaces/1%2F1%2F21",
    "1/1/22": "/rest/v10.04/system/interfaces/1%2F1%2F22",
    "1/1/23": "/rest/v10.04/system/interfaces/1%2F1%2F23",
    "1/1/24": "/rest/v10.04/system/interfaces/1%2F1%2F24",
    "1/1/25": "/rest/v10.04/system/interfaces/1%2F1%2F25",
    "1/1/26": "/rest/v10.04/system/interfaces/1%2F1%2F26",
    "1/1/27": "/rest/v10.04/system/interfaces/1%2F1%2F27",
    "1/1/28": "/rest/v10.04/system/interfaces/1%2F1%2F28",
    "1/1/3": "/rest/v10.04/system/interfaces/1%2F1%2F3",
    "1/1/4": "/rest/v10.04/system/interfaces/1%2F1%2F4",
    "1/1/5": "/rest/v10.04/system/interfaces/1%2F1%2F5",
    "1/1/6": "/rest/v10.04/system/interfaces/1%2F1%2F6",
    "1/1/7": "/rest/v10.04/system/interfaces/1%2F1%2F7",
    "1/1/8": "/rest/v10.04/system/interfaces/1%2F1%2F8",
    "1/1/9": "/rest/v10.04/system/interfaces/1%2F1%2F9",
    "vlan1": "/rest/v10.04/system/interfaces/vlan1",
    "vlan115": "/rest/v10.04/system/interfaces/vlan115"
}
```

### GET Specific Interface
```bash
http GET https://10.251.11.103/rest/v10.04/system/interfaces/1%2F1%2F1 --verify NO --session mysesh
```

*Example use*
```bash
root@ubuntu:/home/student/TORY# http GET https://10.251.11.103//rest/v10.04/system/interfaces/1%2F1%2F1--verify NO --session mysesh
HTTP/1.1 200 OK
Connection: keep-alive
Content-Security-Policy: script-src 'self' 'unsafe-inline'; object-src 'none'; font-src *; media-src 'none'; form-action 'self';
Content-Type: application/json; charset=utf-8
Date: Tue, 19 Apr 2022 17:09:02 GMT
Etag: 49ba1a9df608ea190293d0fd2020aade
Server: nginx
Strict-Transport-Security: max-age=31536000; includeSubdomains;
Transfer-Encoding: chunked
X-Content-Type-Options: nosniff
X-Frame-Options: SAMEORIGIN
X-XSS-Protection: 1; mode=block
{
  "aaa_auth_precedence": {},
  "acl_init_status": "success",
  "aclmac_in_applied": null,
  "aclmac_in_cfg": null,
  "aclmac_in_cfg_version": null,
  "aclmac_in_statistics": {},
  "aclmac_in_status": {},
  "aclmac_out_applied": null,
  "aclmac_out_cfg": null,
  "aclmac_out_cfg_version": null,
  "aclmac_out_statistics": {},
  "aclmac_out_status": {},
  "aclv4_in_applied": null,
  "aclv4_in_cfg": null,
  "aclv4_in_cfg_version": null,
  "aclv4_in_statistics": {},
  "aclv4_in_status": {},
  "aclv4_out_applied": null,
  "aclv4_out_cfg": null,
  "aclv4_out_cfg_version": null,
  "aclv4_out_statistics": {},
  "aclv4_out_status": {},
  "aclv4_routed_in_applied": null,
  "aclv4_routed_in_cfg": null,
  "aclv4_routed_in_cfg_version": null,
  "aclv4_routed_in_statistics": {},
  "aclv4_routed_in_status": {},
  "aclv4_routed_in_subsystem_states": {},
  "aclv4_routed_out_applied": null,
  "aclv4_routed_out_cfg": null,
  "aclv4_routed_out_cfg_version": null,
  "aclv4_routed_out_statistics": {},
  "aclv4_routed_out_status": {},
  "aclv4_routed_out_subsystem_states": {},
  "aclv6_in_applied": null,
  "aclv6_in_cfg": null,
  "aclv6_in_cfg_version": null,
  "aclv6_in_statistics": {},
  "aclv6_in_status": {},
  "aclv6_out_applied": null,
  "aclv6_out_cfg": null,
  "aclv6_out_cfg_version": null,
  "aclv6_out_statistics": {},
  "aclv6_out_status": {},
  "aclv6_routed_in_applied": null,
  "aclv6_routed_in_cfg": null,
  "aclv6_routed_in_cfg_version": null,
  "aclv6_routed_in_statistics": {},
  "aclv6_routed_in_status": {},
  "aclv6_routed_in_subsystem_states": {},
  "aclv6_routed_out_applied": null,
  "aclv6_routed_out_cfg": null,
  "aclv6_routed_out_cfg_version": null,
  "aclv6_routed_out_statistics": {},
  "aclv6_routed_out_status": {},
  "aclv6_routed_out_subsystem_states": {},
  "active_ip4_address": null,
  "active_ip4_address_secondary": [],
  "active_ip_mtu": {},
  "admin": "down",
  "admin_state": "down",
  "applied_extended_access_vlans": [],
  "applied_vlan_mode": "access",
  "applied_vlan_tag": {
    "1": "/rest/v10.04/system/vlans/1"
  },
  "applied_vlan_trunks": [],
  "applied_vlans_per_protocol": {},
  "arp_inspection": {
    "trust": false
  },
  "arp_timeout": 1800,
  "asic_config_state": {
    "asic_config_state_down_reason": "waiting",
    "ready": false
  },
  "bfd_detect_multiplier": -1,
  "bfd_echo_disable": false,
  "bfd_min_rx_interval": -1,
  "bfd_min_tx_interval": -1,
  "bond_active_slave": null,
  "bond_mode": null,
  "bond_status": {},
  "capabilities": [
    "cable_diagnostics",
    "internal_prbs_loopback",
    "poe_plus_power",
    "speed_downshift"
  ],
  "capacities_status": {},
  "ccm_state": "up",
  "cdp_disable": false,
  "cdp_neighbors": "/rest/v10.04/system/interfaces/1%2F1%2F1/cdp_neighbors",
  "cdp_statistics": {},
  "clear_ip_bindings": {},
  "client_ip_track_configuration": {
    "admin_state": "auto",
    "client_limit": 128,
    "update_interval": 1800
  },
  "coa_bounce": false,
  "description": null,
  "device_profile": {},
  "dhcp_config": {},
  "dhcp_info": {},
  "dhcp_relay_statistics": {},
  "dhcpv4_snooping_configuration": {
    "max_bindings": 8192,
    "trusted": false
  },
  "dhcpv6_snooping_configuration": {
    "max_bindings": 8192,
    "trusted": false
  },
  "dot1x_authenticator_statistics": {},
  "dot1x_status": null,
  "duplex": "full",
  "dyn_trunks": [],
  "dynamic_ip_mtu": {},
  "egress_blocked_to_ports": [],
  "egress_redirect_to_port": null,
  "erps_port_blocked": null,
  "error": "Administratively down",
  "error_control": "none",
  "evpn_force_shutdown": false,
  "fault_monitor_fault_status": {},
  "fault_monitor_force_shutdown": {},
  "fault_monitor_profile": null,
  "flaps_performed": 0,
  "flaps_requested": 0,
  "flood_block": null,
  "forwarding_state": {
    "aggregation_layer": false,
    "availability": true,
    "availability_layer": true,
    "block_mode": "BLOCK",
    "blocking_layer": "ENABLEMENT",
    "blocking_trigger": "USER_INTENT",
    "enablement": false,
    "enablement_layer": false,
    "forwarding": false,
    "health_layer": false,
    "loop_protection_layer": false,
    "operational": false,
    "operational_layer": false,
    "security_layer": false
  },
  "hw_intf_info": {
    "bridge": false,
    "card_intf_number": 1,
    "connector": "RJ45",
    "description": "1GbT",
    "mac_addr": "64:e8:81:dd:27:67",
    "max_speed": "1000",
    "pluggable": "false",
    "speeds": "10,100,1000",
    "switch_intf_id": "25",
    "switch_unit": "0"
  },
  "icmp_redirect_disable": false,
  "icmp_unreachable_disable": false,
  "icmp_unreachable_ratelimit": 1000,
  "ifindex": 1,
  "interface_diag_tests": "/rest/v10.04/system/interfaces/1%2F1%2F1/interface_diag_tests",
  "interfaces": {
    "1/1/1": "/rest/v10.04/system/interfaces/1%2F1%2F1"
  },
  "ip4_address": null,
  "ip4_address_secondary": [],
  "ip6_address_custom_link_local": "/rest/v10.04/system/interfaces/1%2F1%2F1/ip6_address_custom_link_local",
  "ip6_address_link_local": {},
  "ip6_addresses": "/rest/v10.04/system/interfaces/1%2F1%2F1/ip6_addresses",
  "ip6_autoconfigured_addresses": "/rest/v10.04/system/interfaces/1%2F1%2F1/ip6_autoconfigured_addresses",
  "ip_directed_broadcast": false,
  "ip_mtu": 1500,
  "ipv4_source_lockdown_enable": false,
  "ipv4_source_lockdown_hw_status": {
    "hw_enabled": "not-applicable"
  },
  "ipv6_address_autoconfig_enable": false,
  "ipv6_address_linklocal_enable": false,
  "ipv6_icmpv6_pkts_statistics": {},
  "ipv6_nd_dad_attempts": 1,
  "ipv6_nd_icmpv6_redirects": false,
  "ipv6_nd_icmpv6_timestamp": {},
  "ipv6_nd_mtu": 1500,
  "ipv6_nd_ns_interval": 1000,
  "ipv6_nd_prefix_default": {
    "no-advertise": false,
    "no-autoconfig": false,
    "no-onlink": false,
    "preferred_lifetime": 604800,
    "valid_lifetime": 2592000
  },
  "ipv6_nd_ra_dnssl": {},
  "ipv6_nd_ra_hoplimit": null,
  "ipv6_nd_ra_lifetime": 1800,
  "ipv6_nd_ra_managed_flag": false,
  "ipv6_nd_ra_max_interval": 600,
  "ipv6_nd_ra_min_interval": 200,
  "ipv6_nd_ra_other_config_flag": false,
  "ipv6_nd_ra_rdnss": {},
  "ipv6_nd_ra_reachable_time": 0,
  "ipv6_nd_ra_retransmit_timer": 0,
  "ipv6_nd_router_preference": "medium",
  "ipv6_nd_suppress_ra": {
    "all": true,
    "dnssl": false,
    "mtu": false,
    "rdnss": false
  },
  "ipv6_neighbor_timeout": 1800,
  "ipv6_ra_counters": {},
  "ipv6_source_lockdown_enable": false,
  "ipv6_source_lockdown_hw_status": {
    "hw_enabled": "not-applicable"
  },
  "l1_current_state": "inactive",
  "l1_next_state": "inactive",
  "l1_state": {
    "l1_state_down_reason": "admin_down",
    "ready": false
  },
  "l1_state_aggregate": {
    "l1_state_aggregate_down_reason": "waiting",
    "ready": false
  },
  "l3_counters_enable": {
    "rx": false,
    "tx": false
  },
  "lacp": null,
  "lacp_current": null,
  "lacp_statistics": {},
  "lacp_status": {},
  "link_errors": 0,
  "link_partner_capabilities": {
    "25gbase-cr": false,
    "25gbase-cr-s": false,
    "base-r-fec": false,
    "pause": "none",
    "rs-fec": false
  },
  "link_resets": 0,
  "link_speed": 0,
  "link_state": "down",
  "link_state_aggregate": {
    "link_state_aggregate_down_reason": "waiting",
    "ready": false
  },
  "link_state_hw": {
    "link_state_hw_down_reason": "waiting",
    "ready": false
  },
  "lldp_med_loc_civic_ca_info": {},
  "lldp_med_loc_civic_info": null,
  "lldp_med_loc_elin_info": null,
  "lldp_neighbors": "/rest/v10.04/system/interfaces/1%2F1%2F1/lldp_neighbors",
  "lldp_statistics": {},
  "loop_detect_source": null,
  "loop_detected": false,
  "loop_protect_action": null,
  "loop_protect_enable": null,
  "loop_protect_port_disabled": null,
  "loop_protect_stagger_count": 1,
  "loop_protect_statistics": {},
  "loop_protect_status": {},
  "loop_protect_vlan": [],
  "mac": null,
  "mac_auth_statistics": {},
  "mac_in_use": "64:e8:81:dd:27:67",
  "mac_learn_disable": null,
  "macs_invalid": null,
  "macs_invalid_on_vlans": [],
  "mdi_mode": null,
  "mep_id": null,
  "mgmd_acl": {},
  "mgmd_counters": {},
  "mgmd_dynamic_group_count": {},
  "mgmd_enable": {},
  "mgmd_enable_status": {},
  "mgmd_igmp_static_groups": [],
  "mgmd_igmp_version": null,
  "mgmd_last_member_query_interval": {},
  "mgmd_mld_static_groups": [],
  "mgmd_mld_version": null,
  "mgmd_oper_version": {},
  "mgmd_pgs": "/rest/v10.04/system/interfaces/1%2F1%2F1/mgmd_pgs",
  "mgmd_querier_enable": {},
  "mgmd_querier_interval": {},
  "mgmd_querier_ip": {},
  "mgmd_querier_max_response_time": {},
  "mgmd_querier_state": {},
  "mgmd_querier_timer_info": {},
  "mgmd_robustness": {},
  "mgmd_snoop_fastlearn_enable": {},
  "mgmd_strict_version_enable": {},
  "mstp_force_shutdown": false,
  "mtu": 1500,
  "multicast_l3_neighbor_forwardings": "/rest/v10.04/system/interfaces/1%2F1%2F1/multicast_l3_neighbor_forwardings",
  "mvrp_enable": false,
  "mvrp_forbidden_vlans": [],
  "mvrp_last_pdu_src_mac": null,
  "mvrp_registration": "normal",
  "mvrp_statistics": {},
  "mvrp_timers": {
    "join": 20,
    "leave": 300,
    "leaveall": 1000,
    "periodic": 100
  },
  "mvrp_vlans": "/rest/v10.04/system/interfaces/1%2F1%2F1/mvrp_vlans",
  "name": "1/1/1",
  "nd_snooping_configuration": {
    "max_bindings": 16384,
    "trusted": false
  },
  "num_clear_sflow_stats_performed": null,
  "num_clear_sflow_stats_requested": null,
  "num_clear_stats_performed": null,
  "num_clear_stats_requested": null,
  "options": {
    "vxlan_dest_udp_port": "4789"
  },
  "origin": "built-in",
  "ospf_auth_keychain": null,
  "ospf_auth_md5_keys": {},
  "ospf_auth_text_key": null,
  "ospf_auth_type": null,
  "ospf_bfd": "default",
  "ospf_if_out_cost": null,
  "ospf_if_shutdown": false,
  "ospf_if_type": null,
  "ospf_intervals": {
    "dead_interval": 40,
    "hello_interval": 10,
    "retransmit_interval": 5,
    "transmit_delay": 1
  },
  "ospf_neighbor_clear_performed": 0,
  "ospf_neighbor_clear_requested": 0,
  "ospf_priority": 1,
  "ospfv3_bfd": "default",
  "ospfv3_dead_interval": 40,
  "ospfv3_hello_interval": 10,
  "ospfv3_if_cost": null,
  "ospfv3_if_priority": 1,
  "ospfv3_if_shutdown": false,
  "ospfv3_if_type": null,
  "ospfv3_ipsec_ah": {
    "ah_null": false
  },
  "ospfv3_ipsec_esp": {
    "esp_null": false
  },
  "ospfv3_neighbor_clear_performed": 0,
  "ospfv3_neighbor_clear_requested": 0,
  "ospfv3_retransmit_interval": 5,
  "ospfv3_transmit_delay": 1,
  "other_config": {
    "lldp_dot3_macphy_disable": false,
    "lldp_dot3_poe_disable": false,
    "lldp_med_capability_disable": false,
    "lldp_med_network_policy_disable": false,
    "lldp_med_poe_disable": false,
    "lldp_med_poe_priority_override": false,
    "lldp_med_topology_notification_disable": false
  },
  "pause": "none",
  "pfc_priorities_applied": null,
  "pfc_priorities_config": null,
  "physical_interface_state": "ready",
  "pim_bfd": {},
  "pim_dense_graft_retry_interval": {},
  "pim_dense_max_graft_retries": {},
  "pim_dense_ttl_threshold": {},
  "pim_dr_priority": {},
  "pim_elected_dr_address": {},
  "pim_hello_interval": {},
  "pim_ipv4_packet_counters": {},
  "pim_ipv4_pending_starg_sg_entries": [],
  "pim_ipv6_packet_counters": {},
  "pim_ipv6_pending_starg_sg_entries": [],
  "pim_lan_prune_delay_disable": {},
  "pim_mode": {
    "ipv4": "disabled",
    "ipv6": "disabled"
  },
  "pim_mroutes": "/rest/v10.04/system/interfaces/1%2F1%2F1/pim_mroutes",
  "pim_neighbors": "/rest/v10.04/system/interfaces/1%2F1%2F1/pim_neighbors",
  "pim_operational": {},
  "pim_override_interval": {},
  "pim_propagation_delay": {},
  "pim_proxy_dr": {
    "ipv4": false,
    "ipv6": false
  },
  "pim_source_address": {},
  "pim_trig_hello_interval": {},
  "pm_info": {
    "dom_supported": false,
    "external_connector": "unknown",
    "formfactor": "unknown",
    "om1_transfer_distance": 0,
    "om2_transfer_distance": 0,
    "om3_transfer_distance": 0,
    "reset_state": "asserted",
    "rx1_los_state": "asserted",
    "rx2_los_state": "asserted",
    "rx3_los_state": "asserted",
    "rx4_los_state": "asserted",
    "rx_los_state": "asserted",
    "smf_transfer_distance": 0,
    "tx1_fault_state": "asserted",
    "tx1_los_state": "asserted",
    "tx1_power_high_alarm": "Off",
    "tx1_power_high_warning": "Off",
    "tx1_power_low_alarm": "Off",
    "tx1_power_low_warning": "Off",
    "tx2_fault_state": "asserted",
    "tx2_los_state": "asserted",
    "tx2_power_high_alarm": "Off",
    "tx2_power_high_warning": "Off",
    "tx2_power_low_alarm": "Off",
    "tx2_power_low_warning": "Off",
    "tx3_fault_state": "asserted",
    "tx3_los_state": "asserted",
    "tx3_power_high_alarm": "Off",
    "tx3_power_high_warning": "Off",
    "tx3_power_low_alarm": "Off",
    "tx3_power_low_warning": "Off",
    "tx4_fault_state": "asserted",
    "tx4_los_state": "asserted",
    "tx4_power_high_alarm": "Off",
    "tx4_power_high_warning": "Off",
    "tx4_power_low_alarm": "Off",
    "tx4_power_low_warning": "Off",
    "tx_disable_state": "asserted",
    "tx_fault_state": "asserted"
  },
  "pm_state": "DEFAULT",
  "poe_interface": "/rest/v10.04/system/interfaces/1%2F1%2F1/poe_interface",
  "policy_in_applied": null,
  "policy_in_cfg": null,
  "policy_in_cfg_version": null,
  "policy_in_conform_rate": {},
  "policy_in_statistics": {},
  "policy_in_status": {},
  "policy_init_status": "success",
  "policy_out_applied": null,
  "policy_out_cfg": null,
  "policy_out_cfg_version": null,
  "policy_out_conform_rate": {},
  "policy_out_statistics": {},
  "policy_out_status": {},
  "policy_routed_in_applied": null,
  "policy_routed_in_cfg": null,
  "policy_routed_in_cfg_version": null,
  "policy_routed_in_conform_rate": {},
  "policy_routed_in_statistics": {},
  "policy_routed_in_status": {},
  "policy_routed_in_subsystem_states": {},
  "port_access_allow_bpdu": [],
  "port_access_allow_flood_traffic": false,
  "port_access_auth_configurations": "/rest/v10.04/system/interfaces/1%2F1%2F1/port_access_auth_configurations",
  "port_access_auth_mode": "client-mode",
  "port_access_auth_role": null,
  "port_access_clients": "/rest/v10.04/system/interfaces/1%2F1%2F1/port_access_clients",
  "port_access_clients_limit": 1,
  "port_access_critical_auth_role": null,
  "port_access_disable_cdp_auth": false,
  "port_access_disable_lldp_auth": false,
  "port_access_extended_access_vlans": [],
  "port_access_fallback_role": null,
  "port_access_onboarding_precedence": {},
  "port_access_policy_in_applied": null,
  "port_access_policy_in_status": {},
  "port_access_pre_auth_role": null,
  "port_access_qos_trust": null,
  "port_access_reauthentication_performed": null,
  "port_access_reauthentication_requested": null,
  "port_access_reject_role": null,
  "port_access_security_violation": {
    "action": "notify",
    "recovery_timer": 10,
    "shutdown_recovery_enable": false
  },
  "port_access_security_violation_reason": {},
  "port_access_security_violation_shutdown": false,
  "port_access_status": {},
  "port_access_stp_admin_edge": null,
  "port_access_vlan_mode": null,
  "port_access_vlan_tag": null,
  "port_access_vlan_trunks": [],
  "port_security": {
    "client_limit": 1,
    "enable": false
  },
  "port_security_static_client_mac_addr": [],
  "portfilter": [],
  "q_profile": null,
  "qos": null,
  "qos_config": {},
  "qos_status": {
    "cos_override_applied": false,
    "dscp_override_applied": false,
    "schedule_profile": "factory-default"
  },
  "queue_bandwidth_status": {
    "0": 1636800000,
    "1": 1636800000,
    "2": 1636800000,
    "3": 1636800000,
    "4": 1636800000,
    "5": 1636800000,
    "6": 1636800000,
    "7": 1636800000
  },
  "queue_tx_bytes": {},
  "queue_tx_errors": {},
  "queue_tx_maxdepth": {},
  "queue_tx_packets": {},
  "rate_limits": {
    "broadcast_units": "kbps",
    "icmp_units": "kbps",
    "icmp_version": "ip-all",
    "multicast_units": "kbps"
  },
  "rate_limits_status": {},
  "rdisc_irdp_broadcast": null,
  "rdisc_irdp_enable": null,
  "rdisc_irdp_preference": null,
  "rdisc_irdp_timers": {},
  "routing": false,
  "selftest": {
    "status": "skipped"
  },
  "selftest_disable": false,
  "sflow_statistics": {},
  "software_update_force_shutdown": false,
  "speed_downshift": false,
  "split_admin_status": "none",
  "split_children": [],
  "split_oper_status": "none",
  "split_parent": null,
  "statistics": {},
  "status": {
    "netdev_state": "ready"
  },
  "stp_config": {
    "admin_edge_port_enable": false,
    "bpdu_filter_enable": false,
    "bpdu_guard_enable": false,
    "bpdus_rx_disable": false,
    "bpdus_tx_disable": false,
    "link_type": "auto",
    "loop_guard_enable": false,
    "port_priority": 128,
    "protocol_migration_disable": false,
    "restricted_port_role_disable": false,
    "restricted_port_tcn_disable": false,
    "root_guard_enable": false,
    "rpvst_filter_enable": false,
    "rpvst_guard_enable": false
  },
  "stp_status": {
    "oper_edge_port_enabled": false,
    "oper_link_type": "point_to_point"
  },
  "tunnel_endpoints": "/rest/v10.04/system/interfaces/1%2F1%2F1/tunnel_endpoints",
  "type": "system",
  "udld_active": false,
  "udld_arubaos_compatibility_mode": "forward_then_verify",
  "udld_compatibility": "aruba_os",
  "udld_enable": false,
  "udld_interface_state": "uninitialized",
  "udld_interface_status": "unblock",
  "udld_interval": 7000,
  "udld_num_clear_stats_performed": null,
  "udld_num_clear_stats_requested": null,
  "udld_remote_interface_mac": null,
  "udld_remote_interface_name": null,
  "udld_remote_system_id": null,
  "udld_retries": 4,
  "udld_rfc5171_compatibility_mode": "normal",
  "udld_statistics": {
    "udld_port_transitions": 0,
    "udld_rx": 0,
    "udld_rx_discarded": 0,
    "udld_rx_dropped": 0,
    "udld_tx": 0
  },
  "urpf_check": "disable",
  "user_config": {
    "admin": "down",
    "speed_downshift": false
  },
  "virtual_ip4_routers": "/rest/v10.04/system/interfaces/1%2F1%2F1/virtual_ip4_routers",
  "virtual_ip6_routers": "/rest/v10.04/system/interfaces/1%2F1%2F1/virtual_ip6_routers",
  "vlan_mode": null,
  "vlan_tag": null,
  "vlan_translation_hw_status": "not-configured",
  "vlan_translations": {},
  "vlan_trunks": [],
  "vlans_per_protocol": {},
  "vrf": null,
  "vrrpv2_statistics": {},
  "vrrpv3_statistics": {},
  "vrrpv3_status": {},
  "vsf_force_shutdown": false,
  "vsf_hw_state": "disabled",
  "vsf_interface_status": {},
  "vsf_peer_status": {},
  "vsx_virtual_gw_mac_v4": null,
  "vsx_virtual_gw_mac_v6": null,
  "vsx_virtual_ip4": [],
  "vsx_virtual_ip6": []
}
```

### Associate an Interface with a VLAN

Since POST creates a resource, and the interfaces already exist, we use PUT to update the config of the interface.

As we did before, we will create some JSON in a file that contains the request information.

```json
{
  "routing": false,
  "vlan_mode": "access",
  "vlan_tag": {
    "999":"/rest/v10.04/system/vlans/999"
  }
}
```

Next we issue the PUT request with the redirect < sending in the JSON payload.

```bash
http PUT https://10.251.11.103/rest/v10.04/system/interfaces/1%2F1%2F1 --verify NO --session mysesh < interface1.json 
```

*Example use*
```bash
root@ubuntu:/home/student/TORY# http PUT https://10.251.11.103/rest/v10.04/system/interfaces/1%2F1%2F1 --verify NO --session mysesh < interface1.json 
HTTP/1.1 200 OK
Connection: keep-alive
Content-Length: 0
Content-Security-Policy: script-src 'self' 'unsafe-inline'; object-src 'none'; font-src *; media-src 'none'; form-action 'self';
Content-Type: application/json; charset=utf-8
Date: Tue, 19 Apr 2022 17:21:20 GMT
Server: nginx
Strict-Transport-Security: max-age=31536000; includeSubdomains;
X-Content-Type-Options: nosniff
X-Frame-Options: SAMEORIGIN
X-XSS-Protection: 1; mode=block
```

### Lets verify the interface is associated

```bash
http GET https://10.251.11.103/rest/v10.04/system/interfaces/1%2F1%2F1 --verify NO --session mysesh | grep "vlan_tag" -A 5
```

Grep allows us to match on "vlan_tag" and show the preceeding 5 lines using -A.

```bash
root@ubuntu:/home/student/TORY# http GET https://10.251.11.103/rest/v10.04/system/interfaces/1%2F1%2F1 --verify NO --session mysesh | grep "vlan_tag" -A 5

  "applied_vlan_tag": {
    "999": "/rest/v10.04/system/vlans/999"
  },
  "applied_vlan_trunks": [],
  "applied_vlans_per_protocol": {},
  "arp_inspection": {
--
  "port_access_vlan_tag": null,
  "port_access_vlan_trunks": [],
  "port_security": {
    "client_limit": 1,
    "enable": false
  },
--
  "vlan_tag": {
    "999": "/rest/v10.04/system/vlans/999"
  },
  "vlan_translation_hw_status": "not-configured",
  "vlan_translations": {},
  "vlan_trunks": [],
```

We see that the interface is in vlan 999.

