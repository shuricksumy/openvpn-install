# openvpn-install

- #### This project was cloned from [https://github.com/angristan/openvpn-install](https://github.com/angristan/openvpn-install) (big thanks for this great job)

- #### The Docker builder with UI part is here [**OPENVPN-SERVER-UI**](https://github.com/shuricksumy/openvpn-u)

## Updates

- Refactored internal structure to use this script for the docker builder
- Added Docker menu with next options:

  ```bash
  DOCKER_COMMAND
  
  1) Install packages
  2) Configure openvpn and setup files
  3) Create new Client
  4) Generate .ovpn file
  ```

- Added menu for setup IP openvpn network:

  ```bash
  #variable
  IP_CHOICE
  
  1) Default: 10.8.0.0
  2) Custom [variable IP_RANGE]
  ```

- Added tls-crypt-v2

  ```bash
  #variable
  TLS_SIG="3"
  ```

- Added a headless password adding to the user

  ```bash
  #variable
  CL_PASS="somepass"
  ```

- Add a variable for setting the tun number

  ```bash
  #variable
  TUN_NUMBER="12"
  ```

- New logic for file generation
  - if easy-rsa is exist -> do not delete it and use it for ovpn configs, if not -> create a new directory with configs
  - if openvpn server.conf does not exist -> generated a new one based on env config and easy-rsa directory

- Added small services variables:

  ```bash
  #variable
  DISABLE_DEF_ROUTE_FOR_CLIENTS="y|n"
  
  #add 10 years expiration
  echo "set_var EASYRSA_CA_EXPIRE 3650" >>vars
  echo "set_var EASYRSA_CERT_EXPIRE 3650" >>vars
  
  ```

- Added OVPN_PATH to set path to openvpn configs

  ```bash
  #default
  OVPN_PATH="/etc/openvpn"
  ```

<details>

<summary> Environment Variables</summary>


### 1. [openvpn-install](https://github.com/shuricksumy/openvpn-install) variables
```bash
DOCKER_COMMAND="1-4"

    1) Install packages
    2) Configure openvpn and setup files
    3) Create new Client
    4) Generate .ovpn file
```
```bash
AUTO_INSTALL="y|n"

    "y" - install without questions with predefined variables [default]
```
### 2 Server setup variables
```bash
DOCKER_COMMAND="2"
  ||
  ENDPOINT="<Public IP>"
  TUN_NUMBER="12"
  APPROVE_IP="y"
  IPV6_SUPPORT="n"
  AUTO_INSTALL="y"
  DISABLE_DEF_ROUTE_FOR_CLIENTS="y|n"
  CLIENT_TO_CLIENT="y"
  SET_MGMT="<IP:PORT>"
  IP_CHOICE="1-2"
    |   |
    |   [1] IP_RANGE="10.8.0.0" [default]
    |   [2] IP_RANGE="<your internal ovpn ip subnetwork>" [set custom] 
    |
    PORT_CHOICE="1-3"
    |   |
    |   [1] PORT="1194" [default]
    |   [2] PORT="<your port>"
    |   [3] PORT="<random generator>"
    |
    PROTOCOL_CHOICE="1-2"
    |   |
    |   [1] PROTOCOL="udp" [default]
    |   [2] PROTOCOL="tcp"
    |
    DNS="1-13"
    |    |
    |    [1]  Current system resolvers
    |    [2]  Self-hosted DNS Resolver (Unbound) [not tested with Docker]
    |    [3]  Cloudflare (Anycast: worldwide)
    |    [4]  Quad9 (Anycast: worldwide)
    |    [5]  Quad9 uncensored (Anycast: worldwide)
    |    [6]  FDN (France)
    |    [7]  DNS.WATCH (Germany)
    |    [8]  OpenDNS (Anycast: worldwide)
    |    [9]  Google (Anycast: worldwide)
    |    [10] ---- FUCK RUSSIA
    |    [11] AdGuard DNS (Anycast: worldwide) [default]
    |    [12] NextDNS (Anycast: worldwide)
    |    [13] Custom 
    |         |
    |         |- DNS1="<your DNS1 IP>"
    |         |- DNS2="<your DNS1 IP>"
    |     
    COMPRESSION_ENABLED="y|n"
    |    | 
    |   [y] COMPRESSION_CHOICE="1-3"
    |    |    |
    |    |    [1] COMPRESSION_ALG="lz4-v2" [default]
    |    |    [2] COMPRESSION_ALG="lz4"
    |    |    [3] COMPRESSION_ALG="lzo"
    |    |  
    |    [n] [default]
    |
    CUSTOMIZE_ENC="y|n"
         | 
        [y] CIPHER_CHOICE="1-6"
         |    |
         |    [1] AES-128-GCM [default]
         |    [2] AES-192-GCM
         |    [3] AES-256-GCM
         |    |
         |    |- HMAC_ALG_CHOICE="1-3"
         |        |
         |        [1] HMAC_ALG="SHA256" [default]
         |        [2] HMAC_ALG="SHA384"
         |        [3] HMAC_ALG="SHA512"
         |    
         |    [4] AES-128-CBC
         |    [5] AES-192-CBC
         |    [6] AES-256-CBC
         |    
         |- CERT_TYPE="1-2"
         |    |
         |    [1] ECDSA [default]
         |    |   |
         |    |   CERT_CURVE_CHOICE="1-3"
         |    |   |
         |    |   [1] CERT_CURVE="prime256v1" [default]
         |    |   [2] CERT_CURVE="secp384r1"
         |    |   [3] CERT_CURVE="secp521r1"
         |    |   |
         |    |   CC_CIPHER_CHOICE="1-2"
         |    |   |
         |    |   [1] CC_CIPHER="TLS-ECDHE-ECDSA-WITH-AES-128-GCM-SHA256" [default]
         |    |   [2] CC_CIPHER="TLS-ECDHE-ECDSA-WITH-AES-256-GCM-SHA384"
         |    |
         |    [2] RSA
         |         |
         |         RSA_KEY_SIZE_CHOICE="1-3"
         |         |
         |         [1] RSA_KEY_SIZE="2048" [default]
         |         [2] RSA_KEY_SIZE="3072"
         |         [3] RSA_KEY_SIZE="4096"
         |         |
         |         CC_CIPHER_CHOICE="1-2"
         |         |
         |         [1] CC_CIPHER="TLS-ECDHE-RSA-WITH-AES-128-GCM-SHA256" [default]
         |         [2] CC_CIPHER="TLS-ECDHE-RSA-WITH-AES-256-GCM-SHA384"
         |      
         |- DH_TYPE="1-2"
         |    |
         |    [1] ECDH [default]
         |    |    |
         |    |    DH_CURVE_CHOICE="1-3"
         |    |    |
         |    |    [1] DH_CURVE="prime256v1" [default]
         |    |    [2] DH_CURVE="secp384r1"
         |    |    [3] DH_CURVE="secp521r1"
         |    |    
         |    [2] DH
         |         |
         |         $DH_KEY_SIZE_CHOICE="1-3"
         |         |
         |         [1] DH_KEY_SIZE="2048" [default]
         |         [2] DH_KEY_SIZE="3072"
         |         [3] DH_KEY_SIZE="4096"
         |
         |- TLS_SIG="1-4"
         |    |
         |    [1] tls-crypt
         |    [2] tls-auth
         |    [3] tls-crypt-v2 [default]
         |    [4] no tls
         |   
         [n] [default]
             | CIPHER="AES-128-GCM"
             | CERT_TYPE="1" # ECDSA
             | CERT_CURVE="prime256v1"
             | CC_CIPHER="TLS-ECDHE-ECDSA-WITH-AES-128-GCM-SHA256"
             | DH_TYPE="1" # ECDH
             | DH_CURVE="prime256v1"
             | HMAC_ALG="SHA256"
             | TLS_SIG="3" # tls-crypt-v2
         
       

```
### 3 Client setup variables
```bash
DOCKER_COMMAND="3" 
CLIENT="<client name>"
PASS="1-2"
 |
 [1] no password [default]
 [2] CL_PASS="<client password>"
```

</details>