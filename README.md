# Luvion testnet signer

A restricted Bitget Wallet handoff page for a fixed BNB Smart Chain testnet transaction. This is a development validation tool, not the full Luvion product or a general-purpose wallet.

For the product walkthrough, use the [isolated Luvion demo](https://luvion-product-demo.onrender.com/bridge). It does not require a wallet or real funds. Current product documentation is at [docs.luvion.dev](https://docs.luvion.dev/).

## Scope

- BNB Smart Chain testnet only: chain ID `97` (`0x61`).
- One sender, recipient, token contract and ERC-20 transfer payload are fixed in `index.html`.
- The displayed transfer is 1 Test USDT, with zero native value; testnet gas is still required.
- The page requests the transaction through Bitget Wallet. It does not ask for a seed phrase or private key.
- The page checks the connected account and network before submission, and disables submission when the supplied expiry has 60 seconds or less remaining.

The `request` identifier and `expires` timestamp are URL inputs. The page checks their format and time window; it does **not** cryptographically verify a Luvion authorization certificate or enforce approvals on-chain. These browser checks can be modified or bypassed and are not a production authorization boundary. A returned transaction hash is not proof of a confirmed or successful transfer; receipt verification is a separate step.

## Controlled test use

Only use this tool as part of a maintainer-coordinated test with the fixed test account. Arbitrary wallets will fail the account check.

1. Obtain the test handoff link through the agreed validation workflow. Do not fabricate an identifier or expiry to represent an approval.
2. Open it in the Bitget Wallet DApp browser with the designated test account.
3. Check the network, token, recipient and amount against the agreed test before confirming anything in the wallet.
4. If the link has expired, stop and request a new test handoff. Keep the returned transaction hash for independent receipt verification.

Never use a production wallet, real funds, private keys or seed phrases in this test. Wallet confirmation may broadcast a real transaction on the testnet.

## Source and hosting

The implementation is the static `index.html` file on the `gh-pages` branch. The [hosted test page](https://kevinluvion.github.io/luvion-testnet-signer/) is served by GitHub Pages. There is no package installation or application build step.

Open `index.html` to inspect the interface locally. Wallet behavior requires the supported wallet browser and a controlled test setup. This README documents the existing implementation; it is not an audit or a new validation report.
