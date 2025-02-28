# Work in progress! Not working yet!

# MySeat

This Python library can be used to work with the MySeat API.

## Get In Touch

We have an active community in our discord. [Feel free to join](https://discord.gg/t7az2hSJXq).

If you have any issues, please report them in our issue tracker.

## Quick Start

The MySkoda package is published to Pypi and can be found [here](https://pypi.org/project/myskoda/).

It can be installed the usual way:

```sh
pip install myskoda
```

### Basic example

```python
from aiohttp import ClientSession
from myskoda import MySkoda

session = ClientSession()
myskoda = MySkoda(session)
await myskoda.connect(email, password)

for vin in await myskoda.list_vehicle_vins():
    print(vin)

myskoda.disconnect()
await session.close()
```

## Documentation

Detailed documentation [is available at read the docs](https://myskoda.readthedocs.io/en/latest/):
* [Fetching Data](https://myskoda.readthedocs.io/en/latest/fetching_data/)
* [Subscribing to Events](https://myskoda.readthedocs.io/en/latest/events/)
* [Primer](https://myskoda.readthedocs.io/en/latest/primer/)

## As Library

MySkoda relies on [aiohttp](https://pypi.org/project/aiohttp/) which must be installed.
A `ClientSession` must be opened and passed to `MySkoda` upon initialization.

After connecting, operations can be performed, events can be subscribed to and data can be loaded from the API.

Don't forget to close the session and disconnect MySkoda after you're done.

## As CLI

The MySkoda package features a CLI.
You will have to install it with extras `cli`:

```sh
pip install "myskoda[cli]"
```

Afterwards, the CLI is available in your current environment by invoking `myskoda`.

Username and password must be provided to the CLI for every request as options, before selecting a sub command:

```sh
myskoda --user "user@example.com" --password "super secret" list-vehicles
```

Help can be accessed the usual way:

```sh
myskoda --help
```

## Contribute your Fixtures

Please contribute fixtures for our tests by running this command:

```sh
# Export all endpoints for all vehicles.
myskoda \
    --user user \
    --password password \
    gen-fixtures \
        --name my_cars \
        --description "My cars in no specific state."
        --vehicle all \
        get all
```

It is also possible to just contribute a single vehicle:

```sh
# Export all endpoints for a specific vehicle.
myskoda \
    --user user \
    --password password \
    gen-fixtures \
        --name my_favorite_car \
        --description "My favorite car in no specific state."
        --vehicle TMOCKAA0AA000000 \
        get all
```

Or even narrow down to an inidividual endpoint for an individual vehicle:

```sh
# Export a specific endpoint for a specific vehicle.
myskoda \
    --user user \
    --password password \
    gen-fixtures \
        --name my_favorite_car_info \
        --description "Info for my favorite car in no specific state."
        --vehicle TMOCKAA0AA000000 \
        get info
```

This will call all the selected get-routes and load all data from your vehicles (no actions will be performed).

The data will be anonymized (vin and personal data are replaced) and serves as unit tests.

Please create a pull request with the resulting data to help us cover more vehicles.

## Disclaimer

This project is an unofficial API client for the Skoda API and is not affiliated with, endorsed by, or associated with Skoda Auto or any of its subsidiaries.

Use this project at your own risk. Skoda Auto may update or modify its API without notice, which could render this client inoperative or non-compliant. The maintainers of this project are not responsible for any misuse, legal implications, or damages arising from its use.

Ensure compliance with Skoda Auto's terms of service and any applicable laws when using this software.
