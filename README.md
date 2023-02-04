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
