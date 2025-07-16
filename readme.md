# stem-sdk

A TypeScript/Node.js SDK for interacting with the Stem protocol on the Solana blockchain.  
Provides abstractions for account management, peer-to-peer chat, and protocol-specific transactions.

## Features

- **Solana Account Abstractions**: Classes for managing Solana accounts, connections, and signatures.
- **Peer-to-Peer Chat**: Manage peer lists, invitations, and encrypted chat channels between wallets.
- **Protocol Transactions**: Helpers for registration, inviting, accepting/rejecting peers, and sending messages.
- **Borsh Serialization**: Uses borsh schemas for efficient on-chain data encoding/decoding.
- **Event-driven**: Emits events for account and chat updates.

## Installation

```bash
npm install stem-sdk
```

## Usage

```ts
import { Connection, Account } from "stem-sdk/dist/solana";
import { Stem } from "stem-sdk/dist/stem";
import { PublicKey } from "@solana/web3.js";

// Connect to Solana
const conn = new Connection("https://api.mainnet-beta.solana.com");

// Your wallet public key
const myPubkey = new PublicKey("...");

// Create Stem instance
const stem = new Stem(myPubkey, conn, true);

// Register, invite, accept, send messages, etc.
```

## API Overview

### Solana Abstractions

- `Connection`: Wraps Solana RPC/WebSocket, provides account management and airdrop.
- `Account`: Represents a Solana account, supports fetching and subscribing to changes.
- `Signature`: Handles transaction signature status and confirmation.

### Stem Protocol

- `Stem`: Main class for protocol logic (registration, peer management, chat).
  - `init()`: Loads and subscribes to descriptor and chat accounts.
  - `createRegisterTx()`: Returns a transaction for registering.
  - `createInviteTx(pubkey)`: Returns a transaction to invite a peer.
  - `createAcceptTx(pubkey)`: Accepts an invite.
  - `createRejectTx(pubkey)`: Rejects an invite.
  - `createSendMessageTx(pubkey, message)`: Sends a message to a peer.
  - Event emitters: `onChatsUpdated`, `onStatusUpdated`, `onChatUpdated`.

### Helpers

- `helpers.getDescriptorPda(pubkey)`: Returns PDA for a wallet descriptor.
- `helpers.getChatPda(pubkey, peer)`: Returns PDA for a private chat.
- `helpers.getChatHash(pubkey, peer)`: Deterministic hash for chat.

### Types

- `PeerStatus`: `Invited`, `Requested`, `Accepted`, `Rejected`
- `Descriptor`, `Peer`, `Chat`, `Message` and their borsh-encoded variants.

### Constants

- `PROGRAM_ID`: Stem protocol program on Solana.
- `SEED_DESCRIPTOR`, `SEED_PRIVATE_CHAT`: Seeds for PDA derivation.

## Dependencies

- `@solana/web3.js`
- `borsh`

## Development

- TypeScript, CommonJS output.
- No tests included by default.
- See `src/` for implementation details.

## License

MIT
