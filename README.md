# InwxDomrobot
[INWX](https://www.inwx.com/en/) offers a complete XML-RPC API covering most of
their sites features. The DomRobot API allows you to manage accounts, domains,
name servers and much more directly from your application. Considering the way
their API is built, this package merely acts as a cookie storage and an XML
encoder/decoder proxy.

## Installation
Install from [hex.pm](https://hex.pm/packages/inwx_domrobot)

```elixir
def deps do
  [{:inwx_domrobot, "~> 0.1.0"}]
end
```

## Usage
```elixir
# Start a new connection
iex(1)> {:ok, conn} = InwxDomrobot.start_link
{:ok, PID<0.213.0>}

# Send an "account.login" request to the connection
iex(2)> InwxDomrobot.login conn, "username", "password"
{:ok, 1000}

# Send arbitrary commands to the connection
iex(3)> InwxDomrobot.query conn, "account.info"
{:ok, %{param: %{"code" => 1000,
  ...
}}}

iex(4)> InwxDomrobot.query conn, "account.update", [%{ firstname: "Sven" }]
{:ok, %{param: %{"code" => 1001,
  ...
}}}

# Send an "account.logout" request to the connection
iex(5)> InwxDomrobot.logout conn
{:ok,
 %{param: %{"code" => 1500,
    "msg" => "Command completed successfully; ending session",
    "runtime" => 0.0264, "svTRID" => "..."}}}
```
