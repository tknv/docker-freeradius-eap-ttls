# EAP TTLS authentication

This helps quick setup EAP TTLS for testing WPA2-Enterprise EAP TTLS and WPA3-Enterprise EAP TTLS (GCMP256).  
[FreeRadius](https://github.com/FreeRADIUS/freeradius-server) service it.

## Quick start

```bash
git clone https://github.com/tknv/docker-radius-eap-ttls.git EAP-TTLS_FreeRadius
cd EAP-TLS_FreeRadius
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
**Network name** should be SSID (if use EAP TLS auth for wireless client). **Security type** `WPA2-Enterprise` even want to test `WPA3-Enterprise`. Later can change it to `WPA3-Enterprise`.   

At Setting tick belows;

* Use a certificate on this computer
* Use simple certificate selection(Recommended)
* Verify the server's identity by validating the certificate
* Trusted Root Certification Authorities
    * AWASLab  "which installed at previously as ca.crt"
    * pc  "which installed at previously as pc.p12"

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
