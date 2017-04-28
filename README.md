# VPN IPSec Setup

I am trying to collect all kinds of setups that will provide you a Virtual Private Network at home.

I seems that everything is moving to the cloud nowadays which is fine in some form but at least there should be the option use your own.

You will be able to connect safely to your private network from anywhere in the world. The private network could be your home (pfSense router) or a server in whatever datacenter you like which can host many different services.

## pfSense Setup

#### Self-signing Certificates

There are serveral ways to generate your certificates here are two

@TODO
EXPLANATION: what is a CA, why do we self-sign, ...

##### Command Line

First you have to generate the private key for your own CA. With this key you are able to generate a certificate for your CA which you will do in the next step. Note that you should keep this key private and secure.

    openssl genrsa -aes256 -out private/ca.key.pem 4096
    ...
    Enter pass phrase for private/ca.key.pem: $
    Verifying - Enter pass phrase for private/ca.key.pem: $

In this step you will generate the certificate for your CA.

IMPORTANT: The Organization Unit Name AND the FQDN has to match the hostname of your VPN server.

    # Generate the CA certificate
    openssl req -key private/ca.key.pem -new -x509 -days 7300 -sha256 -out certs/ca.cert.pem
    ...
    Country Name (2 letter code) [AU]:DE
    State or Province Name (full name) [Some-State]: NRW
    Locality Name (eg, city) []: Dortmund
    Organization Name (eg, company) [Internet Widgits Pty Ltd]: Example Ltd
    Organizational Unit Name (eg, section) []: homeserver.example.com
    Common Name (e.g. server FQDN or YOUR name) []: homeserver.example.com
    Email Address []: some@email.com

Next you need to generate a CSR (Certificate Signing Request).

    openssl genrsa -aes256 -out private/server.key.pem 4096
    openssl req -new -sha256 -key private/server.key.pem -out csr/server.csr.pem
    openssl ca -days 3650 -notext -md sha256 -in csr/server.csr.pem -out certs/server.cert.pem

##### pfSense web GUI



#### Setup Phase 1

#### Setup Phase 2

#### Add a road worrior