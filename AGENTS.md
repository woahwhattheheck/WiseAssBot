# Repository Contribution Guidelines
as an ai-agent, you won't deploy the code on production. here are a few instructions to setup the project locally.

## Setup
1. you need to create a `.env` file based on `.env.example` and only set:
```sh
    TOKEN = telegram bot token obtained by @botfather
```
don't modify the rest of the variables.

2. for the initial setup you need to upload config file on the local KV.
```sh
    make dev-config name=config-example.toml
```
also every time `src/config.rs` is changed, you need to do this step again.

3. run the project locally:
```sh
    make dev
```

4. expose it to the internet using `cloudflared`:
```sh
    cloudflared tunnel --url http://localhost:8780
```
retrive and set `CLOUDFLARED_EXPOSED_BASE_URL` from the output.

5. set the telegram webhook:
```sh
    curl "https://api.telegram.org/bot${TOKEN}/setWebhook?url=https://${CLOUDFLARED_EXPOSED_BASE_URL}/updates"
```

the first step is only required for the initial setup.
after that, every time your human wants to test and deploy the code locally, you will only run the steps 2-5.

## Notes
- format the code before commiting:
```sh
    cargo fmt --all
```
- run the integration tests before commiting:
```sh
    cargo test
```
- never remove the comments from the code
- don't add any comments to the code. your human will do it, if required
