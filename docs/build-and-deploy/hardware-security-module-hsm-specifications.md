# Hardware Security Module HSM Specifications

HSM stands for Hardware Security Module and is an incredibly secure physical device specifically designed and used for crypto processing and strong authentication. It can encrypt, decrypt, create, store and manage digital keys, and be used for signing and authentication. The purpose is to safeguard and protect keys.

MOSIP highly recommends the following specifications for HSM:

1. Must support cryptographic offloading and acceleration.
2. Should provide Authenticated multi-role access control.
3. Must have strong separation of administration and operator roles.
4. Capability to support client authentication.
5. Must have secure key wrapping, backup, replication and recovery.
6. Must support 2048, 4096 bit RSA Private Keys, 256 bit AES keys on FIPS 140-2 Level 3 Certified Memory of Cryptographic Module.
7. Must support at least 10000+ 2048 RSA Private Keys on FIPS 140-2 Level 3 Certified Memory of Cryptographic Module.
8. Must support clustering and load balancing.
9. Should support cryptographic separation of application keys using logical Partitions.
10. Must support M of N multi-factor authentication.
11. PKCS\#11, OpenSSL, Java \(JCE\), Microsoft CAPI and CNG.
12. Minimum Dual Gigabit Ethernet ports \(to service two network segments\) and 10G Fibre port should be available.
13. Asymmetric public key algorithms: RSA, DiffieHellman, DSA, KCDSA, ECDSA, ECDH, ECIES.
14. Symmetric algorithms: AES, ARIA, CAST, HMAC, SEED, Triple DES, DUKPT, BIP32.
15. Hash/message digest: SHA-1, SHA-2 \(224, 256, 384, 512 bit\).
16. Full Suite B implementation with fully licensed ECC including Brainpool, custom curves and safe curves.
17. Safety and environmental compliance         
    1. Compliance to UL, CE, FCC part 15 class B.
    2. Compliance to RoHS2, WEEE.
18. Management and monitoring
    1. Support Remote Administration —including adding applications, updating firmware, and checking the status— from NoC.
    2. Syslog diagnostics support.
    3. Command line interface \(CLI\)/graphical user interface \(GUI\).
    4. Support SNMP monitoring agent.
19. Physical characteristics
    1. Standard 1U 19in. rack mount with integrated PIN ENTRY Device.
20. Performance
    1. RSA 2048 Signing performance – 10000 per second.
    2. RSA 2048 Key generation performance – 10+ per second.
    3. RSA 2048 encryption/decryption performance - 20000+.
    4. RSA 4096 Signing performance - 5000 per second.
    5. RSA 4096 Key generation performance - 2+ per second.
    6. RSA 4096 encryption/decryption performance - 20000+.
21. Should have the ability to backup keys, replicate keys, store keys in offline locker facilities for DR. The total capacity is inline with the total number of keys prescribed.
22. Clustering minimum of 20 HSMs.
23. Less than 30 seconds for key replication across the cluster.
24. A minimum of 30 logical partitions and their license should be included in the cost.

