# Eliza

pnpm install --no-frozen-lockfile
pnpm start --character="characters/trump.character.json"
pnpm add @elizaos/plugin-evm

Chain Configuration
By default, Ethereum mainnet is enabled. To enable additional chains, add them to your character config:

"settings": {
    "chains": {
        "evm": [
            "base", "arbitrum", "pulsechain"
        ]
    }
}
Note: The chain names must match those in the viem/chains.

Custom RPC URLs
By default, the RPC URL is inferred from the viem/chains config. To use a custom RPC URL for a specific chain, add the following to your .env file:

ETHEREUM_PROVIDER_<CHAIN_NAME>=https://your-custom-rpc-url
Example usage:

ETHEREUM_PROVIDER_IOTEX=https://iotex-network.rpc.thirdweb.com
Custom RPC for Ethereum Mainnet
To set a custom RPC URL for Ethereum mainnet, use:

EVM_PROVIDER_URL=https://your-custom-mainnet-rpc-url

## Edit the character files

Open `src/character.ts` to modify the default character. Uncomment and edit.

### Custom characters

To load custom characters instead:
pnpm start --character="characters/trump.character.json"
- Use `pnpm start --characters="path/to/your/character.json"`
- Multiple character files can be loaded simultaneously

### Add clients
```
# in character.ts
clients: [Clients.TWITTER, Clients.DISCORD],

# in character.json
clients: ["twitter", "discord"]
```

## Duplicate the .env.example template

```bash
cp .env.example .env
```

\* Fill out the .env file with your own values.

### Add login credentials and keys to .env
```
DISCORD_APPLICATION_ID="discord-application-id"
DISCORD_API_TOKEN="discord-api-token"
...
OPENROUTER_API_KEY="sk-xx-xx-xxx"
...
TWITTER_USERNAME="username"
TWITTER_PASSWORD="password"
TWITTER_EMAIL="your@email.com"
```

## Install dependencies and start your agent

```bash
pnpm i && pnpm start
```
Note: this requires node to be at least version 22 when you install packages and run the agent.

## Run with Docker

### Build and run Docker Compose (For x86_64 architecture)

#### Edit the docker-compose.yaml file with your environment variables

```yaml
services:
    eliza:
        environment:
            - OPENROUTER_API_KEY=blahdeeblahblahblah
```

#### Run the image

```bash
docker compose up
```

### Build the image with Mac M-Series or aarch64

Make sure docker is running.

```bash
# The --load flag ensures the built image is available locally
docker buildx build --platform linux/amd64 -t eliza-starter:v1 --load .
```

#### Edit the docker-compose-image.yaml file with your environment variables

```yaml
services:
    eliza:
        environment:
            - OPENROUTER_API_KEY=blahdeeblahblahblah
```

#### Run the image

```bash
docker compose -f docker-compose-image.yaml up
```
