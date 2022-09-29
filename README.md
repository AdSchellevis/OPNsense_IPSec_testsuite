IPsec test scenario's
==================================



Base configuration
==================================

The test setup consists of two machines, both having a LAN and an OPT1 interface.
Firewall should either be disabled or passing all traffic on both.


Machine A
-----------------------------

Interfaces -> LAN -> Addresses:
*    192.168.111.1/24
*    192.168.113.1/24
*    fc00::1/128

Interfaces -> OPT1 -> Addresses:
*    192.168.2.3/24
*    fc00::2:3/112

Machine B
-----------------------------

Interfaces -> LAN -> Addresses:
    192.168.112.1/24
    192.168.114.1/24
    fc00::2/128

Interfaces -> OPT1 -> Addresses:
    192.168.2.4/24
    fc00::2:4/112

Directory structure
-----------------------------

For all tests performed we collected the following relevant configuration data:

* config.[a|b].xml --> relevant configuration data for this test, depending on settings explained in "Base configuration"
* ipsec.[a|b].conf --> ipsec.conf generated on 22.7.4
* swanctl.[a|b].conf --> new swanctl.conf generated with the changes for https://github.com/opnsense/core/issues/5636

Tests
==================================

* VTI_S2S_psk
    - IKEv2
    - routed IPsec (VTI) 
    - pre-shared-key authentication
    - tunnel 192.168.188.1 <-> 192.168.188.2
* VTI_S2S_pubkey
    - IKEv2
    - routed IPsec (VTI)
    - (RSA) public key authentication
    - tunnel 192.168.188.1 <-> 192.168.188.2
* VTI_S2S_rsa
    - IKEv2
    - routed IPsec (VTI)
    - RSA (certificate) authentication
    - tunnel 192.168.188.1 <-> 192.168.188.2
* PB_S2S_psk_default
    - IKEv2
    - policy based 
    - pre-shared-key authentication
    - tunnel 192.168.111.0/24 <-> 192.168.112.0/24
    - tunnel 192.168.113.0/24 <-> 192.168.114.0/24
* PB_S2S_psk_isolation
    - IKEv2
    - policy based
    - pre-shared-key authentication
    - tunnel isolation selected
    - tunnel 192.168.111.0/24 <-> 192.168.112.0/24
    - tunnel 192.168.113.0/24 <-> 192.168.114.0/24
* PB_S2S_psk_IKEv1
    - IKEv1
    - policy based
    - pre-shared-key authentication
    - tunnel 192.168.111.0/24 <-> 192.168.112.0/24
    - tunnel 192.168.113.0/24 <-> 192.168.114.0/24
* BP_S2S_IPv6_tunnel
    - IKEv2
    - policy based
    - pre-shared-key authentication
    - tunnel isolation selected
    - tunnel 192.168.111.0/24 <-> 192.168.112.0/24
    - tunnel 192.168.113.0/24 <-> 192.168.114.0/24
    - tunnel fc00::1/28 <-> fc00::2/128 
