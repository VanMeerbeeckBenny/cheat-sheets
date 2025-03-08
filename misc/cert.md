### create cert
## create private ca key(do not use -aes256 for traefik)
openssl genrsa -aes256 -out ca-key.pem 4096
## create corresponding ca cert
openssl req -new -x509 -sha256 -days 365 -key ca-key.pem -out ca.pem
## check info if you need
openssl x509 -in ca.pem -text
## cert key maken voor domain
openssl genrsa -out cert-key.pem 4096
## generate certificate to sign request
openssl req -new -sha256 -subj "/CN=textcn" -key cert-key.pem -out cert.csr
## create config file to set the domain
echo "subjectAltName=DNS:*.com.local" >> extfile.
##inspect if needed
cat extfile.cnf
## generate certificate from the certificate sign request
openssl x509 -req -sha256 -days 3650 -in cert.csr -CA ca.pem -CAkey ca-key.pem -out cert.pem -extfile extfile.cnf -CAcreateserial




