
## Requirements before Helix Sandbox installation

Use any local hypervisor like Virtual Box, VMware and KVM or if you need a global internet access we suggest any Cloud Service Provicer (CSP) like AWS, Azure or Google. 

Minimum server configuration: 1 vCPU, 1GB RAM and 16GB HDD or SSD.

Install any Linux distribution, but Ubuntu Server 18.04 LTS has been validated exhaustively for us.

Open ports on the firewall if you are using a CSP:

```
22/TCP - SSH 
5000/TCP - Web Interface
1026/TCP - Orion Contex Broker (HTTP or HTTPs)
27017/TCP - MongoDB "Historical Data Access"
5683/UDP - CoAP
5684/UDP - CoAP with DTLS
```

### Automated installation (Let us help you with that!)

```
git clone https://github.com/fabiocabrini/helix-sandbox.git
cd helix-sandbox
chmod +x install.sh
./install.sh
choose the 1st option!
```
### Creating a CEF Context Broker 

```

Type http://<Helix_Sandbox_IP>:5000 in your web browser
Set a strong password for admin user!

```

Click [here](https://github.com/fabiocabrini/helix-sandbox/blob/master/docs/create_broker.md) to follow CEF Context Broker creation steps.

### Checking the CEF Context Broker health

```

Type http or https://<Helix_Sandbox_IP>:1026/version in your web browser.
The CEF Context Broker should return ...

```

### Response

``` 
version	"2.2.0-next"
uptime	"10 d, 7 h, 37 m, 14 s"
git_hash	"a9582a30de0e1cde19c2da2fe92a91ebd2ff41bf"
compile_time	"Mon Aug 5 18:04:03 UTC 2019"
compiled_by	"root"
compiled_in	"7516f5a020d3"
release_date	"Mon Aug 5 18:04:03 UTC 2019"
doc	"https://fiware-orion.rtfd.io/
```

### Next step

You can use the [Orion Context Broker API Walkthrough](https://fiware-orion.readthedocs.io/en/master/user/walkthrough_apiv2/index.html#before-starting) to model, create, and interact with context information.

### Manual installation (It is at your own risk!)

Server update and upgrade:

```
sudo apt update
sudo apt upgrade
```
Container engine installation:

<a href="https://docs.docker.com/install/linux/docker-ce/ubuntu/">docker</a>

<a href="https://docs.docker.com/compose/install/#install-compose">docker-compose</a>

Download the template images to prevent first-time delays deploying containers:

```
sudo docker pull mongo:3.4
sudo docker pull fiware/orion:latest
sudo docker pull fiware/cygnus-ngsi:1.9.0
sudo docker pull m4n3dw0lf/dtls-lightweightm2m-iotagent
```
If you want to use TLS/DTLS in the Orion and IoT Agents, you need to create a `/run/secrets` directory inside your host and populate with the certificate and key, you can generate a self-signed key-pair using the following command:

```
sudo mkdir -p /opt/secrets
sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /opt/secrets/ssl_key -out /opt/secrets/ssl_crt
git clone https://github.com/fabiocabrini/helix-sandbox.git
cd helix-sandbox/compose
echo "put_here_your_encryption_key" > secrets/aes_key.txt
sudo docker-compose up -d
```


