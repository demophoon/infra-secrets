How to openvpn for dummies.
===========================

...but like really for me in the future because i always forget the invocations of this...

Following the guide found here: https://gist.github.com/Soarez/9688998

Create the client key
---------------------
`openssl genrsa -out hydrogen.home.brittg.com.key 4096`

Create certificate signing request
----------------------------------
`openssl req -new -key ./hydrogen.home.brittg.com.key -out hydrogen.home.brittg.com.csr`

Create CA private key
---------------------
`openssl genrsa -out ca.key 4096`

Create CA Self-signed certificate
---------------------------------
`openssl req -new -x509 -key ca.key -out ca.crt`

Sign client CSR to generate a certificate
-----------------------------------------
`openssl x509 -req -in hydrogen.home.brittg.com.csr -CA ca.crt -CAkey ca.key -CAcreateserial -out hydrogen.home.brittg.com.crt`

Optionally generate new dhparams for server
-------------------------------------------
`openssl dhparam -out dhparam.pem 2048`


Setting up openvpn client
=========================

Create a client certificate with the CA certificate.

1. Install openvpn

`apt-get install openvpn`

2. Copy the openvpn client configuration found here:
https://github.com/OpenVPN/openvpn/blob/master/sample/sample-config-files/client.conf

3. Edit the file to uncomment the user and group directives if on *nix system.

4. Add paths to the CA cert, client cert, and client keys in the client.conf file.

5. Start the openvpn client:

`openvpn --config openvpn.conf`
