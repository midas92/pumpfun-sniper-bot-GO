
# Pump-Fun Sniper Bot

This repository contains a simple Pump and Dump sniper bot, which is not for sale. It is intended for educational purposes and experimentation only.

## Configuration

### Environment Variables

- `PRIVATE_KEY`: The bot pulls the bot wallet's private key from this environment variable.
- `PROXY_URL`: Set this to an https proxy if you want to proxy the main RPC client

### Main Configuration

The main configuration values for the bot are located in `main.go` and can be edited as needed.

- **Public RPCs**: A slice of public RPC URLs that can be used to help transmit transactions can be modified in the `sendTxRPCs` string slice variable.
- **RPC and WebSocket URLs**: Set `rpcURL` and `wsURL` to their proper values for a high-performance Solana RPC (Note: free/cheap RPC services will likely be ratelimited immediately due to the number of requests needed to vet coins and their creators).
- **MySQL Database**: Ensure you have an instantiated MySQL database with information on coins created. Modify the credentials below as needed:
  ```go
  sql.Open("mysql", "root:XXXXXX!@/CoinTrades")
  ```

### Bot Instantiation

The bot is instantiated with the following parameters:

```go
// Purchase coins with 0.05 Solana, priority fee of 200000 microlamports
bot, err := NewBot(rpcURL, wsURL, privateKey, db, 0.05, 200000)
if err != nil {
    log.Fatal(err)
}
```
### Jito Integration

To remove Jito integration, comment out the following block:

```go
if err := bot.beginJito(); err != nil {
    log.Fatal("Error Starting Jito", err)
}
```

## Installation and Running the Bot

1. **Clone the Repository**:
    ```sh
    git clone https://github.com/1fge/pump-fun-sniper-bot.git
    cd pump-fun-sniper-bot
    ```

2. **Install Dependencies**:
    Ensure you have [Go](https://go.dev/doc/install) installed. Then, run:
    ```sh
    go mod tidy
    ```

3. **Set Environment Variables**:
    Ensure `PRIVATE_KEY` is set in your environment.

4. **Edit Configuration**:
    Modify the RPC URLs, WebSocket URLs, and MySQL database credentials in `main.go` as needed.

5. **Run the Bot**:
    ```sh
    go run .
    ```
