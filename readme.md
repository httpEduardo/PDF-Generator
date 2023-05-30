# Gerador de PDF com assinatura digital aplicada


## Como configurar e executar

```
git clone git@github.com

cd php-pdf-assinatura digital

instalação do compositor

# isso irá gerar um arquivo .pdf em storage/logs/
php bin/console.php app:pdf-generate
```

### Verifique a assinatura do arquivo pdf gerado

Abra https://account.ascertia.com/demos/PDFSignatureVerificationStep1 para verificar o arquivo recém-gerado



## Como a Assinatura Digital é aplicada

```
# gera novo arquivo .crt, contém certificado e chave privada
openssl req -x509 -nodes -days 365000 -newkey rsa:1024 -keyout filename.crt -out filename.crt

# converter .crt para arquivo binário .p12
openssl pkcs12 -export -in tcpdf.crt -out filename.p12

# obtém a chave privada do arquivo .p12, ele solicitará a senha/senha, então a chave privada gerada será criptografada
openssl pkcs12 -in filename.p12 -nocerts -out filename.key

# obtém o certificado do arquivo .p12
openssl pkcs12 -in filename.p12 -clcerts -nokeys -out filename.crt
```

```php
<?php
/** @var TCPDF $pdf */
$pdf->setSignature('file://PATH-TO-CRT-FILE', 'file://PATH-TO-PRIVATE-KEY-FILE', 'PRIVATE-KEY-FILE-PASSPHRASE', '', 2 , $info);
```

By Void
