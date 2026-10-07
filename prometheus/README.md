# Prometheus metrics

To run Prometheus and Graphana use the following command.

```shell
docker-compose up
```

Open http://localhost:3000 in your browser to access the Graphana web interface.
Username and password are both `admin`.

NOTE: you'll need to make the JSON-RPC server on the validator node listen on an address
Prometheus can reach - in the setup below that is `0.0.0.0`. The validator JSON-RPC has no
authentication, so treat that listener as trusted-network only: `/_metrics` is served on the
same port as `/json_rpc`, so exposing the metrics endpoint also exposes every JSON-RPC
method, including `prepare_layer_one_transaction`, which signs transactions with the node's
own key. Prefer a private interface; if you must bind `0.0.0.0`, firewall the port so that
only Prometheus can connect.
To do this, you do one of the following:

- edit the `config.toml` file in the validator node's data directory and set the
  `validator_node.json_rpc_listener_address`
- use the `--json-rpc-listener-address` command line argument when starting the validator node
- if using swarm, set `listen_ip` setting to 0.0.0.0
