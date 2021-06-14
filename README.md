# H2 Docker

This project create a Docker container that embeds the H2 database.

```bash
mvn package docker:build docker:run
```

```bash
docker exec -it h2-docker-1 bash
root@6b2d5d36b53b:/# java -cp h2.jar org.h2.tools.Shell \
  -url jdbc:h2:/data/h2.test -user sa -password test

Welcome to H2 Shell 1.4.200 (2019-10-14)
Exit with Ctrl+C
Commands are case insensitive; SQL statements end with ';'
help or ?      Display this help
list           Toggle result list / stack trace mode
maxwidth       Set maximum column width (default is 100)
autocommit     Enable or disable autocommit
history        Show the last 20 statements
quit or exit   Close the connection and exit

sql> SELECT 1;
1
1
(1 row, 21 ms)
sql> quit
Connection closed
root@3b7fbd9cd4c7:/# ls /data
h2.test.mv.db
```

## References

1. [H2 Console](https://h2database.com/javadoc/)
