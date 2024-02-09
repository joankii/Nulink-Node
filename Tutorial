STEP RUN VALIDATOR NULINK

~Minimum System Requirements
~Debian/Ubuntu (Recommended)
~30GB available storage
~4GB RAM
~x86 architecture
~Static IP address
~Exposed TCP port 9151, make sure it's not occupied
~Nodes can be run on cloud infrastructure.


1.Prepare
~Masuk Ke Root : sudo -i
~Update VPS : sudo apt-get update
~install docker https://docs.docker.com/engine
*Ubuntu Installation 

# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update


*Enter 2x 

~install ptyhon : apt install python3-pip

2.Create Worker Account
~Example on Ubuntu
This section will demonstrate how to generate a Worker account using the official build package provided by Ethereum on Ubuntu.
Download Geth, select the installation packages of various versions applicable to different systems.

wget https://gethstore.blob.core.windows.net/builds/geth-linux-amd64-1.10.23-d901d853.tar.gz

~Unzip the downloaded installation package
tar -xvzf geth-linux-amd64-1.10.23-d901d853.tar.gz

~Enter the unzipped directory
cd geth-linux-amd64-1.10.23-d901d853/

~Use. / get account new -- keystore. / keystore to generate Ethereum account and keystore
./geth account new --keystore ./keystore


You will be prompted to enter the password and confirm the password. Please remember this password for late use.
Example：
INFO [09-08|15:30:11.904] Maximum peer count                       ETH=50 LES=0 total=50
INFO [09-08|15:30:11.905] Smartcard socket not found, disabling    err="stat /run/pcscd/pcscd.comm: no such file or directory"
Your new account is locked with a password. Please give a password. Do not forget this password.
Password: 
Repeat password: 

Your new key was generated

(SIMPAN ADDRESS DAN SECRET KEY DI NOTEPAD)
Public address of the key:   0x8B1819341BEc211a45a2186C4D0030681cccE0Ee 
Path of the secret key file: /root/geth-linux-amd64-1.10.23-d901d853/keystore/UTC--2022-09-13T01-14-32.465358210Z--8b1819341bec211a45a2186c4d0030681ccce0ee


3.NuLink Worker Installation
PASTE COMMAND DI BAWAH KE VPS:

docker pull nulink/nulink:latest

cd /root

mkdir nulink

cp /root/geth-linux-amd64-1.10.23-d901d853/keystore/* /root/nulink

chmod -R 777 /root/nulink

4.RUNNING NODE 
COPAS COMMAND DI BAWAH KE VPS DAN EDIT SEDIKIT :

export NULINK_KEYSTORE_PASSWORD=<YOUR NULINK STORAGE PASSWORD>
export NULINK_OPERATOR_ETH_PASSWORD=<YOUR WORKER ACCOUNT PASSWORD>

*CONTOH : export NULINK_OPERATOR_ETH_PASSWORD=HESOYAM


~NEXT 
COPAS DAN EDIT COMMAND DI BAWAH :

$ docker run -it --rm \
-p 9151:9151 \
-v </path/to/host/machine/directory>:/code \
-v </path/to/host/machine/directory>:/home/circleci/.local/share/nulink \
-e NULINK_KEYSTORE_PASSWORD \
nulink/nulink nulink ursula init \
--signer <KEYSTORE YNAG KALIAN SIMPAN DI NOTEPAD> \
--eth-provider <NULINK PROVIDER URI>  \
--network <NULINK NETWORK NAME> \
--payment-provider <PAYMENT PROVIDER URI> \
--payment-network <PAYMENT NETWORK NAME> \
--operator-address < ADDRESS YANG KALIAN SIMPAN DI NOTEPAD> \
--max-gas-price <GWEI>


*CONTOH 
docker run -it --rm \
-p 9151:9151 \
-v /root/nulink:/code \
-v /root/nulink:/home/circleci/.local/share/nulink \
-e NULINK_KEYSTORE_PASSWORD \
nulink/nulink nulink ursula init \
--signer keystore:///code/UTC--2022-09-13T01-14-32.465358210Z--8b1819341bec211a45a2186c4d0030681ccce0ee \
--eth-provider https://data-seed-prebsc-2-s2.binance.org:8545 \
--network horus \
--payment-provider https://data-seed-prebsc-2-s2.binance.org:8545 \
--payment-network bsc_testnet \
--operator-address 0x8B1819341BEc211a45a2186C4D0030681cccE0Ee \
--max-gas-price 10000000000

~CONTOH OUTPUT DI TERMINAL KALIAN 
*COPAS PHRASE DAN PRIVATEKEY YANG MUNCUL KE NOTEPAD (KALIAN BISA ADD PK KE METAMASK)

# step 1
 Detected IPv4 address (8.219.186.125) - Is this the public-facing address of Ursula? [y/N]: y
 
 Please provide a password to lock Operator keys.
 Do not forget this password, and ideally store it using a password manager.
 
 # step 2
 Enter nulink keystore password (8 character minimum): xxxxxx
 Repeat for confirmation: xxxxxx
 
 Backup your seed words, you will not be able to view them again.
 
 xxxxxxxxxxxxxxxxxxxxxxxx
 
 # step 3
 Have you backed up your seed phrase? [y/N]: y
 
 # step 4
 Confirm seed words: xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
 
 
Public Key:   02bb2067d21a677ce928967c0ece79a9
Path to Keystore: /home/circleci/.local/share/nulink/keystore

- You can share your public key with anyone. Others need it to interact with you.
- Never share secret keys with anyone! 
- Backup your keystore! Character keys are required to interact with the protocol!
- Remember your password! Without the password, it's impossible to decrypt the key!


Generated configuration file at default filepath /home/circleci/.local/share/nulink/ursula.json

* Review configuration  -> nulink ursula config
* Start working         -> nulink ursula run

*CHECK PASSWORD KALIAN 

echo $NULINK_KEYSTORE_PASSWORD
echo $NULINK_OPERATOR_ETH_PASSWORD

*JIKA PASSWORD GAK MUNCUL BUAT PASSWORD SEPERTI SEBELUMNYA 

export NULINK_KEYSTORE_PASSWORD=<YOUR NULINK STORAGE PASSWORD>
export NULINK_OPERATOR_ETH_PASSWORD=<YOUR WORKER ACCOUNT PASSWORD>

*JALANKAN NODE NYA DI DOCKER 

docker run --restart on-failure -d \
--name ursula \
-p 9151:9151 \
-v /root/nulink:/code \
-v /root/nulink:/home/circleci/.local/share/nulink \
-e NULINK_KEYSTORE_PASSWORD \
-e NULINK_OPERATOR_ETH_PASSWORD \
nulink/nulink nulink ursula run --no-block-until-ready

*CONTOH OUTPUT DI TERMINAL KALIAN 

aa3a0f6376b566473cbcde46b0e772feb4d3658188d2cbb424a1e94588d6d8eb

*CHECK NODE STATUS DI DOCKER 

docker logs -f ursula

*CONTOH OUTPUT 

Authenticating Ursula
Loaded Ursula (horus)
✓ External IP matches configuration
Starting services
✓ Node Discovery (Horus)
✓ Work Tracking
✓ Start Operator Bonded Tracker
✓ Rest Server https://8.219.186.125:9151
Working ~ Keep Ursula Online!

#JIKA ERROR RESTART 

docker ps 

*lihat pojok kiri ada container ID 

docker restart <container ID>

########
Kirim tBNB Ke Akun Worker Kalian Untuk Jalanin Node 
Lalu Tunggu 30 menit 
Check Dashboard nulink kalian di browser lalu bonded sama address Node yang kalian jalanin tadi 
