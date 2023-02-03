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

### insert
```go
o := orm.NewOrm()
user := User{Name: "slene"}
// insert
id, err := o.Insert(&user)
```

### sharding insert
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

### update
```go
o := orm.NewOrm()
user := User{Name: "slene"}
 
// update
user.Name = "astaxie"
num, err := o.Update(&user)
```
### sharding update
```go
o := orm.NewOrm()
user := User{Name: "slene"}
 
// set table name to `user_1`
o.ShardingTable(
    func(tableName string) string {
        return tableName + "_1"
    },
)
 
// update
user.Name = "astaxie"
num, err := o.Update(&user)
```

### query
```go
o := orm.NewOrm()
user := User{id: 1}
 
 
// select
o.QueryTable(user).One(&user)
```
### sharding query
```go
o := orm.NewOrm()
user := User{id: 1}
 
// set table name to `user_1`
o.ShardingTable(
    func(tableName string) string {
        return tableName + "_1"
    },
)
 
// select
o.QueryTable(user).Offset(offset).Limit(limit).One(&user)
 
// select id, name from user_1 where id=1 limit 0,1
```

### delete
```go
o := orm.NewOrm()
user := User{id: 1}
 
 
// delete
o.Delete(user)
 
// delete from user_1 where id=1
```
### sharding delete
```go
o := orm.NewOrm()
user := User{id: 1}
 
// set table name to `user_1`
o.ShardingTable(
    func(tableName string) string {
        return tableName + "_1"
    },
)
 
// delete
o.Delete(user)
 
// delete from user_1 where id=1
```
