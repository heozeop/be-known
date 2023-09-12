# definition
- method of manipulating resolution of domain name.

## how it works
- victim -> contaminated DNS server -> ip -> JS/Flash -> internal ip

## how to prevents
- firewall
- DNS pinning
    - IP address is locked to the value received in the first DNS response.
- NoScript extension like tool
- DNS server can filter out private IP and loopback IP address 

# REF
- [wiki - DNS rebinding](https://en.wikipedia.org/wiki/DNS_rebinding)