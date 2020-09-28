# Possible bug demo

## TL;DR

Using elixir `1.11.0-rc.0`, calling the following in `config/runtime.exs` overwrites all other configuration for the endpoint.

    config :my_app, MyAppWeb.Endpoint,
      secret_key_base: "abc123"

## Demo

- Use the Elixir, Erlang and Node versions in `.tool-version`
- `export SECRET_KEY_BASE=some_val`
- `iex -S mix` and `Application.get_env(:my_app, MyAppWeb.Endpoint)`. Observe that only `[secret_key_base: "some_val"]` is returned.
- Comment out the `config` call in `config/runtime.exs`
- `iex -S mix` and `Application.get_env(:my_app, MyAppWeb.Endpoint)`. Observe that the keys configured under `MyAppWeb.Endpoint` in the other `config/` files are now returned.
