Privacy Pass is a browser extension with the aim of making the internet more accessible.

Version 2.0 of the extension is now available in [Chrome](https://chrome.google.com/webstore/detail/privacy-pass/ajhmfdgkijocedmfjonnpjfojldioehi) and [Firefox](https://addons.mozilla.org/en-US/firefox/addon/privacy-pass/)!

## How?

Privacy Pass interacts with supporting websites to introduce an anonymous user-authentication mechanism. In particular, Privacy Pass is suitable for cases where a user is required to complete some proof-of-work (e.g. solving an internet challenge) to authenticate to a service. In short, the extension receives *blindly signed* 'passes' for each authentication and these passes can be used to bypass future challenge solutions using an *anonymous redemption* procedure.  For example, Privacy Pass is supported by Cloudflare to enable users to redeem passes instead of having to solve CAPTCHAs to visit Cloudflare-protected websites.

The *blind* signing procedure ensures that passes that are redeemed in the future are not feasibly linkable to those that are signed. We use a privacy-preserving cryptographic protocol based on 'Verifiable, Oblivious Pseudorandom Functions' (VOPRFs) built from elliptic curves to enforce unlinkability. The protocol is exceptionally fast and guarantees privacy for the user. As such, Privacy Pass is safe to use for those with strict anonymity restrictions.

## The Protocol

When an internet challenge is solved correctly by a user, Privacy Pass will generate a number of random nonces that will be used as tokens. These tokens will be cryptographically *blinded* and then sent to the challenge provider. If the solution is valid, the provider will sign the blinded tokens and return them to the client. Privacy Pass will *unblind* the tokens and store them for future use.

Privacy Pass will detect when an internet challenge is required in the future for the same provider. In these cases, an unblinded, signed token will be embedded into a privacy pass that will be sent to the challenge provider. The provider will verify the signature on the unblinded token, if this check passes the challenge will not be invoked.

This protocol allows a client to bypass a number of internet challenges proportional to the number of tokens that are signed. The blinding feature used in the signing process preserves the anonymity of the user involved by randomising the tokens that are signed --- rendering them unlinkable from the tokens that are redeemed.

Cryptographically speaking, every time the Privacy Pass plugin needs a new set of privacy passes, it creates a set of thirty random numbers `t1` to `t30`, hashes them into an elliptic curve (P-256 in our case), blinds them with a value `b` and sends them along with a challenge solution. The server returns the set of points multiplied by its private key and a batch discrete logarithm equivalence proof. Each pair `(ti, HMACi(M))` constitutes a Privacy Pass and can be redeemed to solve a subsequent challenge. Voila!

Read the full protocol specification [here](https://github.com/privacypass/challenge-bypass-extension/blob/master/docs/PROTOCOL.md) and the design choices that were made [here](https://privacypass.github.io/protocol).

## Paper

We have written a [paper](https://www.petsymposium.org/2018/files/papers/issue3/popets-2018-0026.pdf) that has been accepted into the 2018 edition of the [Privacy Enhancing Technologies Symposium (PETS2018)](https://www.petsymposium.org/2018/). In the paper, we formalize the protocol and are able prove (based on discrete-log-based cryptographic assumptions) some of the security properties that we require for guaranteeing anonymity and unforgeability. We also provide more details on the implementation of the browser extension and our collaboration with Cloudflare.

## Contribute

The browser extension has been open-sourced under the BSD-3 license and is available on [GitHub](https://github.com/privacypass/challenge-bypass-extension). We have also open-sourced a reference [server implementation](https://github.com/privacypass/challenge-bypass-server) that is compatible with the extension.

Privacy Pass and the protocol that we use have undergone extensive testing and review but this is still a relatively youthful project. In particular, the implementation of DLEQ proof verification for checking that the server is using consistent keys has not been completed yet and is still under development. As such, it is possible that you may also find other issues when using the extension or within the protocol. In the case that you do then get in contact with a member of the Privacy Pass team. Code contributions to the projects are also welcome. 

For any other questions, see the [FAQ](https://privacypass.github.io/faq).

## Download

Available on [Chrome](https://chrome.google.com/webstore/detail/privacy-pass/ajhmfdgkijocedmfjonnpjfojldioehi) & [Firefox](https://addons.mozilla.org/en-US/firefox/addon/privacy-pass/).
