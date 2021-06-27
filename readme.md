Android (9 or newer)

    1. Go to «Settings»
    2. Go to «Connection & Sharing»
    3. Press «Private DNS»
    4. Insert server name (example [Cloudflare]: 1dot1dot1dot1.cloudflare-dns.com)
    5. Press «Save»

iOS (14 or newer)

    1. Download configuration file (examples: https://github.com/paulmillr/encrypted-dns)
    2. Open the folder with the configuration file
    3. Press and hold + select «Info»
    4. Press «Open»
    5. Go to «Settings» — «General» — «Profile»
    6. Select profile and press «Install»

MacOS (Big Sur or newer)

    1. Download configuration file:
        1. Open Terminal
        2. git clone https://github.com/paulmillr/encrypted-dns.git)
        3. cd encrypted-dns/
        4. open .
    2. Double click selected profile
    3. Go to «System Preferences» — «Profiles»
    4. Select profile and press «Install»

Windows (10 ver. 20185 or newer)

    1. Open «Setting» — «Network & Internet» — «Status»
    2. Press «Properties» — «Edit DNS»:
    3. Configure DNS:
        1. Select Manual
        2. IPv4 — On
        3. Preferred DNS — (example [Cloudflare]: 1.1.1.1)
        4. Preferred DNS encryption — Encrypted only (DNS over HTTPS)
        5. Alternate DNS — (example [Cloudflare]: 1.0.0.1)
        6. Alternate DNS encryption — Encrypted only (DNS over HTTPS)
        7. IPv6 — On
        8. Preferred DNS — (example [Cloudflare]: 2606:4700:4700::1111)
        9. Preferred DNS encryption — Encrypted only (DNS over HTTPS)
        10. Alternate DNS — (example [Cloudflare]: 2606:4700:4700::1001)
        11. Alternate DNS encryption — Encrypted only (DNS over HTTPS)
        12. Press «Save»

Linux (Mint 20 or newer)

    1. Install package dnscrypt-proxy:
        1. Open Terminal
        2. sudo apt install dnscrypt-proxy
    2. Make sure that port 53 is not listening:
        1. sudo netstat -tunlp
            1. if there are rows containing x.x.x.x:53 in «Local Address» with status «LISTEN»:
                1. sudo kill -9 [Program name]
    3. Start dnscrypt-proxy service: sudo systemctl start dnscrypt-proxy.service
    4. Add the dnscrypt-proxy service to startup: sudo systemctl enable dnscrypt-proxy.service
    5. Configure NetworkManager:
        1. Open the configuration file: sudo xed /etc/NetworkManager/NetworkManager.conf
        2. In section [Main] add: dns=none
        3. Save the changes
        4. Restart NetworkManager: sudo systemctl restart NetworkManager
    6. Configure resolv.conf:
        1. Make a backup copy of the resolv.conf: sudo cp /etc/resolv.conf /etc/resolv.conf.backup
        2. Remove /etc/resolv.conf: sudo rm -f /etc/resolv.conf
        3. Create a /etc/resolv.conf: sudo xed /etc/resolv.conf
            1. Add to file next lines:
        ◦ nameserver 127.0.2.1
        ◦ options edns0 single-request-reopen
        ◦ EDNSPayloadSize 4096
        4. Save the changes
    7. Configure dnscrypt-proxy: 
        1. Open the configuration file: sudo xed /etc/dnscrypt-proxy/dnscrypt-proxy.toml
        2. Change line «server_names = ['google']» on (change to the selected server: example [Cloudflare]: «server_names = ['cloudflare', 'cloudflare-ipv6']»)
        3. Save the changes
        4. Restart dnscrypt-proxy: sudo systemctl restart dnscrypt-proxy.service