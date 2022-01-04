# TODO

**TODO** is a web application that introduces you to the power, performance, and simplicity of [MariaDB](https://mariadb.com/products/).

<p align="center" spacing="10">
    <kbd>
        <img src="media/demo.gif" />
    </kbd>
</p>

This application is made of two parts:

* Client
    - web UI that communicates with REST endpoints available through an API app (see below).
    - is a React.js project located in the [client](src/client) folder.
* API
    - uses [MySqlConnector](https://github.com/mysql-net/MySqlConnector) with [Dapper](https://dapperlib.github.io/Dapper/) to connect to MariaDB.
    - is a .NET solution located int the [api](src/api) folder.

This README will walk you through the steps for getting the TODO web application up and running using MariaDB.

# Table of Contents
1. [Requirements](#requirements)
2. [Getting started with MariaDB](#mariadb)
3. [Get the code](#code)
4. [Create the database and table](#schema)
5. [Configure, build and run the apps](#app)
    1. [Configure](#configure-api-app)
    4. [Build and run the .NET API app](#build-run-api)
    5. [Build and run the Client app](#build-run-client)
6. [Support and contribution](#support-contribution)
7. [License](#license)

## Requirements <a name="requirements"></a>

This sample application requires the following to be installed/enabled on your machine:

* [.NET](https://dotnet.microsoft.com/en-us/download/dotnet)
* [Visual Studio](https://visualstudio.microsoft.com/vs/)
* [Node.js (v. 12+)](https://nodejs.org/docs/latest-v12.x/api/index.html) (for the Client/UI app)
* [NPM (v. 6+)](https://docs.npmjs.com/) (for the Client/UI app)
* [MariaDB command-line client](https://mariadb.com/products/skysql/docs/clients/mariadb-clients/mariadb-client/) (optional), used to connect to MariaDB database instances.

## 1.) Getting Started with MariaDB <a name="mariadb"></a>

[MariaDB](https://mariadb.com) is a community-developed, commercially supported relational database management system, and the database you'll be using for this application.

If you don't have a MariaDB database up and running you can find more information on how to download, install and start using a MariaDB database in the [MariaDB Quickstart Guide](https://github.com/mariadb-developers/mariadb-getting-started).

## 2.) Get the code <a name="code"></a>

First, use [git](git-scm.org) (through CLI or a client) to retrieve the code using `git clone`:

```
$ git clone https://github.com/mariadb-developers/todo-app-python.git
```

Next, because this repo uses a [git submodule](https://git-scm.com/book/en/v2/Git-Tools-Submodules), you will need to pull the [client application](https://github.com/mariadb-developers/todo-app-client) using:

```bash
$ git submodule update --init --recursive
```

## 3.) Create the database and table <a name="schema"></a>

[Connect to your MariaDB database](https://mariadb.com/products/skysql/docs/clients/) (from [Step #2](#mariadb)) and execute the following SQL scripts using the following options:

a.) Use the [MariaDB command-line client](https://mariadb.com/products/skysql/docs/clients/mariadb-clients/mariadb-client/) to execute the SQL contained within [schema.sql](schema.sql).

_Example command:_
```bash
$ mariadb --host HOST_ADDRESS --port PORT_NO --user USER --password PASSWORD < schema.sql
```

**OR**

b.) Copy, paste and execute the raw SQL commands contained in [schema.sql](schema.sql) using a [client of your choice](https://mariadb.com/products/skysql/docs/clients/).

```sql
CREATE DATABASE todo;

CREATE TABLE todo.tasks (
  id INT(11) unsigned NOT NULL AUTO_INCREMENT,
  description VARCHAR(500) NOT NULL,
  completed BOOLEAN NOT NULL DEFAULT 0,
  PRIMARY KEY (id)
);
```

## 4.) Configure, Build and Run the App <a name="app"></a>

This application is made of two parts:

This application is made of two parts:

* Client
    - web UI that communicates with REST endpoints available through an API app (see below).
    - is a React.js project located in the [client](src/client) folder.
* API
    - uses [MySqlConnector](https://github.com/mysql-net/MySqlConnector) with [Dapper](https://dapperlib.github.io/Dapper/) to connect to MariaDB.
    - is a .NET solution located int the [api](src/api) folder.

The following steps, `a` through `c`, will walk you through the process of configuring, building and running the `api` and `client` applications.

### a.) Configure the app <a name="configure-api-app"></a>

Configure the MariaDB connection with **your** connection details in [appsettings.json](src/api/Todo.API/appsettings.json) file.

Example implementation:

```json
{
  "Logging": {
    "LogLevel": {
      "Default": "Information",
      "Microsoft": "Warning",
      "Microsoft.Hosting.Lifetime": "Information"
    }
  },
  "ConnectionStrings": {
    "TodoDatabase": "host=localhost;port=3306;user id=app_user;password=Password123!;database=todo;"
  },
  "AllowedHosts": "*"
}
```

### b.) Build and run the [API app](src/api) <a name="build-run-api"></a>

Build and run the application using Visual Studio. The solution will be built and the Web API project will begin listening on http://localhost:8080.

### c.) Build and run the [UI (Client) app](src/client) <a name="build-run-client"></a>

Once the API project is running you can now communicate with the exposed endpoints directly (via HTTP requests) or with the application UI, which is contained with the [client](src/client) folder of this repo.

To start the [client](src/client) application follow the instructions [here](https://github.com/mariadb-developers/todo-app-client).

## Support and Contribution <a name="support-contribution"></a>

Please feel free to submit PR's, issues or requests to this project project directly.

If you have any other questions, comments, or looking for more information on MariaDB please check out:

* [MariaDB Developer Hub](https://mariadb.com/developers)
* [MariaDB Community Slack](https://r.mariadb.com/join-community-slack)

Or reach out to us diretly via:

* [developers@mariadb.com](mailto:developers@mariadb.com)
* [MariaDB Twitter](https://twitter.com/mariadb)

## License <a name="license"></a>
[![License](https://img.shields.io/badge/License-MIT-blue.svg?style=plastic)](https://opensource.org/licenses/MIT)
