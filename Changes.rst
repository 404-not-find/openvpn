Version 2.4.0

============
New features
============

keying-material-exporter
    Keying Material Exporter [RFC-5705] allow additional keying material to be
    derived from existing TLS channel. 

redirect-gateway ipv6
    OpenVPN has now feature parity between IPv4 and IPv6 for redirect
    gateway including the handling of overlapping IPv6 routes with
    IPv6 remote VPN server address

Mac OS X Keychain management client
    add contrib/keychain-mcd which allows to use Mac OS X keychain
    certificates with OpenVPN

Peer ID support
    Added new packet format P_DATA_V2, which includes peer-id. If
    server and client  support it, client sends all data packets in
    the new format. When data packet arrives, server identifies peer
    by peer-id. If peer's ip/port has changed, server assumes that
    client has floated, verifies HMAC and updates ip/port in internal structs.

Dualstack client connect
    Instead of only using the first address of each --remote OpenVPN
    will now try all addresses (IPv6 and IPv4) of a --remote entry.

LZ4 Compression
    Additionally to LZO compression OpenVPN now also supports LZ4
    compression.

=======
Changes
=======
- proto udp and proto tcp specify to use IPv4 and IPv6. The new
  options proto udp4 and tcp4 specify to use IPv4 only.

- connect-timeout specifies now the timeout until the first TLS packet
  is received (identical to server-poll-timeout) and this timeout now
  includes the removed socks proxy timeout and http proxy timeout.

  In --static mode connect-timeout specifies the timeout for TCP and
  proxy connection establishment 


- connect-retry now specifies the maximum number of unsucessfully
  trying all remote/connection entries before exiting.

- sndbuf and recvbuf default now to OS default instead of 64k

- OpenVPN exits with  an error if an option has extra parameters;
  previously they were silently ignored

- The default of tls-cipher is now "DEFAULT:!EXP:!PSK:!SRP:!kRSA"
  instead of "DEFAULT" to always select perfect forward security
  cipher suites

- --tls-auth always requires OpenVPN static key files and will no
  longer work with free form files

- proto udp6/tcp6 in server mode will now try to always listen to
  both IPv4 and IPv6 on platforms that allow it. Use bind ipv6only
  to explicitly listen only on IPv6.
