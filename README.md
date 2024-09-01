## Checkseed: Custom Electrum-Compatible Mnemonics

### Overview

**Checkseed** is a tool that allows users to create custom mnemonic phrases that can be used as a seed in Electrum, a widely used Bitcoin wallet. Unlike BIP-39, where the seed is derived from a predefined dictionary of words, Electrum uses the hash of the mnemonic phrase to generate the master key. This characteristic enables Electrum to accept any mnemonic phrase, making it possible to create personalized mnemonics while still generating valid wallets.

### How It Works

Electrum determines the wallet version by examining the first bits of the hash generated from the mnemonic phrase. If the beginning of the hash does not match a recognized wallet version, Electrum will reject the mnemonic. Checkseed solves this issue by automatically appending a nonce to the user-provided mnemonic. This nonce is adjusted until the hash of the entire mnemonic (including the nonce) starts with the correct bits for a supported wallet version, such as `SegWit` or `Standard`.

[See more](https://github.com/spesmilo/electrum/blob/bd845080b852ab19c54c2c4bd5ec8a36255b9e35/electrum/mnemonic.py)

### Example Workflow

1. **User Input**: Begin with a custom phrase, such as "i liek bitcoin ".

2. **Automatic Nonce Search**: Checkseed automatically appends and adjusts a nonce to the input phrase, hashing the result repeatedly until the hash begins with the required bits for the desired wallet version.

3. **Result**: The process produces a mnemonic like "i liek bitcoin 178", where "178" is the nonce that makes the hash valid for the selected wallet version.

### Important Considerations

- **Security Risks**: Custom mnemonics often have lower entropy compared to randomly generated ones, making them more susceptible to collisions or brute-force attacks. This increases the risk of funds being compromised. It's important to thoroughly understand these risks before using Checkseed-generated mnemonics in a live wallet.

- **Electrum Compatibility**: After generating the mnemonic, it should be tested to confirm that it correctly generates the intended wallet in Electrum and that the correct wallet version is recognized.

### Disclaimer

Using low-entropy, human-generated mnemonics as wallet seeds introduces significant security risks, including the potential loss of funds. For securing substantial amounts of cryptocurrency, it is strongly recommended to use standard, randomly generated mnemonics. Custom mnemonics should only be used with a full understanding of the associated risks.

### Live demo:

Live demo is hosted here:
[https://kenyerman.github.io/checkseed](https://kenyerman.github.io/checkseed)
