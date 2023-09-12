# Debugging
- inspect flag
- use default 127.0.0.1:9229
- take debugging messages when it gets `SIGUSR1` signal
## use
- use remote debugging scenarios
    - `ssh -L {remote port}:localhost:9229 user@{remote site}`

## Secure
- It is not safe to expose debug port to public
    - Anyone can run any node code through that port
- 