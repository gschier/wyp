# Will You Please [![Release](https://github.com/gschier/will-you-please/workflows/Release/badge.svg)](https://github.com/gschier/will-you-please/actions?query=workflow%3ARelease)

Will you please is a script runner for local development.

![Demo GIF](https://raw.githubusercontent.com/gschier/wyp/master/screenshots/demo.gif)

## Getting Started

Install the `wyp` binary:

```bash
curl -sf https://gobinaries.com/gschier/wyp | sh
```

Generate a config file:

```bash
wyp init  # Generate ./wyp.yaml
```

Run some commands!

```bash
wyp run                           # Prompt for script to run
wyp run [name]                    # Execute script by name
wyp run [name] --watch            # Prompt and restart on file change
wyp run [name] --watch-dir ./src  # Watch specific directory

wyp combine [name...]  # Execute scripts in parallel

wyp start  # Shorthand for `wyp run start`
```

## Configuration

Configuration is defined in `wyp.(yaml|toml|json)`. An sample config can be generated by running `wyp init`.

```yaml
# ~~~~~~~~ #
# wyp.yaml #
# ~~~~~~~~ #

# Scripts are defined in a map of [name] => [config]
scripts:
  helloworld: 
    help: say hello
    run: echo 'Hello World!'
  
  sleep:
    help: get some rest
    run: 'while true; do echo "zzz"; sleep 0.5; done'
  
  build:
    help: build static assets
    run: npm run build
    watch: .
  
  # Complete example
  example:

    # Help text for command
    help: command with all options
  
    # Make available under "wyp [name]" vs default "wyp run [name]"
    root: true
  
    # Execute other scripts by name
    combine:
      - simpleGreet
      - detailedGreet

    # Code to execute for script
    run: echo "Hello World"
  
    # Define environment variables for run context
    env:
      - NAME=value
      - ANOTHER='something that needs quotes'

    # Change the directory the command is run in (default ./)
    dir: './some/other/directory'

    # Hide command from help output
    hide: true

    # Select between bash/zsh/sh (default: current shell)
    shell: bash

    # Restart when file change detected (recursive)
    watch: .
```
