# GoDotEnv ![CI](https://github.com/joho/godotenv/workflows/CI/badge.svg) [![Go Report Card](https://goreportcard.com/badge/github.com/joho/godotenv)](https://goreportcard.com/report/github.com/joho/godotenv)

A Go (golang) port of the Ruby [dotenv](https://github.com/bkeepers/dotenv) project (which loads env vars from a .env file).

From the original Library:

> Storing configuration in the environment is one of the tenets of a twelve-factor app. Anything that is likely to change between deployment environments–such as resource handles for databases or credentials for external services–should be extracted from the code into environment variables.
>
> But it is not always practical to set environment variables on development machines or continuous integration servers where multiple projects are run. Dotenv load variables from a .env file into ENV when the environment is bootstrapped.

It can be used as a library (for loading in env for your own daemons etc.) or as a bin command.

There is test coverage and CI for both linuxish and Windows environments, but I make no guarantees about the bin version working on Windows.

## Installation

As a library

```bash
go get github.com/leonardopernett/godotenv
```

or if you want to use it as a bin command

go >= 1.17
```shell
go install github.com/leonardopernett/godotenv/cmd/godotenv@latest
```

go < 1.17
```shell
go get github.com/leonardopernett/godotenv/cmd/godotenv
```

## Usage

Add your application configuration to your `.env` file in the root of your project:

```shell
S3_BUCKET=YOURS3BUCKET
SECRET_KEY=YOURSECRETKEYGOESHERE
```

Then in your Go app you can do something like

```go
package main

import (
    "log"
    "os"

    "github.com/joho/godotenv"
)

func main() {
  err := godotenv.Load()
  if err != nil {
    log.Fatal("Error loading .env file")
  }

  s3Bucket := os.Getenv("S3_BUCKET")
  secretKey := os.Getenv("SECRET_KEY")

  // now do something with s3 or whatever
}
