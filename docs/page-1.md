---
hidden: true
---

# Page 1

Questions from 18 November Workshop:\


1. What DID methods are currently supported?
2. How will we get the p12 file when creating oidc client?
3. How to configure mimoto in inji-web?
4. Will how credentials are stored and secured in web/mobile wallet be covered?
5. In a real-world deployment, which party configures (binds) various issuers so they are visible via the wallet?
6. Is it the service provider helping on-board the issuer?
7. Inji-web and verify is available only in the collab env? Or if any other env please share the link.
8. Keys, signatures, and proofs - can blockchain be used instead of traditional RDBMS within the context of Inji ecosystem?
9. Please once config mimoto for inji web. Whenever we are trying to do it, we are facing issues.
10. How is the credential validation happening?
11. Is VC following the W3C data model?
12. Also, when the farmerId was entered to download credentials, how is authentication with the end user happening?
13. For verify, what is the trust model? Who can verify trust/not trust?
14. Is it required to use Inji wallet with Inji certify and verify? Or can they stand on their own?
15. Is the credential whatever we are giving dummy data?
16. Where is the wallet stored?
17. There is a feature mentioned in the repository readme "Conduct offline face authentication." Can you give more details on how it works and what it uses?
18. Can you demonstrate oidc client onboarding and p12 file creation?
19. Please can you show once Inji-web configuration with mimoto? How do we connect?
20. Any scope to run AI agents for selective disclosure on top of Inji wallet where Inji wallet can provide SDK functionalities to develop various AI agents?





FAQs about Inji : MOSIP’s Digital Credentialing Stack

\
\\

General Questions on Inji:

\\

1. What are Verifiable Credentials (VCs)?

A [verifiable credential](https://www.w3.org/TR/vc-data-model-2.0/#dfn-verifiable-credential) can represent all the same information that a physical [credential](https://www.w3.org/TR/vc-data-model-2.0/#dfn-credential) represents. Adding technologies such as digital signatures can make [verifiable credentials](https://www.w3.org/TR/vc-data-model-2.0/#dfn-verifiable-credential) more tamper-evident and trustworthy than their physical counterparts. In short, VCs are secure digital certificates that can be verified cryptographically. They represent identity documents, degrees, or other trusted information.
