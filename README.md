# openvpn-install

- #### There is original [README.MD](https://github.com/angristan/openvpn-install/blob/master/README_ORIGINAL.md).
- #### This project was cloned from https://github.com/angristan/openvpn-install (big thanks fort this great job)
- #### The Docker builder with UI part will be added as separate project [here] soon ...

## Updates:
- Refactored internal structure to use this script for docker builder
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
  ```
  #variable
  TLS_SIG="3"
  ```
- Added headless added password to user
  ```
  #variable
  CL_PASS="somepass"
  ```
- Add variable for setting tun number
  ```
  #variable
  TUN_NUMBER="12"
  ```
- New logic of file generation
  - if easy-rsa is exist -> do not delete in and use for ovpn configs, if not -> create new direcory with configs 
  - if openvpn server.conf does not exist -> generated new one based on env config and easy-rsa direcory

- Added small services variables:
  ```
  #variable
  DISABLE_DEF_ROUTE_FOR_CLIENTS="y|n"
  
  #add 10 years expiration
  echo "set_var EASYRSA_CA_EXPIRE 3650" >>vars
  echo "set_var EASYRSA_CERT_EXPIRE 3650" >>vars
  
  ```