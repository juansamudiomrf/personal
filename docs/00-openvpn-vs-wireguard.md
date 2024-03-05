# OPENVPN VS WIREGUARD

## comparative table

| Aspect        | OpenVPN                                       | WireGuard                                         | Observations                                                   |
|----------------|-----------------------------------------------|---------------------------------------------------|------------------------------------------------------------------|
| Availability  | Yes                                           | Yes                                               | Both can operate in active-passive mode                          |
| Authentication  | With certificates                             | With certificates                                 | While both use certificates for authentication, OpenVPN often requires a more elaborate public key infrastructure due to its need for a CA (Certificate Authority) to sign the certificates. In contrast, WireGuard simplifies this process, making certificate management easier and more straightforward. |
| Automation    | Medium                                        | High                                              | WireGuard provides a more direct configuration, facilitating its integration into automated and orchestrated environments. On the other hand, OpenVPN may require more complex and detailed configurations, which can hinder automation. |
| Performance   | Medium                                        | High                                              | WireGuard is known for its greater efficiency and lower resource consumption compared to OpenVPN.  |
| Clients       | Linux, macOS, mobile                         | Linux, macOS, mobile                              | Both OpenVPN and WireGuard offer clients for a variety of platforms, allowing broad compatibility with popular operating systems such as Linux, macOS, and mobile devices.  |

## these are some of my observations

- i found a good Docker project for WireGuard with autoconfig per user: [link](https://github.com/linuxserver/docker-wireguard). 
- both have good exporters: [WireGuard exporte](https://github.com/MindFlavor/prometheus_wireguard_exporter) , [OpenVPN exporter](https://github.com/kumina/openvpn_exporter). 
- WireGuard also has a console which is relatively easy to install: [WireHole.](https://github.com/IAmStoxe/wirehole/blob/74c4c9cedf686d53304cc3996c9e802fbac3a82b/docker-compose.yml#L41)
- WireGuard can deny communication between clients: [link](https://www.lautenbacher.io/en/lamp-en/wireguard-prohibit-communication-between-clients-client-isolation/)
