Dino Go: Location-Based NFT Game on Sui Blockchain

Summary

Dino Go is a Web/Mobile game where players explore real-world checkpoints, collect random letters, and mint them into Sentence NFTs. Each NFT has custom artwork stored on Walrus decentralized storage and is tradeable via the Sui Kiosk marketplace.

Core Loop

1. Explore – Players navigate a 3D map (Google Maps + Three.js). Seal validates GPS within ~50m, blocking spoofing.
2. Collect – Sui's on-chain randomness fairly distributes letters (A–Z) with epoch-based claim limits.
3. Create – In the NFT Studio, letters are atomically consumed in a Move transaction, minting a Sentence NFT with metadata and Walrus CID.
4. Trade – Kiosk marketplace ensures escrow-secured trades, automatic royalties, and interoperability with other Sui markets.
5. Progress – Stats, leaderboards, and seasonal events foster community growth.

Technical Implementation

Move Smart Contracts

Three-Module Architecture: user.move, checkpoint.move, nft.move

- Applied: User profiles store letter inventory as Sui Bag objects. Checkpoint claims use sui::random for fair distribution. NFT minting atomically consumes letters and embeds Walrus blob IDs.
- Benefits: Object-centric design prevents double-spends; parallel execution handles thousands of concurrent players.

Sui Blockchain Integration

SDK Stack: @mysten/dapp-kit, @mysten/sui.js, @mysten/enoki

- Applied: Custom React hooks (useCheckpoints, useLetterInventory) wrap transaction building. zkLogin via Google OAuth eliminates seed phrase barriers.
- Benefits: Type-safe transactions prevent costly errors; passwordless onboarding increases user adoption.

Walrus Decentralized Storage

Direct HTTP API: Custom WalrusClient in src/web3/walrusClient.ts

- Applied: NFT artwork uploaded via chunked uploads, returns blob_id embedded in Move objects. Deduplication prevents storage waste.
- Benefits: 10x cost reduction vs on-chain storage; cryptographic proofs ensure data integrity.

Seal Threshold Encryption

Geofencing & Secrets: Custom SealClient in src/web3/sealClient.ts

- Applied: Location proofs encrypted before checkpoint validation. Google Maps API keys secured via distributed threshold encryption.
- Benefits: Prevents GPS spoofing attacks; no single point of failure for sensitive data.

Kiosk Marketplace

Standard Compliance: Custom KioskClient in src/web3/kioskClient.ts

- Applied: NFTs automatically compatible with external Sui marketplaces. Fee-splitting logic handles creator royalties via Move events.
- Benefits: Zero additional integration for cross-platform trading; transparent royalty distribution.

Technical Strengths

- Atomic Operations: Move contracts prevent partial state updates during letter consumption and NFT minting
- Cryptographic Fairness: Sui randomness API eliminates bias in letter distribution across all players
- Decentralized Storage: Walrus integration reduces costs while maintaining permanent artwork availability
- Security: Seal threshold encryption protects against location spoofing and key compromise
- Interoperability: Kiosk standard ensures NFTs work across the entire Sui ecosystem
