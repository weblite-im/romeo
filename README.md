# Romeo

> XMPP Client

[![Build Status](https://travis-ci.org/scrogson/romeo.svg?branch=master)](https://travis-ci.org/scrogson/romeo)
[![Coverage Status](https://coveralls.io/repos/scrogson/romeo/badge.svg?branch=master&service=github)](https://coveralls.io/github/scrogson/romeo?branch=master)

## Motivation to Fork
This fork trims incoming messages before parsing to prevent unexpected errors

## Installation

1. Add romeo to your list of dependencies in `mix.exs`:

```elixir
def deps do
  [{:romeo, "~> 0.7"}]
end
```

2. Ensure romeo is started before your application:

```elixir
def application do
  [applications: [:romeo]]
end
```

## Usage

```elixir
alias Romeo.Stanza
alias Romeo.Connection, as: Conn
alias Romeo.Roster

# Minimum configuration options
opts = [jid: "romeo@montague.lit", password: "iL0v3JuL137"]

# Start the client
{:ok, pid} = Conn.start_link(opts)

# Send presence to the server
:ok = Conn.send(pid, Stanza.presence)

# Request your roster
:ok = Conn.send(pid, Stanza.get_roster)

# Join a chat room
:ok = Conn.send(pid, Stanza.join("library@muc.montague.lit", "romeo"))

# Send a message to the room
msg = "See how she leans her cheek upon her hand! " <>
      "O that I were a glove upon that hand, that " <>
      "I might touch that cheek!"
:ok = Conn.send(pid, Stanza.groupchat("library@muc.montague.lit", msg))

# Get roster items as tuple of %Romeo.Roster.Items{} struct
items = Roster.items(pid)

# Add jid to roster
:ok = Roster.add(pid, "juliet@capulet.lit")

# Remove jid from roster
:ok = Roster.remove(pid, "juliet@capulet.lit")
```

## Documentation

Documentation is available on [hexdocs](http://hexdocs.pm/romeo/)

## Naming

It follows the great tradition to use characters of William Shakespeare's Romeo
and Juliet in the XMPP specifications.

## License

The MIT License (MIT)

Copyright (c) 2015 Sonny Scroggin

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

------------

![Romeo and Juliet](https://upload.wikimedia.org/wikipedia/commons/c/cc/Picou%2C_Henri_Pierre_-_Romeo_and_Juliet.jpg
"Henri-Pierre Picou [Public domain], via Wikimedia Commons")
**Image credit:** Henri-Pierre Picou [Public domain], via Wikimedia Commons
