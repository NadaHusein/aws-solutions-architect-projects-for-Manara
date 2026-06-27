**Project Overview**



Designed a hybrid AWS network connecting an on-premises environment to multiple AWS VPCs through AWS Transit Gateway and Site-to-Site VPN.



The solution demonstrates centralized networking, hybrid DNS resolution, and network security best practices



**Services Used**



1-Amazon VPC

2-AWS Transit Gateway

3-Site-to-Site VPN

4-Route 53 Resolver

5-AWS RAM

6-AWS Network Firewall

7-CloudTrail

8-AWS Config



**Transit Gateway**



* Created a central Transit Gateway.
* Attached Dev, Staging, and Production VPCs.
* Added VPN attachment.
* Configured route tables



**VPN Configuration**



* Site-to-Site VPN
* IKEv2
* BGP Dynamic Routing
* Customer Gateway
* Virtual Private Gateway



**Hybrid DNS**



Configured Route53 Resolver



* Inbound Endpoint
* Outbound Endpoint
* Forwarding Rules



This enables:



* On-premises servers to resolve AWS private DNS.
* AWS workloads to resolve on-premises DNS.



**Network Security**



Centralized inspection using Network Firewall.



Traffic filtered between:



* VPC to VPC
* Internet
* On-premises



**Monitoring**



Enabled:



CloudTrail

AWS Config



to audit network configuration changes



**Design Decisions**



**CIDR Planning**



Used non-overlapping CIDRs to avoid routing conflicts.



**Transit Gateway**



Selected instead of VPC Peering because it scales better for multiple VPCs.



**VPN**



Used Site-to-Site VPN with BGP for automatic route propagation.



**DNS**



Implemented Route53 Resolver endpoints for hybrid DNS resolution.



**Security**



Network Firewall provides centralized inspection.



**Auditing**



CloudTrail and AWS Config monitor all networking changes

