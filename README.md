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

