# Time Machine DB 🐓
[![Discord](https://img.shields.io/badge/Discord-%235865F2.svg?style=for-the-badge&logo=discord&logoColor=white)](https://discord.gg/pDGNPj3dTM) 
![Status](https://img.shields.io/badge/Status-Ideation-ffb3ff?style=for-the-badge)

A distributed, fault tolerant scheduler database that can potentially scale to millions of jobs. 

The idea is to build it with a storage layer based on B+tree or LSM-tree implementation, consistent hashing for load balancing, and raft for consensus.

![Cluster animation](/docs/images/cluster_animation.gif)

## 🎯 Quick start

```bash
# Start 3 nodes. Create respective data folders 
# as data/node1/data and data/node1/raft
./create-cluster.sh 3

# To add node2 to node1 as to form cluster
❯ curl -X POST 'http://localhost:8001/cluster/join' \
-H 'Content-Type: application/json' \
--data-raw '{
 "node_id":"node2",
 "raft_address":"localhost:8102"
}'
# Do the same thing to node3.

# To check cluster health of 3 nodes
❯ ./check-health.sh 3

# More scripts coming soon
```

## 🧬 Documentation
- [Purpose](./docs/Purpose.md)
- [Architecture](./docs/Architecture.md)
- [Developer APIs](./docs/DevAPI.md) | [Job APIs](./docs/DevAPI.md#-job-apis) | [Route APIs](./docs/DevAPI.md#-route-apis)
- [TODO](./docs/TODO.md)

## 🎬 Roadmap
- [x] Core project structure
- [x] Data storage layer
    - [x] Implement BoltDB
    - [ ] Implement Badger
    - [ ] Optimise to Messagepack, proto or avro
- [ ] Bash/Make script
    - [ ] Cluster deployment
    - [ ] Build and run tests
    - [ ] Add and remove nodes
- [x] Client CRUD
    - [x] Rest interface
- [x] Node leader election
    - [x] Implement Raft
    - [x] Implement FSM
    - [x] Add/Remove nodes
- [ ] `vnode` leader election
    - [ ] Failure and restart
    - [ ] `vnode` leader and follower health check
- [ ] Node connection manager
    - [ ] GRPC contracts and message passing
    - [ ] Data replication
- [ ] Properties file
    - [ ] Validation
    - [ ] Using master properties file
- [ ] Partioner Hash function
    - [ ] Provision for clustering key
    - [ ] Re-routing via connection manager
- [ ] Restart, scale up and scale down handling
    - [ ] Invoking node and `vnode` leader election

## 🛺 Tech Stack
* Storage layer
    * [BoltDB](https://github.com/boltdb/bolt) and [BBoltDB](https://github.com/etcd-io/bbolt)
    * [BadgerDB](https://github.com/dgraph-io/badger)
    * [PebbleDB](https://github.com/cockroachdb/pebble)
* Consensus
    * [Hashicorp raft](https://github.com/hashicorp/raft)
    * [Etcd raft](https://github.com/etcd-io/etcd/tree/main/raft)
* Consistent hashing: [Hashring](https://github.com/serialx/hashring)
* Storage format
    * [MessagePack](https://github.com/vmihailenco/msgpack)
    * [Avro](https://github.com/hamba/avro)
* Message passing: [GRPC](https://github.com/grpc/grpc-go)
* Clients
    * REST
    * CLI on rest
* and more ...

## ⚽ Contribute
Coming soon. Join our discord server till then