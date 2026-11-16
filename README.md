# Noventia lists

The addresses of services that the Noventia core recognizes on Solana: launchpads, lockers, bridges, liquidity pool programs, governance programs, named programs and DEX programs. Each entry names the public source it was taken from.

These are the lists the core itself uses. The core answers them live at `GET https://core.noventia.app/v1/recognized`, with no key, and the site shows them at https://noventia.xyz/docs/what-we-recognize. The files here were read from that answer on 2026-11-16.

## The lists

| List | Id | Version | Entries | What the core does with it |
|---|---|---|---|---|
| [Exchange wallets](lists/exchanges.json) | `exchanges` | 3 | 150: 76 here, 74 linked | A wallet whose first SOL came from one of these is linked to nobody by that transfer. Tokens moved to one are counted as moved to an exchange in a distribution report. |
| [Launchpads](lists/launchpads.json) | `launchpads` | 2 | 8 | A token authority held by one of these belongs to the launchpad and does not sign in a project. A first funding from one links nobody. |
| [Lockers](lists/lockers.json) | `lockers` | 1 | 2 | Programs that hold tokens under a lock or a vesting schedule. A distribution report names the program when tokens move to it. |
| [Bridges](lists/bridges.json) | `bridges` | 1 | 12 | A bridge pays out from accounts its program owns and serves many unrelated people. A first funding that came from one links nobody, and a distribution report names the program when tokens move to it. |
| [Liquidity pool programs](lists/pool-programs.json) | `pool-programs` | 1 | 24 | A token account that belongs to a pool of one of these programs is liquidity. It is left out of the holders in a token check. |
| [Governance programs](lists/governance-programs.json) | `governance-programs` | 1 | 2 | A vote cast through one of these counts as a DAO vote in the Builder branch. |
| [Programs named in reports](lists/named-programs.json) | `named-programs` | 1 | 11 | A distribution report names these programs when tokens move to them. A program with no entry is shown by its address. |
| [Swap programs](lists/dex-programs.json) | `dex-programs` | 2 | 36 | The transaction check of the public API names these programs when a transaction calls them. A program with no entry is shown by its address, with a note that it is outside the lists. |

`index.json` holds the version of every list and `infrastructureVersion`, the version of the lists the funding graph uses (`ex3-lp2-br1`).

## What a list means

* The lists hold addresses of services and no address of a person.
* An address on no list is not recognized, and nothing is concluded from that.
* A list changes only with its version. An answer of the core names the versions it was made with.

Two things need no list:

* An address off the ed25519 curve is an account of a program. It is not treated as a common funder.
* The system program as an authority means nobody holds it.

## Exchange wallets

The core recognizes 150 exchange wallets. 76 of them are here, each with the exchange's own publication as its source: a proof-of-reserves file or page, or the exchange's own repository at a commit. The other 74 are linked. These rows come from Dune Spellbook, which is published under the Business Source License 1.1. This repository links to the file at the commit the core uses and holds no copy of them. The link and the count are in `reference` in [lists/exchanges.json](lists/exchanges.json).

## Format

Each file in `lists/` is one list:

| Field | Meaning |
|---|---|
| `id`, `kind`, `title` | the list and what kind of service it holds |
| `use` | what the core does with an address of this list, in the core's own words |
| `version` | goes up with any change of the list |
| `titleCode`, `useCode` | stable message codes of the two texts, for translation |
| `entries[].address` | the address, base58 |
| `entries[].name` | the name of the service |
| `entries[].group` | the service, when it has several addresses |
| `entries[].role` | `wallet`, `program` or `authority` |
| `entries[].source`, `entries[].sourceUrl` | where the entry was taken from, in words, and the first link in it |

## Adding or correcting an entry

See [ADDING.md](ADDING.md).

## License

The lists as collected here are under [CC BY 4.0](LICENSE). Each entry's source stays under its own terms. Attribution: "Noventia lists, https://noventia.xyz".
