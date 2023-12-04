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
