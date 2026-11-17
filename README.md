# EEA Tokenization Starter Kit

**Hackathon Track:** {track name/number}

**Status:** specification. Nothing below is built yet; the definition of done is the build plan.

An open-source kit that issues four sample regulated tokens with one command: a tokenized deposit, a money market fund share, a private credit note and an interbank deposit held by verified legal entities. Each is a standard ERC-20 with issuer controls (pause, freeze, forced transfer, redeem), and each is defined by one small config file. Every "who may hold this?" check runs through [Shibui](https://github.com/EntEthAlliance/rnd-rwa-erc3643-eas), the Enterprise Ethereum Alliance's open-source eligibility layer.

## Outcome

Any institution can try compliant tokenization in an afternoon, on a local chain or a public testnet, without writing Solidity. Investors are verified once and recognised across all tokens, and each token still applies its own rules. Natural persons prove eligibility through KYC attestations; institutions prove who they are through a GLEIF vLEI credential, so the kit covers both retail and institutional holders with the same mechanics.

## The four templates

| Template | Who may hold it (Shibui topics) | Issuance |
|---|---|---|
| Tokenized deposit | KYC + sanctions | Mint on deposit, burn on withdrawal |
| Money market fund share | KYC + AML + country | Mint on subscription, burn on redemption |
| Private credit note | KYC + accreditation + country | Mint at closing, burn at repayment |
| Interbank deposit | vLEI legal entity + sanctions | Mint on deposit, burn on withdrawal; the holder is a GLEIF-registered institution, not a person |

A template is one config file: name, symbol, required topics and trusted attesters. Adding a fourth product is a new file, not new code.

## Definition of done

- [ ] One command starts a local chain with the three tokens, Shibui and a small web console. One setting switches it to Sepolia.
- [ ] Issuance and redemption work for all four tokens.
- [ ] An investor with a single KYC attestation can hold the deposit and the fund, and is refused the credit note until they have accreditation.
- [ ] Revoking a credential blocks the investor's next transfer, with the reason shown by topic.
- [ ] A wallet holding a vLEI attestation from the bridge can hold the interbank deposit; a wallet with only KYC is refused, and the console shows the holder's LEI and legal name.
- [ ] A trusted attester can be replaced, leaving an audit trail.
- [ ] Issuer controls work: pause, freeze, forced transfer.
- [ ] Adding a fourth product takes a new config file and no new code.
- [ ] A newcomer can follow this README from a clean checkout.

## What it connects

| Piece | Role |
|---|---|
| [Shibui](https://github.com/EntEthAlliance/rnd-rwa-erc3643-eas) (EEA) | Eligibility policies: KYC, AML, sanctions, country, accreditation |
| [Ethereum Attestation Service](https://attest.org) | Where KYC providers publish and revoke credentials |
| ERC-20 and [ERC-7943](https://eips.ethereum.org/EIPS/eip-7943) | The token and its standard control interface |
| [OnChainTrust vLEI bridge](https://converter.onchaintrust.org/) and GLEIF vLEI | Legal-entity identity for institutional holders. Live on Sepolia: the bridge verifies a GLEIF vLEI credential and issues an EAS attestation (`lei`, `legalName`, `credType`, `keriAid`, `vleiSaid`, `verifiedAt`) to the holder's wallet, schema [`0x0b5f…1aa7`](https://sepolia.easscan.org/schema/view/0x0b5f333cdb7e06e0d9f7c5fbd7a151bb0d8afbcde17017390ef73b673f841aa7), attester `0x8EF2312aB6A316a0CA9Ad90661B6bccE8A7eCdc6`. Shibui reads it through its `VLEIPolicy` on claim topics 15 (legal entity) and 16 (authorised role) |
| Networks | Local, Sepolia, or a private Besu network |

## Out of scope

NAV and yield, interest, cash settlement, lock-ups, holder caps and legal treatment. A tokenized deposit is a bank liability, not a security; the kit shows the mechanics only. Shibui is a research model and this kit is a hackathon build: testnet only, not audited, not for production use.

## Installation

Not available yet. The target is one command from a clean checkout.

## Usage example

To be added with the first build: the web console walking through issuance, a refused transfer, a revocation and an attester rotation.

## Development setup

To be added with the first build.

## Roadmap

This project was built during a time-boxed FINOS hackathon. After the hackathon, if the project continues:

1. Extend the vLEI slot: authorised-role credentials (topic 16) for signatories acting for an institution, and vLEI as the identity anchor for attesters themselves.
2. Offer full ERC-3643 (T-REX) as an alternative token base.
3. Drive issuance and lifecycle events from FINOS CDM objects and a Fluxnova workflow.
4. Run a pilot with one issuer, one KYC provider and two tokens.

## Contributing

Coding agents should follow [AGENTS.md](./AGENTS.md), which requires a Developer Certificate of Origin sign-off on every commit.

**All commits** must be signed with a DCO signature to avoid being flagged by the DCO Bot. This means that your commit log message must contain a line that looks like the following one, with your actual name and email address:

```
Signed-off-by: John Doe <john.doe@example.com>
```

See [CONTRIBUTING.md](./CONTRIBUTING.md) for more information.

## License

Copyright 2026 FINOS

Distributed under the [Apache License, Version 2.0](http://www.apache.org/licenses/LICENSE-2.0).

SPDX-License-Identifier: [Apache-2.0](https://spdx.org/licenses/Apache-2.0)
