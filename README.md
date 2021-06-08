# Airbyte Tentacle
This software exists for a reason.

## Releases
There will eventually be a release.

## Setup
1. Clone this repo to your working environment
`git clone github.com/garden-of-delete/airbyte-tentacle`
2. Create a new Python3 virtual environment. For example, to use venv to create a virtual environment in your current working directory:
`python3 -m venv .venv`
Activate the environment with `. .venv/bin/activate`
3. Install all requirements:
`pip3 install requirements.txt`
4. Run Tentacle. `python tentacle.py` will display help and usage.

## Configuration as YAML

## Workflows
Airbyte tentacle supports a number of workflows designed to make managing Airbyte deployments at scale easier. Tentacle uses the .yml or .yaml

### The Sync Workflows
All the sync workflows described below are accessed through the **sync** master mode like so:

`python tentacle.py sync`

In all cases, a configuration origin, which follows the `sync` command, and a `--target` are required.

Tentacle will use the .yaml or .yml file extensions following the `source` and `--target` arguments to choose the right sync workflow.

During setup, Airbyte creates a default workspace called 'default'. Tentacle allows the user to specify an alternative existing workspace by name using the `--workspace` argument, followed by the name of the workspace.

These optional arguments can be used in combination to define what to apply the sync operation to:
- `--sources`
- `--destinations`
- `--connections`
- `--all` (same as `--sources --destinations --connections`)

**Note:** if none of the four optional arguments above are given, no changes will be made to the `--target`.

**Sync yaml to deployment**
The yaml to deployment workflow takes a .yaml file as the origin and applies the configuration contained within to a destination Airbyte deployment.

Basic usage could be something like:

`python tentacle.py sync config.yml --target http://123.456.789.0:8081 --all`

Almost all sources and destinations will have associated secrets. Tentacle ignores any secrets specified in the source config.yml. Secrets are specified separately using the `--secrets` argument, followed by a .yaml file. For example:

`python tentacle.py sync config.yml --target http://123.456.789.0:8081 --secrets secrets.yml --all`

There are a number of additional optional parameters that modify how a sync operation is carried out when syncing yaml to deployment.
- `--wipe` removes all sources, destinations, and connectors **before** applying config.yml
- `--validate` validates the sources, destinations, and connections on the destination Airbyte deployment **after** applying changes.
- `--dump` dumps the full configuration of the destination deployment to a configuration
**before** applying the sync operation.

### Sync Deployment to yaml
An existing Airbyte deployment can be written to a .yaml by following the `--target` argument with a filename having the .yaml or .yml extension. For example:

`python tentacle.py sync config.yml --target http://123.456.789.0:8081 --all`

Note in this case, no `--secrets` file is specified, since it has no meaning in this workflow. Secrets can't be extracted from the Airbyte API.

### Sync Deployment to deployment

### Wipe a deployment

### Validate a deployment

### Update a deployment

## Design

## Contributing

## Acknowledgements

## License