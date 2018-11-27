## Quick Introduction

This is a simplistic Rebar3 template for creating a Nitrogen
application.  To use it, clone this repository and link the resulting
directory to `~/.config/rebar3/templates/nitrogen`.  You can then run
`rebar3 new nitrogen my_app` to create an application.  To run it, `cd
my_app && rebar3 shell`.  This iteration of the sample application can
also be executed with the command `docker-compose up` assuming Docker
and friends are installed.

I know this is a hack and there are features missing (for instance,
only Cowboy is supported as the simple_bridge back end) ... pull
requests are welcome.

An additional caveat: the base image has been modified to suit my
particular needs: running with Docker, connectivity to a PostgreSQL
DB, and the addition of Bootstrap.  Your needs might differ (greatly)
but I hope removing unnecessary cruft proves easy enough.


## How to Get Going

### Prepraration

#### Docker
First, ensure that [Docker](https://docker.com) is installed on your
system.  If you're using MacOS or Windows, there's a very reasonable
[Docker Desktop](https://www.docker.com/products/docker-desktop)
available.  If Docker is correctly installed, you should be able to run 

``` 
$ docker run --rm hello-world
```

without incurring errors.

#### Erlang
Then, install [Erlang](http://erlang.org).  This installation is
required to run rebar3 (see below) but will not be the Erlang runtime
of your application.  Erlang Solutions has a nifty and up-to-date
collection of packages for a variety of systems on their [Download
Page](https://www.erlang-solutions.com/resources/download.html).

When Erlang is installed, you should be able to run `erl` and see results like 

```
Erlang/OTP 21 [erts-10.0.3] [source] [64-bit] [smp:4:4] [ds:4:4:10] [async-threads:1] [hipe] [dtrace]

Eshell V10.0.3  (abort with ^G)
1>
```

(Type `q().` to exit the Erlang shell.)

#### Rebar3

Install [rebar3](http://www.rebar3.org) either by downloading the
binary into your path or by following the instructions on the [rebar3
Getting Started](http://www.rebar3.org/docs/getting-started) page.
When installed you should be able to execute it like

```
$ rebar3 --version
rebar 3.6.1 on Erlang/OTP 21 Erts 10.0.3
```

Note that version 3.6.1 is the latest version nitrogen-template has
been tested with.


#### Install nitrogen-template

```
$ mkdir -p ~/.config/rebar3/templates
$ cd ~/.config/rebar3/templates
$ git clone git@github.com:bunnylushington/nitrogen-template nitrogen
```

### Creating and Using an Application

To create the application my_app in /var/tmp/my_app

```
$ cd /var/tmp
$ rebar3 new nitrogen my_app
```

To run the application

```
$ cd /var/tmp/my_app
$ docker-compose up
```

This will run two Docker containers: one will host the new Nitrogen
application and the other a PostgreSQL DB.  You should be able to
browse to http://localhost:3003 and see the landing page.

To connect to the Nitrogen container

```
$ docker attach my_app_fe_1
```

and if desired, run start sync

```
1> sync:go().
```

Now changes you make on your host system (in `/var/tmp/my_app/src`)
will be re-compiled on the fly.  The DB parameters are enumerated in
`/var/tmp/my_app/config/my_app.config` and should be changed for
production use.  Should you desire it, you can also use psql to
connect to the DB

```
$ docker container exec -it my_app_db_1 /bin/bash
# psql -U my_app
```

(the password also defaults to `my_app`.)

There's a default `.gitignore` file present and so git can be
initialized with the usual seqquence of

```
$ cd /var/tmp/my_app
$ git init
$ git add .
$ git commit -m "initial commit"
```

### Remarks

There are numerous ways of using Nitrogen with or without DB backends
(many of my projects rely on dets or mnesia), using PostgreSQL is not
in any way required.

The template assumes the use of Bootstram v4.  I've found that
Bootstrap and Nitrogen work well together.

There are some DB functions provided in my_app_db.erl that might be of
use.  I don't embed SQL directly in Erlang code and so expect that SQL
files will reside in `my_app/priv/sql`.

**Comments, corrections, or additions are always welcome.**
