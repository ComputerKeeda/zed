## Step 4: Binding to Connections and Channels

A light client by itself is only an engine that stores verified block hashes. To use it for packet verification:

1. **Connection Handshake (`MsgConnectionOpenInit`):** The connection explicitly references the `client_id`:

   ```protobuf
   message MsgConnectionOpenInit {
     string client_id = 1; // "07-tendermint-14"
     Counterparty counterparty = 2; // References Chain A's client
     ...
   }
   ```

2. **Channel Creation (`MsgChannelOpenInit`):** Channels bind to the connection.

When a packet arrives via `MsgRecvPacket`, the path resolution is deterministic:
$$\text{Channel} \longrightarrow \text{Connection} \longrightarrow \text{ClientID}\ \ (`07\text{-tendermint-}14`) \longrightarrow \text{AppHash} \longrightarrow \text{Verify Merkle Proof}$$
