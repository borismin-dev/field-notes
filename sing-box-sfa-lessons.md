# sing-box for Android (SFA) lessons

- QR imports require the official remote-profile URI format:
  `sing-box://import-remote-profile?url=<urlencoded>#<name>`
  A bare https subscription URL is rejected with "Not a valid sing-box remote profile URI".
- A remote profile must include a `tun` inbound (auto_route). A profile with only a mixed inbound "connects" but passes 0 up/down traffic.
- sing-box (tested 1.13.11) does NOT support the `xhttp` transport. A VLESS+XHTTP node cannot be imported into SFA at all — deliver it for Xray-based clients / Shadowrocket instead, and say so honestly.
- VLESS+WS+TLS nodes are fine in sing-box; verify with a real client handshake (generate_204 = 204) and report the measured exit IP, including whether it is a datacenter or residential address.
