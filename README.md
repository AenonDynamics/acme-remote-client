acme-tiny
=====================================
This is an extensions of [acme-tiny](https://github.com/diafygi/acme-tiny), a small and simple audtiable python script that you can use to issue and renew [Let's Encrypt](https://letsencrypt.org/) certificates.
It can talk to any [ACME](https://letsencrypt.github.io/acme-spec/) based web services to issues [X509v3](https://en.wikipedia.org/wiki/X.509) certificates based on your CSR.

Features
--------------------------------------

  * **CSR in, CERT out - no less, no more**
  * Intended to use with [Let's Encrypt](https://letsencrypt.org/)
  * Ability to run on a dedicated Certificate Management Host
  * Upload hook to transfer the http-challenge-token
  * Domain Validation via [SimpleHTTP/http-01](https://letsencrypt.github.io/acme-spec/#simple-http) challenge
  * Runs as normal user - not root/sudo required
  * Easily to integrate into existing PKI management environments

Audience
--------------------------------------

This derived version is targeted to people who are familar with **Let's Encrypt, X509 certificate management (PKI), webserver administration (nginx, apache, lighttpd, ..) and server management!**
It's a small tool which can be integrated into your existing toolchain to manage X509 certificates.
It does only talk to the [Let's Encrypt Authority](https://letsencrypt.org/) to validate your domain name and issue a certificate.

The webserver management is **on yours!** You have to create your CSR by yourself and install the generated certificates manually.

**If you plan to use this tool on a single server, please take a look on the [original vesion](https://github.com/diafygi/acme-tiny) before using this extended one!**

**If you are a beginner or don't understand what I just said, this script likely isn't for you! Please use the official [Let's Encrypt client](https://github.com/letsencrypt/letsencrypt)**

Preface
--------------------------------------



Usage
--------------------------------------

### Step 1: Create a Let's Encrypt account private key (if you haven't already)

You must have a public key registered with Let's Encrypt and sign your requests with the corresponding private key.
To accomplish this you need to initially create a key, that can be used by acme-tiny, to register a account for you and sign all following requests.

```shell
# create a new 4096bit RSA Keypair
openssl genrsa -out .letsencrypt/account.pem 4096
```

### Step 2: Create or Provide CSR (Certificate Signing Request)

I assume that you are familar with this procedure. The tool requires the CSR to be in **DER** format.

#### Example: Convert PEM to DER

```shell
openssl req -in mysite_com.csr -outform DER -out mysite_com.der
```

### Step 3: Run the Tool

```shell
python acme_tiny.py --account-key ./.letsencrypt/account.pem --csr ./requests/mysite_com.der --acme-dir ./.challenges --out ./certs/mysite_com.cert --token-upload ./$1/upload.sh
```

### Step 4: Install the certificates

Finally you have to install the certificate manually on your Webserver.

License
-------

**amce-tiny** is OpenSource and licensed under the Terms of [The MIT License (X11)](http://opensource.org/licenses/MIT). You're welcome to contribute!
The original [acme-tiny](https://github.com/diafygi/acme-tiny) is created by [Daniel Roesler](https://github.com/diafygi) - Many thanks!
