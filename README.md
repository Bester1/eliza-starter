# Eliza

pnpm install --no-frozen-lockfile
pnpm start --character="characters/trump.character.json"

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
- Use `pnpm start --characters="path/to/your/character.json"`
- Multiple character files can be loaded simultaneously

### Add clients

```diff
- clients: [],
+ clients: [Clients.TWITTER, Clients.DISCORD],
```

## Duplicate the .env.example template

```bash
cp .env.example .env
```

\* Fill out the .env file with your own values.

### Add login credentials and keys to .env

```diff
-DISCORD_APPLICATION_ID=
-DISCORD_API_TOKEN= # Bot token
+DISCORD_APPLICATION_ID="000000772361146438"
+DISCORD_API_TOKEN="OTk1MTU1NzcyMzYxMT000000.000000.00000000000000000000000000000000"
...
-OPENROUTER_API_KEY=
+OPENROUTER_API_KEY="sk-xx-xx-xxx"
...
-TWITTER_USERNAME= # Account username
-TWITTER_PASSWORD= # Account password
-TWITTER_EMAIL= # Account email
+TWITTER_USERNAME="username"
+TWITTER_PASSWORD="password"
+TWITTER_EMAIL="your@email.com"
```

## Install dependencies and start your agent

```bash
pnpm i && pnpm start
```
Note: this requires node to be at least version 22 when you install packages and run the agent.
