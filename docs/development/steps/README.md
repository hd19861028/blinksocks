# Preparation

## Get the source

```
$ git clone https://github.com/blinksocks/blinksocks
```

## Install dependencies

```
$ cd blinksocks && npm install
```

## Start blinksocks

Prepare your configurations(**blinksocks.client.json** and **blinksocks.server.json**) in the project root folder, then start to test:

### Debug Mode(Use Chrome Developer Tool)

Debug in Chrome requires Node.js v6 and Chrome 57 or later.

```
$ npm run debug:client
$ npm run debug:server
```

Then open **chrome://inspect/#devices** in Chrome. Click **inspect** under **bin/cli-client.js** or **bin/cli-server.js**.

### Production Mode

```
$ npm run compile
$ npm run client
$ npm run server
```

This will run compiled code under **build/**.

Notice that you can change program behaviour using the following environment variants:

| NAME      | VALUE                       |
| :-------- | :-------------------------- |
| NODE_ENV  | "development", "production" |
| RUN_AS    | "server", "client"          |

If **RUN_AS** provided, log file name will be **blinksocks-[RUN_AS].log**, otherwise **blinksocks.log**. This is useful
to distinguish log files in different roles.

## Verify

Any application support HTTP/Socks5/Socks4/Socks4a can be used for verification.

For example(use curl):

```
# Socks5
$ curl -L --socks5 localhost:1080 https://www.google.com
$ curl -L --socks5-hostname localhost:1080 https://www.google.com

# Socks4
$ curl -L --socks4 localhost:1080 https://www.google.com

# Socks4a
$ curl -L --socks4a localhost:1080 https://www.google.com

# HTTP
$ curl -L -x http://localhost:1080 https://www.google.com
```

## Compile

For production use, we are running our code under `build` not `src`, so compilation is necessary.

Compilation of blinksocks is ultra easy:

```
$ npm run compile
```

This will compile `src/*` to `build/*`.

## Bundle

For portable use, we use **webpack** to compile, bundle and compress `src` into `build/blinksocks.js`:

```
$ npm run bundle
```

## Package

For users don't have Node.js installed, we use [zeit/pkg](https://github.com/zeit/pkg) to prepare compiled executables:

```
$ npm run pkg
```

This will generate compressed executables for different platforms named `blinksocks-{platform}-${arch}-${version}.gz`.
And can be distribute to target platform and architecture at once.