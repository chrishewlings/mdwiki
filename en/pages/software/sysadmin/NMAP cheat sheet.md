# NMAP cheat sheet

`-A`  - Turn on OS and version detection. Requires `sudo`.
`-sA` - Test if host is protected by a firewall. (ACK scan)
`-sV` - detect remote services/versions

`-PN` - Scan a firewalled host for open ports.

`-sP` - Host discovery (ping scan). Fast, no detail. 
`-F` - Fast scan; only probes ports listed in `/etc/services`

`-p xx` 

`--open` - Only show open ports.
`--reason -p xx` - show reason that port is in that state