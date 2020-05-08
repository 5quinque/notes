# OpenSSL Commands

## Get info about certificate

`openssl req -noout -text -in mycsr.csr`

`openssl x509 -noout -text -in certificate.cer`

## Confirm certificate, private key and certificate signing request all match

`openssl x509 -noout -modulus -in certificate.crt | openssl md5`
`openssl rsa -noout -modulus -in privateKey.key | openssl md5`
`openssl req -noout -modulus -in CSR.csr | openssl md5`

## Generate new private key and certificate signing request

`openssl genrsa -out ~/domain.com.ssl/domain.com.key 2048`
`openssl req -new -sha256 -key ~/domain.com.ssl/domain.com.key -out ~/domain.com.ssl/domain.com.csr`

`openssl req -new -sha256 -key sd.fqdn.key -out test.csr -config san.cnf`

### san.cnf example file

```
[ req ]
default_bits       = 2048
distinguished_name = req_distinguished_name
req_extensions     = req_ext
[ req_distinguished_name ]
countryName                 = Country Name (2 letter code)
stateOrProvinceName         = State or Province Name (full name)
localityName               = Locality Name (eg, city)
organizationName           = Organization Name (eg, company)
OU                      = Organizational Unit
commonName                 = Common Name (e.g. server FQDN or YOUR name)
emailAddress               = Email address
[ req_ext ]
subjectAltName = @alt_names
[alt_names]
DNS.1   = sd.fqdn
```