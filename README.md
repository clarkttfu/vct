VSOA Command line Tool
======

A command line toolbox of VSOA in JavaScript, which runs over JSRE of SylixOS,
EdgerOS or Node.js for other platforms.

In addition to the client mode, this command line tool also works in server mode
which support data mocking and proxy mode which is able to record all the data
payloads passing through. The recorded payload could be loaded with `-l` option
to start a replay server.

## Get started

```
# start a mocking server
npx vct serv -j -b 'date/pub={time: new Date()}' localhost:3000 &

# start a proxy server (optionally)
npx vct proxy 

# connect the mocking server and listen (subscribe)
npx vct -l localhost:3000/date/pub

```

Note, installing the `vct` locally as devDependencies would make the command
startup more quickly.

## Command line options

```
vct [cli]   [options] HOST
vct s|serv  [options] HOST
vct x|proxy [options] HOST

GENERAL OPTIONS
  -h                Print this help message.
  -v                Print version info (including VSOA version).

CLIENT MODE OPTIONS

  -p PASSWORD       Client authentication password.
  [-g JSON] URL     Send GET reqeust with optional param JSON string.
  -s [JSON] URL     Send SET reqeust with optional param JSON string.
  -e                Use JSON payload as JavaScript to be evaluated.
  -w URL            Read from URL(or file) then write it to the server as stream
                    Url could be local filepath, VSOSA or HTTP GET endpoint.
  -r URL            Read stream from server then forward it to URL, which can
                      be local filepath, VSOA SET or HTTP POST endpoint that
                      accept streamed payload.
  -l PATH[..,PATH]  Listen (subscribe) comma separated topic paths.

SERVER MODE OPTIONS

  -p PASSWORD       Server password.
  -e                Execute the JSON payload as JavaScript.
  -c CERT           Certificate to be used to start a SSL server.
  -k KEY            Private KEY for the SSL cert.
  -l URL            Load saved records from stdin '-' or FILE loaded from URL.
  -r [PATH=]URL     Mock RPC responses, with JSON or binary loaded from URL.
  -g [PATH=]URL     Mock RPC GET response with JSON or binary loaded from URL.
  -s [PATH=]URL     Mock RPC SET response with JSON or binary loaded from URL.
  -d [PATH=]URL     Mock DATAGRAM response with JSON loaded from URL.
  -b [PATH=]URL     Mock pub/sub Broadcast with JSON loaded from URL.
  -e                Use loaded resource as JavaScript to be evaluated.

PROXY MODE OPTIONS

  -p PASSWORD       Server password.
  -c CERT           CERT to be used to start a SSL server.
  -k KEY            Private KEY for the SSL cert.
  -x [PATH=]URL     Proxy the VSOA server of given URL and optionally mount to
                      PATH. Multiple '-x' may be set but only one without
                      "PATH=" is acceptable.
  -r FILE           Record and save the requests to local JSON Record FILE.
  -n MAX            Maximum records to save, defaults 1000.
```

## JSON Record File

