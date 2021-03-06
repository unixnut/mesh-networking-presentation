# OpenVPN mesh networking
A talk to be given at the AWS meetup
on 16 May 2017

## Blurb
AWS provides a service whereby two [VPCs][AWS-VPC] can be linked, but what if you want to link more than two VPCs, or you aren't using AWS?  This talk describes a peer-to-peer arrangement (i.e. no central VPN server) that allows this using IPv4.  For brevity, each VPC and/or physical network that is to be linked is hereafter referred to as a LAN.

The talk consists of a technical demonstration of a set of software tools called [P2P-VPN](https://github.com/unixnut/P2P-VPN), which generates OpenVPN config files that support a mesh of LANs and provides universal static routing, i.e. nodes on any LAN can reach nodes on any other LAN.  This requires each LAN to have a designated subnet that is private (i.e. having a prefix that is listed in [RFC1918][]) and is different from all the others, and from any other resources that may be used by nodes in any of the LANs.  Each LAN requires a publicly accessible Linux server that acts as the VPN gateway; this must be able to have one UDP port opened (e.g. in a Security Group, or forwarded from a router) for every other LAN in the mesh.  A [VPC "NAT Instance"][VPC-NAT] (which does address masquerading for EC2 instances in a VPC that don't have a public IP address) can be used for this.  Only one public IP address is required per LAN.

Adding new LANs to the mesh is possible, but requires the config of all other LANs to be re-generated centrally and then distributed to the VPN gateways.

P2P-VPN is open source software, but was developed with the intent of being used in commercial environments.  There is already at least one commercial user.  If you wish to make a financial contributution to encourage the developer to maintain this and other open source software, please contact Alastair Irvine via [Warpspace IT](http://www.warpspace.net/).

  [AWS-VPC]: https://aws.amazon.com/vpc/
  [RFC1918]: http://www.faqs.org/rfcs/rfc1918.html "Address Allocation for Private Internets"
  [VPC-NAT]: http://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/VPC_NAT_Instance.html

## Outline

1. Introduction
  1. Background
  1. AWS VPCs
  1. Types of VPN
1. Solution summary
  1. Topology diagram
  1. Details
  1. Special VPN CIDR address range required
1. AWS
  1. Why not use VPC Peering Connections?
  1. NAT instance vs. NAT Gateway
  1. Subnets and route tables
  1. Security Groups
  1. Don't forget to turn off "Source address check" on VPN instances
1. P2P-VPN
  1. Code snippets
1. Adding a new LAN
  1. Track LAN numbers!
  1. Distribute config
  1. Add routes
  1. Modify firewall rules / Security Groups
1. Gotchas
  1. Non-overlapping LAN network ranges
  1. ClassicLink
  1. Public vs. private IP addresses for servers with both
1. Further considerations
  1. Interaction with regular VPNs
  1. High availability (HA)
  1. Fully peer-to-peer, i.e. either end of each link can initiate
  1. BGP recommended for large deployments
  

## Presenter bio

Alastair Irvine is a Software Engineer and system administrator by trade.  He has a BSc in Computer Science from Curtin University.

His computer-related interests lie in various areas within his trade; suffice to say that he is a "geek of many colours". :)  Alastair is a die-hard FOSS user and Linux fan.

He is also a freelancer with his own business.  [Warpspace IT](http://www.warpspace.net/) is a consultancy with a fairly broad focus on the technical side of IT.

### Contact

guru@warpspace.net

1300 881744

## Slides

**TBA**
