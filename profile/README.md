# 🦖 Dino Go: Location-Based NFT Game on Sui Blockchain

<p align="center">
  <img src="https://img.shields.io/badge/Blockchain-Sui-blue?logo=sui&logoColor=white" />
  <img src="https://img.shields.io/badge/Smart_Contracts-Move-orange?logo=rust&logoColor=white" />
  <img src="https://img.shields.io/badge/Storage-Walrus-green?logo=databricks&logoColor=white" />
  <img src="https://img.shields.io/badge/Security-Seal-red?logo=vercel&logoColor=white" />
  <img src="https://img.shields.io/badge/Marketplace-Kiosk-purple?logo=shopify&logoColor=white" />
  <img src="https://img.shields.io/badge/Frontend-Next.js-black?logo=next.js&logoColor=white" />
  <img src="https://img.shields.io/badge/Hosting-Vercel-black?logo=vercel&logoColor=white" />
</p>

**Dino Go** is a Web/Mobile game where players explore real-world checkpoints, collect random letters, and mint them into **Sentence NFTs**.  
Each NFT includes custom artwork stored on **Walrus decentralized storage** and is tradeable via the **Sui Kiosk marketplace**.

---

## Demo
[![](./logo.png)](https://www.youtube.com/watch?v=H0VpKQUAESw)

---

## Core Loop

1. **Explore** – Players navigate a 3D map (Google Maps + Three.js).  
   - Seal validates GPS within ~50m, blocking spoofing.

2. **Collect** – Sui's on-chain randomness fairly distributes letters (A–Z).  
   - Epoch-based claim limits prevent abuse.

3. **Create** – In the NFT Studio, letters are atomically consumed in a Move transaction.  
   - A new **Sentence NFT** is minted with metadata and Walrus CID.

4. **Trade** – The Kiosk marketplace enables:  
   - Escrow-secured trades  
   - Automatic royalties  
   - Interoperability with other Sui markets

5. **Progress** – Stats, leaderboards, and seasonal events foster community growth.

---

## Technical Implementation

### Move Smart Contracts

**Module Architecture:**  
- `user.move`  
- `checkpoint.move`  
- `nft.move`  
- `marketplace.move`

**Applied:**  
- User profiles store letter inventory as **Sui Bag objects**  
- Checkpoint claims use `sui::random` for fair distribution  
- NFT minting atomically consumes letters and embeds Walrus blob IDs 
- Implements Kiosk-compatible listing and trading logic  

**Benefits:**  
- Object-centric design prevents double-spends  
- Parallel execution supports thousands of concurrent players  
- Seamless integration with external Sui NFT marketplaces 

---

### Sui Blockchain Integration

**SDK Stack:**  
- `@mysten/dapp-kit`  
- `@mysten/sui.js`  
- `@mysten/enoki`  
- `@mysten/walrus` 
- `@mysten/kiosk` 
- `@mysten/seal`

---

### Walrus Decentralized Storage

**Implementation:**  
- Custom `WalrusClient` in `src/web3/walrusClient.ts`  
- Artwork uploaded via chunked uploads, returning a `blob_id`  

**Benefits:**  
- **10x cheaper** than on-chain storage  
- Deduplication prevents storage waste  
- Cryptographic proofs ensure integrity  

---

### Seal Threshold Encryption

**Implementation:**  
- Custom `SealClient` in `src/web3/sealClient.ts`  
- Location proofs encrypted before checkpoint validation  
- Google Maps API keys secured with distributed threshold encryption  

**Benefits:**  
- Prevents GPS spoofing  
- No single point of failure for secrets  

---

### Kiosk Marketplace

**Implementation:**  
- Custom `KioskClient` in `src/web3/kioskClient.ts`  
- NFTs automatically compatible with external Sui marketplaces  
- Move events handle fee-splitting for royalties  

**Benefits:**  
- Zero additional integration needed for cross-market trading  
- Transparent royalty distribution  

---

## Technical Strengths

- **Atomic Operations** – Move contracts prevent partial state updates during minting  
- **Cryptographic Fairness** – Sui randomness API eliminates distribution bias  
- **Decentralized Storage** – Walrus reduces costs, ensures permanence  
- **Security** – Seal encryption protects against spoofing & key compromise  
- **Interoperability** – Kiosk standard ensures cross-ecosystem NFT trading  
