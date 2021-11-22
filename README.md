# orm
add sharding table implement fork from beego orm v.1.12.3

# how to sharding table?
```go
    // 1. get orm instance
    ormInstance = orm.NewOrm()
    err =ormInstance.Using("default")
    
    // 2. set table name in time
    ormInstance.ShardingTable(
        func(tableName string) string {
            return tableName + "_yyyymm"
        },
    )
    
    // 3. curd data from db
    err = ormInstance.Insert(testTableModel)
```
