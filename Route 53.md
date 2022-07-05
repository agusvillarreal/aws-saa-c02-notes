## Route 53 Overview
DNS -> DNS is used to convert-human-friendly domain names into an Internet Protocol (IP) address
IPV4 and IPV6

#### Top-Level Domain
If we look at common domain names (e.g, google.com, bbc.co.uk, and acloud.guru), you will notice a string of characters separated by dots (periods)
The last word in a domain name represents the top-level domain. The second word in a domain name is known as a second-level domain name (this is optional, though, and depends on the domain name)

Start of Authorite
The SOA record stores information about:
- The name if teh server that supplied the data for the zone
- The administrator of the zone
- The current version of the data file
- The default number of seconds for the time-to-live on resource records

NS name server
Ns records are used by top-level domain servers to direct traffic to the content DNS server that contains the authoritative DNS records

### DNS RECORDS
#### A Record
An A (or address) record is the fundamental type of DNS record.
The A record is used by a computer to translate the name of the domain to an IP address

#### TTL
The length that a DNS record is cached on either the resolving server or the user's own local PC is equal to the value of the time to live (TTL) in seconds
The lower the time to live, the faster changes to DNS records take to propagate throughout the internet

#### CNAME
A CNAME (canonical name) can be used to resolve one domain name to another. For example, you may have a mobile website with the domain name http://m.acloud.guru that is used for when users browse to your domain name on their mobile devices

alias record vs cname -> alias record (AWS)
1. SOA Records
2. CNAME Records
3. NS Records
4. A records
