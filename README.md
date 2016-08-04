# redis
http://www.redis.cn/  redis 中文网
http://doc.redisfans.com/  redis 命令介绍 
https://github.com/MSOpenTech/redis  非官方支持，微软开放技术小组针对win64开发的该版本。


在使用redis时遇到的问题，设置的key不能保留在redis中，每次都会去取数据库。原因是 为给定 key 设置生存时间，当 key 过期时(生存时间为 0 )，它会被自动删除。

在 Redis 中，带有生存时间的 key 被称为『易失的』(volatile)。

生存时间可以通过使用 DEL 命令来删除整个 key 来移除，或者被 SET 和 GETSET 命令覆写(overwrite)，这意味着，如果一个命令只是修改(alter)一个带生存时间的 key 的值而不是用一个新的 key 值来代替(replace)它的话，那么生存时间不会被改变。

比如说，对一个 key 执行 INCR 命令，对一个列表进行 LPUSH 命令，或者对一个哈希表执行 HSET 命令，这类操作都不会修改 key 本身的生存时间。

另一方面，如果使用 RENAME 对一个 key 进行改名，那么改名后的 key 的生存时间和改名前一样。

RENAME 命令的另一种可能是，尝试将一个带生存时间的 key 改名成另一个带生存时间的 another_key ，这时旧的 another_key (以及它的生存时间)会被删除，然后旧的 key 会改名为 another_key ，因此，新的 another_key 的生存时间也和原本的 key 一样。

使用 PERSIST 命令可以在不删除 key 的情况下，移除 key 的生存时间，让 key 重新成为一个『持久的』(persistent) key 。

更新生存时间

可以对一个已经带有生存时间的 key 执行 EXPIRE 命令，新指定的生存时间会取代旧的生存时间。
