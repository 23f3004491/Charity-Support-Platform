![alt text](Screenshot_27-12-2025_153438_explorer.aptoslabs.com.jpeg)

# Charity Support Platform

A decentralized charity donation platform built on Aptos blockchain where users can donate to charity campaigns with all transactions tracked on-chain.

## Overview

This smart contract enables:
- Charity organizers to create fundraising campaigns with target amounts
- Donors to contribute APT coins transparently
- On-chain tracking of total donations and donor count per campaign

## Features

- **Create Campaign**: Initialize a new charity campaign with a fundraising target
- **Donate to Charity**: Contribute APT coins to any registered charity campaign
- **On-Chain Tracking**: All donations, donors, and campaign progress are recorded immutably on the blockchain

## Project Structure

```
Aptos-meetup/
├── sources/
│   └── project.move           # Smart contract code
├── Move.toml                  # Project configuration
└── README.md                  # This file
```

## Smart Contract Details

**Module Name**: `CharityModule::CharityPlatform`

**Module Address**: `f9ac9420e52ca2ffb2b157cb0340ed8ec2b4ba4bb9b73666422ad64e42287b71`

### Functions

#### 1. `create_campaign(organizer: &signer, target_amount: u64)`
Creates a new charity campaign.

**Parameters**:
- `organizer`: The account creating the campaign
- `target_amount`: The fundraising goal in APT tokens

**Example**:
```move
create_campaign(organizer, 1000000000); // 10 APT
```

#### 2. `donate_to_charity(donor: &signer, charity_address: address, amount: u64)`
Donate APT tokens to a charity campaign.

**Parameters**:
- `donor`: The account making the donation
- `charity_address`: Address of the charity organizer
- `amount`: Amount to donate in APT tokens

**Example**:
```move
donate_to_charity(donor, 0xf9ac9420..., 100000000); // 1 APT
```

### Data Structures

**CharityCampaign**
```move
struct CharityCampaign {
    total_donations: u64,   // Total funds raised
    target_amount: u64,     // Fundraising goal
    donor_count: u64,       // Number of donors
}
```

## Prerequisites

- [Aptos CLI](https://aptos.dev/tools/aptos-cli/install-cli) installed
- Aptos wallet with testnet APT tokens
- Move knowledge (basic understanding of the Move language)

## Installation & Setup

1. **Clone/Navigate to project**:
```bash
cd Aptos-meetup
```

2. **Create an Aptos profile** (if not already created):
```bash
aptos init --profile tarun1
```

3. **Fund your account** with testnet APT from the [Aptos Faucet](https://aptos.dev/tools/aptos-faucet)

## Compilation

Compile the smart contract:

```bash
aptos move compile
```

Expected output:
```
BUILDING Charity_app
Result: f9ac9420e52ca2ffb2b157cb0340ed8ec2b4ba4bb9b73666422ad64e42287b71::CharityPlatform
```

## Deployment

Deploy the contract to Aptos testnet:

```bash
aptos move publish --profile tarun1
```

This will:
1. Compile your contract
2. Create a publish transaction
3. Sign with your `tarun1` profile
4. Submit to the Aptos testnet

## Usage Examples

### 1. Create a Campaign (Command Line)

```bash
aptos move run --function-id f9ac9420e52ca2ffb2b157cb0340ed8ec2b4ba4bb9b73666422ad64e42287b71::CharityPlatform::create_campaign --args 1000000000 --profile tarun1
```

### 2. Donate to Campaign

```bash
aptos move run --function-id f9ac9420e52ca2ffb2b157cb0340ed8ec2b4ba4bb9b73666422ad64e42287b71::CharityPlatform::donate_to_charity --args @<CHARITY_ADDRESS> 100000000 --profile tarun1
```

Replace `<CHARITY_ADDRESS>` with the actual charity address.

## Verification

Check deployed modules:

```bash
aptos account list --query modules --profile tarun1
```

## Configuration

**Move.toml** settings:
```toml
[package]
name = "Charity_app"
version = "0.1.0"

[dependencies]
AptosFramework = { git = "https://github.com/aptos-labs/aptos-core.git", subdir = "aptos-move/framework/aptos-framework", rev = "mainnet" }

[addresses]
aptos_framework = "0x1"
CharityModule = "0xf9ac9420e52ca2ffb2b157cb0340ed8ec2b4ba4bb9b73666422ad64e42287b71"
```

## Testing

To test locally without deploying:

```bash
aptos move test
```

## Troubleshooting

### Compilation Errors

**Error**: "address 'aptos_framework' is not assigned a value"
- **Solution**: Ensure `Move.toml` has the correct `[addresses]` section with `aptos_framework = "0x1"`

**Error**: "Name of dependency declared does not match"
- **Solution**: Change dependency name to `AptosFramework` in `Move.toml`

### Deployment Issues

**Error**: "insufficient balance"
- **Solution**: Request more APT from the [Aptos Faucet](https://aptos.dev/tools/aptos-faucet)

## Security Considerations

- All donations are irreversible (by design)
- Only the campaign creator's address stores the campaign data
- APT tokens are transferred directly on-chain

## Future Enhancements

- Multi-sig approval for campaign creation
- Withdrawal mechanisms for organizers
- Campaign expiration dates
- Refund logic if target not met
- Campaign categorization/tags

## Resources

- [Aptos Documentation](https://aptos.dev)
- [Move Language Guide](https://move-language.github.io)
- [Aptos CLI Reference](https://aptos.dev/tools/aptos-cli)

## License

MIT

## Author

Tarun Gangwar 

---

**Questions?** Refer to the Aptos official documentation or community Discord.
