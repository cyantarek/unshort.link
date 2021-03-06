# Unshort.link Server

This is the backend service running [unshort.link](https://unshort.link). You can build & run it yourself for even better privacy

## Building

For using up unshort.link on your own server you need a [working golang installation](https://golang.org/doc/install)

### 1) Generating assets

The assets (html, css, js,...) are directly build into the binary for more portability and an easier usage. You need to 
generate that code by entering `go generate ./...` in the main folder of the project.

### 2) Building
   
Building the project works with `go build` in the main folder of the project. (Please keep in mind that you need to generate
the assets first)

## Setup

The building process provides you with an all-inclusive binary. Just enter `./unshort.link` in your console and you should
be up and running

### Available configuration flags

- `--url`: Set the url of the server you are running on (this is only required for the frontend) (Default: `http://localhost:8080`)
- `--port`: Port to start the server on (Default: `8080`)
- `--local`: Use the assets (frontend & blacklist) directly from the filesystem instead of the internal binary storage. This helps during the development of the frontend as you do not have to do `go generate ./...` after every change. This should not be used in production. (Default: `false`)
- `--blacklist-sources`:  Comma separated list of blacklist urls to periodically sync. The blacklist should be a list of newline separated domains (Default https://hosts.ubuntu101.co.za/domains.list)
- `--sync`: Blacklist synchronization interval. The format is a number and a unit. For example `30m` or `1.5h`, available units are `"s", "m", "h"`. Mixed values are also possible: `XhXmXs` (Default: one hour)

## Development
### How to run the unit tests
Just run `go test ./...` from the command line.

## Docker

Build and run a dockerized version of the app:
```
cd server
docker build -t test/unshort .
docker run --rm --name unlink -p 8080:8080 test/unshort
