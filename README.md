# Robot Challenge

The description of the problem can be found in [PROBLEM.md](PROBLEM.md).

## Usage

### Docker

To avoid dependency issues the application is dockerised, build the docker image first:

```bash
docker build -t robot_challenge .
```

We can now run it:

```bash
docker run -it robot_challenge
```

For a more interactive experience, we can run bash inside the docker container:

```bash
docker run -it --entrypoint /bin/bash robot_challenge
```

We can now run the application or test etc. (see next section for commands)

### Without docker

You need ruby, version is specified in `.ruby-version`

The executable script is `bin/robot_challenge`.

If you want to run tests you can `bundle exec rspec spec` or `bundle exec rake spec`.

This repo is built like a gem, so `bundle install` will bring in dependencies, the only dependencies are `rake` and `rspec`
(and `bundler`), there are no runtime dependencies (this is by design).

You can do `bin/robot_challenge -h` and it should print out some info for you.

To summarise, the simplest way to run it is just `bin/robot_challenge`, it will sit there waiting for input. You can start entering
commands, errors will be printed for invalid commands or invalid arguments (for place command). Nothing will be printed for valid
commands that were successfully executed, you'll have to use the report command to see if it's doing the right thing.

Commands (and arguments for PLACE) can be lower or upper case.

For more fun, I suggest running it like this `bin/robot_challenge -r ascii`, this is similar to above, but after every command it
will print out an ascii representation of the table e.g.:

```bash
> bin/robot_challenge -r ascii
place 3,3,south
---------------------
|   |   |   |   |   |
---------------------
|   |   |   | v |   |
---------------------
|   |   |   |   |   |
---------------------
|   |   |   |   |   |
---------------------
|   |   |   |   |   |
---------------------
```

There is a file with some test data `test_data.txt`, you can pipe it to executable:

```bash
bin/robot_challenge < test_data.txt
```

It has some commands before a place, an invalid command and a bunch of other stuff, it should produce the following output:

```plain
Invalid command given FOOBAR
1,1,NORTH
1,3,NORTH
1,3,EAST
3,3,EAST
1,0,EAST
0,0,SOUTH
0,0,SOUTH
0,0,NORTH
0,1,NORTH
```

