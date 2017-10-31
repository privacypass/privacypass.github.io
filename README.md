Privacy Pass is a browser extension that makes the internet more accessible.

## How?

Privacy Pass interacts with supporting websites to reduce the number of internet challenges that are witnessed by honest users (such as CAPTCHAs). In short, the extension receives *anonymously signed* 'passes' for each correct challenge solution. These passes can be used to bypass future challenge solutions.

The *anonymous* signing procedure ensures that passes that are redeemed in the future are not feasibly linkable to those that are signed. We use a privacy-preserving cryptographic protocol based on 'Verifiable, Oblivious Pseudorandom Functions' (VOPRFs) built from elliptic curves to enforce unlinkability. The protocol is exceptionally fast and guarantees privacy for the user. As such, Privacy Pass is safe to use for those with strict anonymity restrictions.

## The protocol

When an internet challenge is solved correctly by a user, Privacy Pass will generate a number of random nonces that will be used as tokens. These tokens will be cryptographically *blinded* and then sent to the challenge provider. If the solution is valid, the provider will sign the blinded tokens and return them to the client. Privacy Pass will *unblind* the tokens and store them for future use.

Privacy Pass will detect when an internet challenge is required in the future. In these cases, an unblinded, signed token will be embedded into a privacy pass that will be sent to the challenge provider. The provider will verify the signature on the unblinded token, if this check passes the challenge will not be invoked.

This protocol allows a client to bypass a number of internet challenges proportional to the number of tokens that are signed. The blinding feature used in the signing process preserves the anonymity of the user involved by randomising the tokens that are signed --- rendering them unlinkable from the tokens that are redeemed.

Read the full protocol description [here](https://github.com/privacypass/challenge-bypass-extension/blob/master/PROTOCOL.md).

## Contribute

The browser extension has been open-sourced and is available on [GitHub](https://github.com/privacypass/challenge-bypass-extension). We have also open-sourced a reference [server implementation](https://github.com/privacypass/challenge-bypass-server) that is compatible with the extension.

If you find any issues then feel free to let us know. Contributions are also welcome. 

## Download

Available on Chrome & Firefox.

## Team

- [Alex Davidson](https://github.com/alxdavids), Royal Holloway, University of London
- [Ian Goldberg](https://cs.uwaterloo.ca/~iang/), University of Waterloo
- [Nick Sullivan](https://github.com/grittygrease)
- [George Tankersley](https://github.com/gtank) 
- [Filippo Valsorda](https://github.com/filosottile) 
