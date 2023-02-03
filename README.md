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

## insert
```go
o := orm.NewOrm()
user := User{Name: "slene"}
// insert
id, err := o.Insert(&user)
```

## sharding insert
```go
o := orm.NewOrm()
user := User{Name: "slene"}
 
// set table name to `user_1`
o.ShardingTable(
    func(tableName string) string {
        return tableName + "_1"
    },
)
 
// insert
id, err := o.Insert(&user)
```
