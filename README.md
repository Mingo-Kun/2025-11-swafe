# Swafe audit details
- Total Prize Pool: $100,000 in USDC 
    - HM awards: up to $81,600 in USDC
        - If no valid Highs or Mediums are found, the HM pool is $0
    - QA awards: $3,400 in USDC
    - Judge awards: $2,500 in USDC
    - Scout awards: $500 in USDC
    - Mitigation Review: $12,000 in USDC
- [Read our guidelines for more details](https://docs.code4rena.com/competitions)
- Starts November 18, 2025 20:00 UTC 
- Ends December 9, 2025 20:00 UTC 

### ❗ Important notes for wardens
1. Judging phase risk adjustments (upgrades/downgrades):
    - High- or Medium-risk submissions downgraded by the judge to Low-risk (QA) will be ineligible for awards.
    - Upgrading a Low-risk finding from a QA report to a Medium- or High-risk finding is not supported.
    - As such, wardens are encouraged to select the appropriate risk level carefully during the submission phase.

## Publicly known issues

_Anything included in this section is considered a publicly known issue and is therefore ineligible for awards._

Denial of service for HTTP endpoints not in scope.

✅ SCOUTS: Please format the response above 👆 so its not a wall of text and its readable.

# Overview

[ ⭐️ SPONSORS: add info here ]

## Links

- **Previous audits:**  No previous audit reports.
  - ✅ SCOUTS: If there are multiple report links, please format them in a list.
- **Documentation:** https://github.com/swafe-io/swafe-book
- **Website:** https://swafe.io/
- **X/Twitter:** https://x.com/swafe_io

---

# Scope

[ ✅ SCOUTS: add scoping and technical details here ]

### Files in scope
- ✅ This should be completed using the `metrics.md` file
- ✅ Last row of the table should be Total: SLOC
- ✅ SCOUTS: Have the sponsor review and and confirm in text the details in the section titled "Scoping Q amp; A"

*For sponsors that don't use the scoping tool: list all files in scope in the table below (along with hyperlinks) -- and feel free to add notes to emphasize areas of focus.*

| Contract | SLOC | Purpose | Libraries used |  
| ----------- | ----------- | ----------- | ----------- |
| [contracts/folder/sample.sol](https://github.com/code-423n4/repo-name/blob/contracts/folder/sample.sol) | 123 | This contract does XYZ | [`@openzeppelin/*`](https://openzeppelin.com/contracts/) |

### Files out of scope
✅ SCOUTS: List files/directories out of scope

# Additional context

## Areas of concern (where to focus for bugs)
Scope:

lib/
api/
contracts/


Primary Security Concerns:

1. Unauthorized backup reconstruction
2. Unauthorized account recovery - Without email verification and (optionally) guardian approval
3. Backup ciphertext security - Stealing or lack of binding for backup ciphertexts to accounts
4. Integrity attacks - Mauling of stored secrets/backups
5. Privacy violations - Anonymity violations from on-chain content or off-chain node interaction, including leakage of user identity (e.g., email addresses)

✅ SCOUTS: Please format the response above 👆 so its not a wall of text and its readable.

## Main invariants

- Only the owner of an account should be able to request the reconstruction of a backup.
- Only the owner of an email should be able to request the recovery of an account.
- Recovery of an account only occurs when more than the specified threshold of Guardians has approved the request.
- Recovery of a backup only occurs when more than the specified threshold of Guardians has approved the request.
- After recovering an account, the owner should be able to request and complete recovery of backups as long as at there is sufficient Guardians online and off-chain nodes available for relaying shares.
- An email should be associated to at most one account at a time.
- An account may have multiple emails associated for recovery.
- A user should be able to recover his account with only access to his email (and an out-of-band channel for communicating with Guardians).

✅ SCOUTS: Please format the response above 👆 so its not a wall of text and its readable.

## All trusted roles in the protocol

1. Swafe-io
Trusted for:
Keeping user emails confidential
Providing "email certificates" only after users prove email possession
Generating shares for the VPRF used to hide email ↔ account association during a one-time setup ceremony.

Explicitly NOT trusted for:
Unilaterally causing Guardians to reconstruct or recover an account without explicit permission provided by each guardian.


2. Guardians
Trust Model: Honest threshold assumption.
If a user specifies a reconstruction threshold of t out of n nodes, we assume at least t of the selected guardians for that backup are honest for liveness and n-t for secrecy.

Key Assumptions:
Any number of corrupted guardians may exist in the system
Honest users manually select guardians they trust (friends, family, trusted institutions)
The user-selected threshold t at least t guardians are willing to reconstruct.
The user-selected threshold t at most t-1 guardians are corrupted/malicious.

Exception: If both conditions hold:
- Swafe-io is honest
- Off-chain nodes are honest

Then backups/accounts remain unrecoverable even if all Guardians are corrupted.

3. Off-chain Nodes
Off-chain nodes are full nodes capable of running off-chain computation and holding secret state. Security guarantees vary based on the corruption model:

All off-chain nodes are honest:
- User emails remain hidden even at registration/recovery time

A minority of off-chain nodes are honest:
- Snapshot of corrupted off-chain node states hides user emails and account associations. Leaking an off-chain node's state does not reveal user emails or their association to on-chain contracts
- Secrets without specified guardians remain decryptable without a valid "email certificate" from Swafe.
- The system remains available even if a minority subset of off-chain nodes are offline or unresponsive

A majority of off-chain nodes are corrupted:
- Secrets specifying guardians remain undecryptable

✅ SCOUTS: Please format the response above 👆 using the template below👇

| Role                                | Description                       |
| --------------------------------------- | ---------------------------- |
| Owner                          | Has superpowers                |
| Administrator                             | Can change fees                       |

✅ SCOUTS: Please format the response above 👆 so its not a wall of text and its readable.

## Running tests

Install Rust and just, then:

just install-deps
just test

✅ SCOUTS: Please format the response above 👆 using the template below👇

```bash
git clone https://github.com/code-423n4/2023-08-arbitrum
git submodule update --init --recursive
cd governance
foundryup
make install
make build
make sc-election-test
```
To run code coverage
```bash
make coverage
```

✅ SCOUTS: Add a screenshot of your terminal showing the test coverage

## Miscellaneous
Employees of Swafe and employees' family members are ineligible to participate in this audit.

Code4rena's rules cannot be overridden by the contents of this README. In case of doubt, please check with C4 staff.


# Scope

*See [scope.txt](https://github.com/code-423n4/2025-11-swafe/blob/main/scope.txt)*

### Files in scope


| File   | Logic Contracts | Interfaces | nSLOC | Purpose | Libraries used |
| ------ | --------------- | ---------- | ----- | -----   | ------------ |
| /api/src/account/get.rs | ****| **** | 12 | ||
| /api/src/account/mod.rs | ****| **** | 1 | ||
| /api/src/association/get_secret_share.rs | ****| **** | 14 | ||
| /api/src/association/mod.rs | ****| **** | 3 | ||
| /api/src/association/upload_msk.rs | ****| **** | 16 | ||
| /api/src/association/vdrf/eval.rs | ****| **** | 13 | ||
| /api/src/association/vdrf/mod.rs | ****| **** | 1 | ||
| /api/src/init.rs | ****| **** | 24 | ||
| /api/src/lib.rs | ****| **** | 4 | ||
| /api/src/reconstruction/get_shares.rs | ****| **** | 14 | ||
| /api/src/reconstruction/mod.rs | ****| **** | 2 | ||
| /api/src/reconstruction/upload_share.rs | ****| **** | 16 | ||
| /cli/src/commands/account.rs | ****| **** | 299 | ||
| /cli/src/commands/association.rs | ****| **** | 241 | ||
| /cli/src/commands/backup.rs | ****| **** | 182 | ||
| /cli/src/commands/mod.rs | ****| **** | 6 | ||
| /cli/src/commands/reconstruction.rs | ****| **** | 65 | ||
| /cli/src/commands/utils.rs | ****| **** | 126 | ||
| /cli/src/commands/vdrf.rs | ****| **** | 135 | ||
| /cli/src/main.rs | ****| **** | 540 | ||
| /contracts/src/http/endpoints/account/get.rs | ****| **** | 31 | ||
| /contracts/src/http/endpoints/account/mod.rs | ****| **** | 10 | ||
| /contracts/src/http/endpoints/association/get_secret_share.rs | ****| **** | 47 | ||
| /contracts/src/http/endpoints/association/mod.rs | ****| **** | 21 | ||
| /contracts/src/http/endpoints/association/upload_msk.rs | ****| **** | 59 | ||
| /contracts/src/http/endpoints/association/vdrf/eval.rs | ****| **** | 49 | ||
| /contracts/src/http/endpoints/association/vdrf/mod.rs | ****| **** | 10 | ||
| /contracts/src/http/endpoints/init.rs | ****| **** | 65 | ||
| /contracts/src/http/endpoints/mod.rs | ****| **** | 4 | ||
| /contracts/src/http/endpoints/reconstruction/get_shares.rs | ****| **** | 31 | ||
| /contracts/src/http/endpoints/reconstruction/mod.rs | ****| **** | 19 | ||
| /contracts/src/http/endpoints/reconstruction/upload_share.rs | ****| **** | 52 | ||
| /contracts/src/http/error.rs | ****| **** | 89 | ||
| /contracts/src/http/json.rs | ****| **** | 25 | ||
| /contracts/src/http/mod.rs | ****| **** | 115 | ||
| /contracts/src/lib.rs | ****| **** | 88 | ||
| /contracts/src/storage.rs | ****| **** | 22 | ||
| /lib/src/account/mod.rs | ****| **** | 112 | ||
| /lib/src/account/tests.rs | ****| **** | 635 | ||
| /lib/src/account/v0.rs | ****| **** | 646 | ||
| /lib/src/association/mod.rs | ****| **** | 78 | ||
| /lib/src/association/v0.rs | ****| **** | 628 | ||
| /lib/src/backup/mod.rs | ****| **** | 36 | ||
| /lib/src/backup/tests.rs | ****| **** | 450 | ||
| /lib/src/backup/v0.rs | ****| **** | 359 | ||
| /lib/src/crypto/commitments.rs | ****| **** | 283 | ||
| /lib/src/crypto/curve.rs | ****| **** | 8 | ||
| /lib/src/crypto/email_cert.rs | ****| **** | 131 | ||
| /lib/src/crypto/hash.rs | ****| **** | 97 | ||
| /lib/src/crypto/mod.rs | ****| **** | 16 | ||
| /lib/src/crypto/pairing.rs | ****| **** | 348 | ||
| /lib/src/crypto/pke/mod.rs | ****| **** | 469 | ||
| /lib/src/crypto/pke/v0.rs | ****| **** | 268 | ||
| /lib/src/crypto/poly.rs | ****| **** | 128 | ||
| /lib/src/crypto/sig/mod.rs | ****| **** | 75 | ||
| /lib/src/crypto/sig/v0.rs | ****| **** | 124 | ||
| /lib/src/crypto/sss.rs | ****| **** | 148 | ||
| /lib/src/crypto/symmetric.rs | ****| **** | 188 | ||
| /lib/src/crypto/vdrf.rs | ****| **** | 336 | ||
| /lib/src/encode.rs | ****| **** | 243 | ||
| /lib/src/errors.rs | ****| **** | 51 | ||
| /lib/src/lib.rs | ****| **** | 12 | ||
| /lib/src/node.rs | ****| **** | 52 | ||
| /lib/src/types.rs | ****| **** | 91 | ||
| /lib/src/venum.rs | ****| **** | 259 | ||
| **Totals** | **** | **** | **8722** | | |

### Files out of scope

*See [out_of_scope.txt](https://github.com/code-423n4/2025-11-swafe/blob/main/out_of_scope.txt)*

| File         |
| ------------ |
| Totals: 0 |

