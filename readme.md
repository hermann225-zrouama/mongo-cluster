# in configs1 do this:
1 - mongosh

2 - rs.initiate(
  {
    _id: "cfgrs",
    configsvr: true,
    members: [
      { _id : 0, host : "configs1:27017" },
      { _id : 1, host : "configs2:27017" },
      { _id : 2, host : "configs3:27017" }
    ]
  }
)

## 3- Deploy Shard cluster and activate replicaset
# in shard1s1 do this:
1 - mongosh
2 - rs.initiate(
  {
    _id: "shard1rs",
    members: [
      { _id : 0, host : "shard1s1:27017" },
      { _id : 1, host : "shard1s2:27017" },
      { _id : 2, host : "shard1s3:27017" }
    ]
  }
)

## 4- Create mongos instance
## 5- Connect to sharded cluster

in mongos : 

sh.addShard("shard1rs/shard1s1:27017,shard1s2:27027,shard1s3:27017")

#### Activate sharding for an database : 
*sh.enableSharding("[database-name")*

#### Shard collection :
*sh.shardCollection("[database].[collection]", { [field]: 1 } )*