# gotestfmt-logger

A wrapper around [`gotestfmt`](https://github.com/ubuntu/gotestfmt) that
consumes `go test -json` on stdin, writes the output of failed tests to stdout, 
and saves the full test output to a logfile.

This is useful to only get the information needed to debug failed tests on
stdout while still keeping a full record of the test run in a logfile.

It also strips lines from the output of `go test -json` which `gotestfmt`
doesn't handle correctly.

## Installation

Install `gotestfmt`:

```bash
go install github.com/ubuntu/gotestfmt/v2/cmd/gotestfmt@latest
```

Install `gotestfmt-logger` into a directory in your `$PATH`:
```bash
mkdir -p "$HOME/.local/bin"
curl -o "$HOME/.local/bin/gotestfmt-logger" https://raw.githubusercontent.com/adombeck/gotestfmt-logger/main/gotestfmt-logger
chmod +x "$HOME/.local/bin/gotestfmt-logger"
```

## Usage

Pipe the output of `go test -json` into `gotestfmt-logger`:

```bash
go test -json ./... | gotestfmt-logger
```

By default, the logfile is saved to temporary file which is printed to `stderr`:
```bash
gotestfmt-logger: Logging to /tmp/gotestfmt.Ahk9PT.log
```

You can specify the logfile path with the `--logfile` flag:
```bash
go test -json ./... | gotestfmt-logger --logfile test.log
```
