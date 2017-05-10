# weatherspeaker
[![version](https://img.shields.io/badge/version-v1.2.0-red.svg)](https://github.com/marrakchino/weatherspeaker/releases)
[![license](http://img.shields.io/badge/license-mit-blue.svg)](https://opensource.org/licenses/MIT)

**weatherspeaker** | a command-line weather forecast speaker. It allows the user to hear the weather forecast of a particular location for a particular date.


## Dependencies

* **espeak** is a compact opensource software speech synthesizer for English and other languages. You can download it [here](http://www.espeak.sourceforce.net).

* **OpenWeatherMap** is an online service that provides weather data. You must get an API key [here](http://openweathermap.org/API).

* **jq** is an opensource lightweight command line JSON processor. You can download it [here](http://stedolan.github.io/jq/download) depending on your Linux distro.

## Getting and using an API key from OpenWeatherMap

1. You need to sign up with a valid username and email: http://home.openweathermap.org/users/sign_up

2. Get an API key from [this](http://openweathermap.org/api) link, the basic free API works. You might want to chose another existing offer.
The API key might take several minutes before it becomes valid. To test it, check that you get weather information for Marrakesh when visiting this link:
`http://api.openweathermap.org/data/2.5/forecast/city?id=2542997&APPID=<YOUR_API_KEY_HERE>`

# Configuration

## Configuration file

You can directly store your settings in a dedicated file: `config/.weatherspeaker.conf` (or set the variable `CONFIG_FILE` to another directory of your choice) in the following format:

```sh
key:<YOUR_API_KEY>
id:<YOUR_DEFAULT_CITY_ID>
```

The order of the lines is indifferent, but make sure there are no trailing spaces or useless characters. 

Ideally, you can provide the two lines. Still, only the API key is required. Indeed, when the script doesn't find a default city ID, it estimates your location based on your IP address and converts the city name into a city ID based on the API city list. 

However, this solution is not recommended although operational for accuracy reasons.

### Resetting the variables

You can overwrite these environment variables (if you happen to change the city or to use a new API key) by invoking `init`:

```sh
$ weatherspeaker init
API Key already exists in /home/marrakchino/github/weatherspeaker/config/.weatherspeaker.conf, overwrite it? [y]es, [n]o y
New API key: 123456789
[API KEY] Overwrote API key in /home/marrakchino/github/weatherspeaker/config/.weatherspeaker.conf
Default city ID already exists in /home/marrakchino/github/weatherspeaker/config/.weatherspeaker.conf, overwrite it? [y]es, [n]o y
New city ID: 1234554321
[City ID] Overwrote city ID in /home/marrakchino/github/weatherspeaker/config/.weatherspeaker.conf
```

## Setting environment

Otherwise, you may (will) have to export these environment variables (adding them to your `~/.bashrc` file for example):

`export OPENWEATHERMAP_APIKEY=<YOUR_API_KEY>`

`export WTSPEAK_DEFAULT_CITY_ID=<DEFAULT_CITY_ID>` 

# Usage 

```sh
$ weatherspeaker --help
weatherspeaker - Command line weather forecast speaker
Options:
    [--days | -d] <nb_of_days>         Return weather forecast for the day (tomorrow + <nb_of_days>), default: 1.
    [--config-file | -c] <path>        Use a custom configuration file located in <path>.
    [--trace | --verbose]              Activate tracing.
    [--help | -h]                      Show this help and exit.
    [--version | -v]                   Display the version of the program and exit.
    [init]                             Initialize and configure your personal parameters (API Key and city ID).

    Github repository: 		     http://gihthub.com/marrakchino/weatherspeaker
```

# Cron

You can `cron` this job to run periodically, e.g.:

```sh
# Runs weatherspeaker every day at 10 p.m.
0 22 * * * weatherspeaker >> /path/to/weatherspeaker.log 2>&1
```

# TODO

All contributions are welcome. The project is still relatively small, therefore feel free to fork the repository and send pull requests.
A non-exhaustive list of suggested unsolved bugs/improvement ideas is given hereafter:

* Check if there are any open [issues](http://github.com/marrakchino/weatherspeaker/issues) and see whether you can contribute by fixing them.

* Improve the weather forecast script.

* Add new languages for the forecast based on the system language (see `locale`), or on the region (IP Address).

* Write a Makefile containing, among other stuff, an 'install' rule.

* Eventually extend the project to other platforms (Windows, MacOS).

# Licence

**weatherspeaker** is released under the MIT licence, see `LICENCE` file for more details.

