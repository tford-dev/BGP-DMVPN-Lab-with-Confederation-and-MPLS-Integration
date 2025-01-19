Security notes:

MPLS NETWORK

enable secret 3n@b13
username tech privilege 1 secret tech-user
username admin privilege 15 secret @Dm1n-10g1n

-PE1 to P1 OSPF Authentication: 
ospfv3 authentication ipsec spi 512 sha1 1111111111111111111111111111111111111111

-P1 to PE1 OSPF Authentication:
ospfv3 authentication ipsec spi 512 sha1 1111111111111111111111111111111111111111

-P1 to PE2 OSPF Authentication:
ospfv3 authentication ipsec spi 768 sha1 2222222222222222222222222222222222222222

-PE2 to P1 OSPF Authentication:
ospfv3 authentication ipsec spi 768 sha1 2222222222222222222222222222222222222222



CUSTOMER1 NETWORK

enable secret 3n@b13
username company1-tech privilege 1 secret company1-tech-user
username admin privilege 15 secret company1-@Dm1n-10g1n

-C1-HQ to PE1 eBGP Authentication Password: C1toPE1

-C1-BRANCH1 to PE2 eBGP Authentication Password: C1BR@NCH1toPE2

-C1-BRANCH2 to PE2 eBGP Authentication Password: C1BR@NCH2toPE2

CUSTOMER1 IPSEC CONFIG:
crypto isakmp policy 10
 encr aes 256
 authentication pre-share
 group 2
 hash sha
 lifetime 28800
exit

crypto isakmp key C1-KEY address 0.0.0.0

crypto ipsec transform-set C1-SET esp-aes 256 esp-sha-hmac
 mode transport

crypto ipsec profile C1-PROFILE
 set transform-set C1-SET
 set pfs group2

interface Tunnel0
 tunnel protection ipsec profile C1-PROFILE




CUSTOMER2 NETWORK

enable secret 3n@b13
username company2-tech privilege 1 secret company2-tech-user
username admin privilege 15 secret company2-@Dm1n-10g1n

-C2-HQ to PE1 eBGP Authentication Password: C2toPE1

-C2-BRANCH1 to PE2 eBGP Authentication Password: C2BR@NCH1toPE2

-C2-BRANCH2 to PE2 eBGP Authentication Password: C2BR@NCH2toPE2

CUSTOMER2 IPSEC CONFIG:

crypto isakmp policy 20
 encr aes 256
 authentication pre-share
 group 2
 hash sha
 lifetime 28800
exit

crypto isakmp key C2-KEY address 0.0.0.0

crypto ipsec transform-set C2-SET esp-aes 256 esp-sha-hmac
 mode transport

crypto ipsec profile C2-PROFILE
 set transform-set C2-SET
 set pfs group2

interface Tunnel0
 tunnel protection ipsec profile C2-PROFILE
