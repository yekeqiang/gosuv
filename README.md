# gosuv
golang port of python-supervisor

# Plugin Design

All command plugin will store in `$HOME/.gosuv/cmdplugin`, gosuv will treat this plugin as a subcommand.

for example:

	$HOME/.gosuv/cmdplugin/ --.
		|- showpid/
			|- run

There is a directory `showpid`

When run `gosuv showpid`, file `run` will be called.

# Design

Has a folder `.gosuv` under `$HOME` path.

Here is the folder structure

	$HOME/.gosuv
		|-- gosuv.json
		|-- logs/
			  |-- program1.log
		      |-- program2.log

For first run `gosuv` command, will run a golang server.

Server port default 17422 or from env defined `GOSUV_SERVER_PORT`.

When server get `TERM` signal, all processes spwaned by srever will be killed.

## How to add program to gosuv
Eg, current folder is in `/tmp/hello`

	gosuv add --name "program1" -- ./program1 1888

Will add a record to `$HOME/.gosuv/gosuv.json`

	{
		"name": "program1",
		"command": ["./program1", "1888"],
		"dir": "/tmp/hello",
		"env": [],
	}

Show status

	$ gosuv status
	program1		RUNNING

Stop program, ex: "program1"

	$ gosuv stop program1
	program1 stopped

## Program not implement

## LICENSE
[MIT](LICENSE)
