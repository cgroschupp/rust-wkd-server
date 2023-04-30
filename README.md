# Rust WKD server

## What is WKD?

https://wiki.gnupg.org/WKD

## Running this project

Put your __public__ keys into `./openpgp/keys`.
Files should be named after the email address that the key is registered for.
See some examples below:

- Valid names:
  - `user@example.com`
  - `user@example.com.asc` (optional `.asc` file ending will be ignored)
- Invalid names:
  - `ktujkt7nrz91b17es7prizffedzxrsna` (wkd hash -- this tool will hash the username)
  - `my-public-key.asc`

Optionally, put your policy into a text file in `./openpgp`.

```shell
cargo build --release
./target/release/wkd-server ./openpgp/keys
```

### Usage

```
Usage: wkd-server [OPTIONS] <KEYS_PATH>

Arguments:
  <KEYS_PATH>  The path where the GPG keys are stored

Options:
      --address <ADDRESS>  [env: ADDRESS=] [default: 0.0.0.0]
      --port <PORT>        [env: PORT=] [default: 8080]
  -p, --policy <POLICY>    The path to the policy file. If not set, an empty policy is served [env: POLICY=]
  -h, --help               Print help
```

### Security

This server will refuse to serve private or invalid keys.
If a file contains a private and a public key, only the public key will be served.
Nonetheless, make sure to only include your public key.
