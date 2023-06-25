# State Sync

#### **Step 1: Stop service, reset data.**

{% code overflow="wrap" %}
```
sudo systemctl stop cascadiad
cp $HOME/.cascadiad/data/priv_validator_state.json $HOME/.cascadiad/priv_validator_state.json.backup
cascadiad tendermint unsafe-reset-all --home $HOME/.cascadiad --keep-addr-book
```
{% endcode %}



**Step 2: Get and configure state sync.**

It would be best to get an active RPC endpoint and its peer. Also, it would be better to know the frequency of the snapshot to adapt the following row with a correct value `SYNC_BLOCK_HEIGHT=$(($LATEST_HEIGHT - 300))`, otherwise, state-sync will be failed.

Below is an example of one of the working validator's peer

{% code overflow="wrap" %}
```
STATE_SYNC_RPC=https://cascadia.rpc.liveraven.net:443
STATE_SYNC_PEER=5126c2904cf4d9ed9b2c6cd203fccbe3983229da@cascadia.rpc.liveraven:22656
LATEST_HEIGHT=$(curl -s $STATE_SYNC_RPC/block | jq -r .result.block.header.height)
SYNC_BLOCK_HEIGHT=$(($LATEST_HEIGHT - 300))
SYNC_BLOCK_HASH=$(curl -s "$STATE_SYNC_RPC/block?height=$SYNC_BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $SYNC_BLOCK_HEIGHT $SYNC_BLOCK_HASH

sed -i \
    -e "s|^enable *=.*|enable = true|" \
    -e "s|^rpc_servers *=.*|rpc_servers = \"$STATE_SYNC_RPC,$STATE_SYNC_RPC\"|" \
    -e "s|^trust_height *=.*|trust_height = $SYNC_BLOCK_HEIGHT|" \
    -e "s|^trust_hash *=.*|trust_hash = \"$SYNC_BLOCK_HASH\"|" \
    -e "s|^persistent_peers *=.*|persistent_peers = \"$STATE_SYNC_PEER\"|" \
    $HOME/.cascadiad/config/config.toml

mkdir -p $HOME/.cascadiad/data && mv $HOME/.cascadiad/priv_validator_state.json.backup $HOME/.cascadiad/data/priv_validator_state.json
```
{% endcode %}



**Step 3: Restart service, check logs.**

{% code overflow="wrap" %}
```
sudo systemctl start cascadiad && sudo journalctl -u cascadiad -fn 100 -o cat
```
{% endcode %}
