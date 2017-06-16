# 🌲 Timber - Simple Node Structured Logging

[![CircleCI](https://circleci.com/gh/timberio/timber-node.svg?style=svg)](https://circleci.com/gh/timberio/timber-node)
[![Coverage Status](https://coveralls.io/repos/github/timberio/timber-node/badge.svg?branch=master)](https://coveralls.io/github/timberio/timber-node?branch=master)
[![npm version](https://badge.fury.io/js/timber.svg)](https://badge.fury.io/js/timber)
[![ISC License](https://img.shields.io/badge/license-ISC-ff69b4.svg)](LICENSE.md)

* [Timber website](https://timber.io)
* [Timber docs](https://timber.io/docs)
* [Library docs](https://timberio.github.io/timber-node/)
* [Support](mailto:support@timber.io)


## Overview

Timber for Node is an optional upgrade you can install for your Node apps. Instead of completely replacing your log messages, this library automatically augments your logs with JSON metadata. Essentially turning them into rich JSON events with context. This preserves the readability of your logs while still dramatically improving the quality of your data. The end result: better logging and faster problem solving.


## How it works

For example, Timber turns this raw text log:

```
Sent 200 in 45.ms
```

Into a rich [`http_server_response` event](https://timber.io/docs/node/events-and-context/http-server-response-event/).

```
Sent 200 in 45.2ms @metadata {"dt": "2017-02-02T01:33:21.154345Z", "level": "info", "context": {"http": {"method": "GET", "host": "timber.io", "path": "/path", "request_id": "abcd1234"}}, "event": {"http_response": {"status": 200, "time_ms": 45.2}}}
```

In the [Timber console](https://app.timber.io) simply
[click the line to view this metdata](https://timber.io/docs/app/tutorials/view-metadata/).
Moreover, this data allows you to run powerful queries like:

1. `context.request_id:abcd1234` - View all logs generated for a specific request.
2. `type:http_response` - View specific events (exceptions, sql queries, etc)
3. `http_server_response.time_ms:>=1000` - View slow responses with the ability to zoom out and view them in context (request, user, etc).
4. `level:error` - Levels in your logs!

For a complete overview, see the [Timber for Node docs](https://timber.io/docs/node/overview/).


## Installation

```bash
npm install --save timber
```

## Usage

```js
var timber = require('timber');

// first we create a writeable stream that the logs will get sent to
const transport = new timber.transports.HTTPS('your-timber-api-key');

// attach the stream to stdout
timber.install(transport);
```

## Usage

<details><summary><strong>Basic logging</strong></summary><p>

No special API, Timber works directly with `console.log`:

```js
console.log("My log message")

// => My log message @metadata {"level": "info", "context": {...}}

console.info("My log message")

// => My log message @metadata {"level": "info", "context": {...}}

console.warn("My log message")

// => My log message @metadata {"level": "warn", "context": {...}}

console.error("My log message")

// => My log message @metadata {"level": "error", "context": {...}}
```

---

</p></details>

<details><summary><strong>Custom events</strong></summary><p>

Custom events are currently not supported in the current version of the Node library. We are planning to add support for them soon!

---

</p></details>

<details><summary><strong>Custom contexts</strong></summary><p>

Custom contexts are currently not supported in the current version of the Node library. We are planning to add support for them soon!


</p></details>


## Jibber-Jabber

<details><summary><strong>Which log events does Timber structure for me?</strong></summary><p>

Out of the box you get everything in the [`timber.events`](src/events) namespace.

We also add context to every log, everything in the [`timber.contexts`](src/contexts)
namespace. Context is structured data representing the current environment when the log line
was written. It is included in every log line. Think of it like join data for your logs.

---

</p></details>

<details><summary><strong>What about my current log statements?</strong></summary><p>

They'll continue to work as expected. Timber adheres strictly to the default `console` interface
and will never deviate in *any* way.

</p></details>

<details><summary><strong>How is Timber different?</strong></summary><p>

1. **It's just _better_ logging**. Nothing beats well structured raw data. And that's exactly
   what Timber aims to provide. There are no agents, special APIs, or proprietary data
   sets that you can't access.
2. **Improved log data quality.** Instead of relying on parsing alone, Timber ships libraries that
   structure and augment your logs from _within_ your application. Improving your log data at the
   source.
3. **Human readability.** Timber _augments_ your logs without sacrificing human readability. For
   example: `log message @metadata {...}`. And when you view your logs in the
   [Timber console](https://app.timber.io), you'll see the human friendly messages
   with the ability to view the associated metadata.
4. **Long retention**. Logging is notoriously expensive with low retention. Timber
   offers _6 months_ of retention by default with sane prices.
5. **Normalized schema.** Have multiple apps? All of Timber's libraries adhere to our
   [JSON schema](https://github.com/timberio/log-event-json-schema). This means queries, alerts,
   and graphs for your ruby app can also be applied to your js app (for example).

---

</p></details>

---

<p align="center" style="background: #221f40;">
<a href="http://github.com/timberio/timber-js"><img src="http://files.timber.io/images/ruby-library-readme-log-truth.png" height="947" /></a>
</p>
