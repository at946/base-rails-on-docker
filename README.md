# base-rails-on-docker
This repository contains minimum required files for building the alpine linux based docker image that runs a ruby on rails application using postgresql as a database.
You can get more information on [Rails on DockerのQuickstartをalpine linuxでやってみる - Qiita](https://qiita.com/at-946/items/c69a512ea47941747b18).

# How to use

At first, you have to run `rails new` command.

```
$ docker-compose run --rm --no-deps web rails new . -f -T -d postgresql
$ docker-compose build
```

Next, you modify the setting about database.

```yaml:config/database.yml
default: &default
  adapter: postgresql
  encoding: unicode
  host: db            # add
  username: postgres  # add
  password:           # add
  pool: <%= ENV.fetch("RAILS_MAX_THREADS") { 5 } %>
```

And you create a database.

```
$ docker-compose run --rm web rails db:create
```

Now, you can run the ruby on rails application already.

```
$ docker-compose up -d
```

You can access the application on `http://localhost:3000`.
If you want to stop the container, execute the command as below.

```
$ docker-compose down
```
