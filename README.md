# H2 Docker

This project creates a Docker container image that embeds an H2 database and includes H2 tools such as the [console](https://www.h2database.com/javadoc/org/h2/tools/Console.html?highlight=console&search=console) and [shell](https://www.h2database.com/javadoc/org/h2/tools/Shell.html?highlight=shell&search=shell).

## Quick Start

Clone this repository and then execute the following.

```bash
mvn package docker:build docker:run
```

This will build and run a Docker container that holds H2. Open a browser and navigate to: http://localhost:8080. You will be presented with a login dialog.

![Login](docs/h2-console-login.png)

The project does not actually create a database but you may create one by attaching to the container and executing the H2 shell to do so.

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

Test the connection.

![Test Connection](docs/h2-test-connection.png)

You now may connect to the database.

![H2 Console](docs/h2-console.png)

To stop the container use `Ctrl+C`. Following is a summary.

```bash
[INFO] --------------------------------[ pom ]---------------------------------
[INFO]
[INFO] --- maven-dependency-plugin:2.8:copy (copy) @ h2-docker ---
[INFO] Configured Artifact: com.h2database:h2:1.4.200:jar
[INFO] com.h2database:h2:1.4.200:jar already exists in .../h2-docker/src/main/docker
[INFO]
[INFO] --- docker-maven-plugin:0.36.0:build (default-cli) @ h2-docker ---
[INFO] Building tar: .../docker-build.tar
[INFO] DOCKER> [h2-docker:latest] "dockerfile": Created docker-build.tar in 63 milliseconds
[INFO] DOCKER> [h2-docker:latest] "dockerfile": Built image sha256:5a28c
[INFO]
[INFO] --- docker-maven-plugin:0.36.0:run (default-cli) @ h2-docker ---
[INFO] DOCKER> [h2-docker:latest] "dockerfile": Start container 9fbb28e27abe
dockerfile> Web Console server running at http://172.17.0.2:8082 (others can connect)
dockerfile> Failed to start a browser to open the URL http://172.17.0.2:8082: Browser detection failed, and java property 'h2.browser' and environment variable BROWSER are not set to a browser executable.
dockerfile> TCP server running at tcp://172.17.0.2:9092 (only local connections)
dockerfile> PG server running at pg://172.17.0.2:5435 (only local connections)
[INFO] DOCKER> [h2-docker:latest] "dockerfile": Stop and removed container 9fbb28e27abe after 0 ms
```

## References

1. [H2 Console](https://www.h2database.com/javadoc/org/h2/tools/Console.html?highlight=console&search=console)
1. [H2 Shell](https://www.h2database.com/javadoc/org/h2/tools/Shell.html?highlight=shell&search=shell)
1. [Creating New Databases](http://www.h2database.com/html/tutorial.html#creating_new_databases)
