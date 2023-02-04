# create-ssl-cert-using-openssl



## creat eprivate key 
```
openssl genrsa -des3 -out domain.key 2048

```

## Create a cert signing request (CSR)
```
openssl req -key domain.key -new -out domain.csr
```

## Or you can create both at once with \
```
openssl req -newkey rsa:2048 -keyout domain.key -out domain.csr
```
## create a self-signed certificate
```
openssl x509 -signkey domain.key -in domain.csr -req -days 365 -out domain.crt
```
# cretae A CA signed certificate with our Own CA
```
openssl req -x509 -sha256 -days 1825 -newkey rsa:2048 -keyout rootCA.key -out rootCA.crt
```
### make sure to put enter pem pass phrase password
## create a conffig file domain.ext with this content
```
authorityKeyIdentifier=keyid,issuer
basicConstraints=CA:FALSE
subjectAltName = @alt_names
[alt_names]
DNS.1 = domain
```
### The “DNS.1” field should be the domain of our website.
## freestar
##Then we can sign our CSR (domain.csr) with the root CA certificate and its private key:
```
openssl x509 -req -CA rootCA.crt -CAkey rootCA.key -in domain.csr -out domain.crt -days 365 -CAcreateserial -extfile domain.ext
```
### As a result, the CA-signed certificate will be in the domain.crt file.
## View the certificates
```
openssl x509 -text -noout -in domain.crt
```
![image](https://user-images.githubusercontent.com/107158398/216734626-ee1b358c-b0d7-49c3-b018-11e9a99df3b4.png)


