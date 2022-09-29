# minecraft-announce firewall hacker

The Minecraft (Java edition) _Open to LAN_ multiplayer feature hosts the LAN
game on a random port. This port is multicasted so that other Minecraft clients
can dynamically discover the multiplayer game.

This repository contains a script that listens to the multicast message, and
another script that uses the information to open a port in an nftables firewall.
Other scripts to support iptables, ufw or firewalld could be added.

The script could also be used to set up a port forward in a router or to
redirect a stable port number to the dynamic port number.

## Use with nftables

Set up a named set containing `inet_service` elements (that is, port numbers),
and use that to match on traffic to the LAN port. In this example, `mcport` is
the named set, and there are two rules, one to accept the multicast message
and another to accept the LAN traffic:

    table inet filter {
        set mcport {
            type inet_service;
        }

        chain INPUT {
            type filter  hook input  priority filter;
            policy drop;

            ct state established  counter  accept

            pkttype host  tcp dport @mcport  counter  accept

            pkttype multicast  udp dport 4445  counter  accept
        }
    }

Then, enable and start `mcannounce-nft.service`, which will listen to the
announcements and add and remove elements to the `mcport` set as necessary.
