# LambdaBase

Base library to create Elixir AWS Lambda

## Installation

The package can be installed by adding `lambda_base` to your list of dependencies in `mix.exs`:

```elixir
def deps do
  [
    {:lambda_base, "~> 1.0.0"}
  ]
end
```

## Basic Usage

1. Create Lambda module. Implement handle(event, context) function.

```elixir
defmodule UpCase do
  use LambdaBase
  @impl LambdaBase
  def handle(event, context) do
    {:ok, event |> Json.encode |> String.upcase}
  end
end
```

2. Create zip file for AWS Lambda.

```
$ docker run -d -it --name elx erintheblack/elixir-lambda-builder:20200112.01
$ docker cp ${project} elx:/tmp
$ docker exec elx /bin/bash -c "cd /tmp/${project}; mix deps.get; mix lambda_release"
$ docker cp elx:/tmp/${app_name}.zip .
```

3. Upload zip file and set configuration.
- Set `Module Name` to `handler`.
- Set Log level to `environment` -> `LOG_LEVEL`

The docs can be found at [https://hexdocs.pm/lambda_base](https://hexdocs.pm/lambda_base).

