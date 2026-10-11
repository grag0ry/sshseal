# sshseal

Encrypt data at rest, sealed to your ssh-agent ed25519 identity.

## How it works

sshseal asks your running `ssh-agent` to sign a random nonce with an
ed25519 key, then derives an AES-256-GCM key from that signature with
HKDF. ed25519 signatures are deterministic, so the same identity can
reproduce the key later to decrypt. The private key never leaves the
agent.

## Usage

```
sshseal identities
sshseal encrypt [--identity <fingerprint>] < plaintext > sealed.bin
sshseal decrypt < sealed.bin > plaintext
```

If `$SSHSEAL_IDENTITY` is set, `--identity` defaults to its value. Only
ed25519 keys are supported. RSA and ECDSA agent signatures are
randomized, so they cannot reproduce the same key on decrypt.

## Install

Download a prebuilt binary from the [Releases](../../releases) page, or
build from source:

```
cargo build --release
```

## Disclaimer

This is a personal hobby project, built for my own use and shared as-is.
It comes with no warranty and no security guarantee of any kind. Review
the code yourself before you trust it with anything sensitive.

## License

BSD-2-Clause, see [LICENSE](LICENSE).
