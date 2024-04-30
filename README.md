 TANSSi-NODE

        

![image](https://github.com/muratyazar501/TANSS--NODE/assets/136369047/13951c36-baea-4208-a549-a23bb6e1a546)


 
           


#[Website](https://www.tanssi.network/)|[Twitter](https://twitter.com/TanssiNetwork)

|[Discord](https://discord.gg/WMxTM2fQkr)

|[Explorer](https://polkadot.js.org/apps/?rpc=wss://fraa-dancebox-rpc.a.dancebox.tanssi.network#/extrinsics)
     


https://twitter.com/TanssiNetwork




Gereksimlerin yüklenmesi

```shell
wget https://github.com/moondance-labs/tanssi/releases/download/v0.6.0/tanssi-node && \
chmod +x ./tanssi-node

sudo mkdir /root/tanssi-data/

cd /root/tanssi-data/

mv /root/tanssi-node /root/tanssi-data

```

Servis kurulumunu ayarlama NODEADINIYAZ bulunan yerlere node isminizi yazmayı unutmayınız eğer hata ile adınıız yazmayı unutursanız lütfen 08 nolu koda gidiniz

```shell
sudo tee /etc/systemd/system/tanssid.service > /dev/null <<'EOF'
[Unit]
Description="Tanssi systemd service"
After=network.target
StartLimitIntervalSec=0

[Service]
Type=simple
Restart=on-failure
RestartSec=10
User=root
SyslogIdentifier=tanssi
SyslogFacility=local7
KillSignal=SIGHUP
ExecStart=/root/tanssi-data/tanssi-node \
--chain=dancebox \
--name=nodeadınıyaz \
--sync=warp \
--base-path=/root/tanssi-data/para \
--state-pruning=2000 \
--blocks-pruning=2000 \
--collator \
--database paritydb \
--telemetry-url='wss://telemetry.polkadot.io/submit/ 0' 
-- \
--name=nodeadınıyaz \
--base-path=/root/tanssi-data/container \
--telemetry-url='wss://telemetry.polkadot.io/submit/ 0' 
-- \
--chain=westend_moonbase_relay_testnet \
--name=nodeadınıyaz \
--sync=fast \
--base-path=/root/tanssi-data/relay \
--state-pruning=2000 \
--blocks-pruning=2000 
--database paritydb \
--telemetry-url='wss://telemetry.polkadot.io/submit/ 0' 

[Install]
WantedBy=multi-user.target
EOF
```

Başlatalım...


```shell
sudo systemctl daemon-reload
sudo systemctl enable tanssid.service
sudo systemctl restart tanssid.service
```
journalctl -u tanssid -fo cat

Logları kontrol edelim 


```shell
journalctl -u tanssid -fo cat
```

key oluşturalım log kodundan çıkış yapınız ctrl c


```shell
curl http://127.0.0.1:9944 -H \
"Content-Type:application/json;charset=utf-8" -d \
  '{
    "jsonrpc":"2.0",
    "id":1,
    "method":"author_rotateKeys",
    "params": []
  }'
```
