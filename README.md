# EAP TTLS authentication

This helps quick setup EAP TTLS for testing WPA2-Enterprise EAP TTLS.
[FreeRadius](https://github.com/FreeRADIUS/freeradius-server) service it.

## Quick start

```bash
git clone https://github.com/tknv/docker-radius-eap-ttls.git EAP-TTLS_FreeRadius
cd EAP-TTLS_FreeRadius
docker-compose up
```

Install Root CA and client cert by double click(usually) `pc.p12` and `ca.crt` in EAP-TTLS_FreeRadius directory.

## Usage

* Radius is listening on port 1812 UDP.
* A secret for Radius server connection is `symbol123`
    * It usually set it at Access Point.
* A password for all private key is `symbol`
    * It will be asked when install client certificate `pc.p12`

### Install client cert and CA to client machine/device

#### Windows

Install cert and CA by double click `pc.p12` then double click `ca.crt`. And goto Control Panel > All Control Panel Items > Network and Sharing Center > Manually connect or Network.  
**Network name** should be SSID (if use EAP TLS auth for wireless client). **Security type** `WPA2-Enterprise`. Then Next.

At pop up. XXXX Wireless Network Properties.  
Choose a network authentication method: Microsoft: EAP-TTLS  
Settings > tick Enable identity privacy  
Trusted Root Certification Authorities:  
  tick AWASLab  
Select a non-EAP method for authentication  
  Unencrypted password (PAP), but others also fine. yet not use LDAP.  
Then back to the pop up.  
Advanced settings > tick specify authentication mode: 
  User authentication > Save credentials.  
    **User account** is `tknv@awas.lab`, `symbol123` 

### Linux

#### WPA2-Enterprise (EAP TTLS)

`sudo wpa_supplicant -dd -c ./wpa2_supplicant.conf -i wlo1`

wlo1 is wireless interface. `ssid` is vary, change to AP's. 

### Run EAP TTLS auth service

```bash
git clone https://github.com/tknv/docker-radius-eap-ttls.git
cd docker-radius-eap-ttls
docker-compose up
```

## Configuration

No configuration at all.

## See also

[easy-rsa](https://github.com/OpenVPN/easy-rsa/) can quickly generate your certificates and keys.

## WARNING

This is for lab use only. **Not secure at all.**

## TODO

- Add windows how to.
- Add EAP-TTLS with client cert auth.
