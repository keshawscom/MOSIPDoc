# Glossary

This section mainly comprises a list of terms in the identity domain along with their definitions.

<details>

<summary>Digital ID Wallet</summary>

A digital ID wallet is a tool that stores and manages personal information and identity credentials securely in a digital format. It helps people keep their information organized and protected. This wallet ensures the safety of personal data and makes it easily accessible when needed.

</details>

<details>

<summary>Good ID</summary>

Good ID refers to a set of principles and practices that encompass secure, inclusive, and privacy-respecting methods for digital identity. It emphasizes the following key attributes:

1. **Secure**: Good ID systems should prioritize security, ensuring that individuals' identities are protected from theft and unauthorized access. This involves robust authentication methods and data encryption.
2. **Inclusive**: Good ID systems should be accessible to all, regardless of socio-economic status, location, or personal circumstances. They should not exclude or discriminate against any group.
3. **Privacy-Respecting**: Good ID systems should respect individuals' privacy by minimizing the collection and use of personal data to only what is necessary and by implementing strong data protection measures.
4. **User-Centric**: Good ID focuses on user control and consent, allowing individuals to manage and control their digital identities.
5. **Interoperable**: It's essential that different ID systems can work together, fostering compatibility and reducing the need for individuals to manage multiple, fragmented identities.
6. **Open Standards**: Open, transparent standards should underpin Good ID systems to ensure they can be independently reviewed and are not controlled by a single entity.
7. **Sustainability**: Good ID systems should be sustainable in the long term, considering the environmental impact, cost, and resource requirements.

These principles are essential for building trustworthy and ethical digital identity systems that benefit both individuals and the organizations and services that rely on them.

</details>

<details>

<summary>Identity Systems</summary>

Identity systems, in the context of digital identity and access management, refer to the infrastructure, processes, and technologies used to manage and verify the identities of individuals or entities in the digital realm. These systems play a crucial role in ensuring secure and controlled access to various online services, platforms, and resources.

</details>

<details>

<summary>Identity Verification</summary>

Identity verification is the important process of ensuring that a person is who they claim to be to avail of various government and private sector services.

This process allows one to confirm one's identity and confirm the validity of details shared on the relying party's online portal.

Let us understand the different models and their pros and cons.

* **Assisted model:** In this model, an assistant lends his system or uses it on behalf of the user. While using this model, it is important not to use a password for user verification.
  * Biometric verification is passwordless, making verification equitable for everyone. Biometric capture is based on [SBI](https://docs.mosip.io/1.1.5/biometrics/biometric-specification). This specification allows a general-purpose biometric device (of course compliant with the specification) to capture anyone's biometrics and verify them. This allows the use of biometrics beyond the personal device.
  * OTP: Passwordless, but will require access to one's phone. Biometrics, in rare cases, can reject a valid user. Our OTP solution bridges the divide in these scenarios.
* **Self-authentication** - In this model, a user can verify themselves. This is a well-known model and has been in use over the internet.
  * QR Code - By using a selfie image in a smartphone, one can authenticate locally on their phone and use the enrolled private key to release an authentication token. This mode allows the usage of a personal smartphone as an authenticator.

</details>

<details>

<summary>Relying Party</summary>

A relying party is a service provider that depends on an identity provider for authentication and identity verification, enabling users to access their services securely and conveniently.

They are typically online services, websites, or applications that need to verify the identity of users for access control, personalization, or other purposes.

The identity provider, often utilizing protocols like [OpenID Connect](https://openid.net/connect/), provides authentication and identity information to the relying party, allowing users to access the service without having to create a new account or authenticate separately for each relying party.

</details>




Define ID registry plugin

ID Registry plugin carries on with the same approach and philosophy to integrate the Signup Service as well, Now the Signup service integrate with any Id registry system. Now the tight integration of signup service with MOSIP ID-repository has been done away with.

...

Tight integration of signup service with MOSIP ID-repository should be removed. Follow the same eSignet plugin approach to integrate signup service with any ID registry systems.

In signup service version < 1.1.0, Integration was used to create user identity entry and update user identity. Validation of the input user identity data was carried out in signup service before posting the request to MOSIP ID repository. ID repository also validated the identity data in the request using MOSIP defined Identity schema.

Once the data is validated and saved in ID repo, the same was published to MOSIP IDA. Only after the identity data is published to IDA, end user will be able to authenticate via eSignet using the created identity. So it is required for signup service to check the status of the identity in ID registry before confirming registration completion to the end user.

Note: eSignet connects to MOSIP IDA via 'Authenticator' plugin.



...


## Overview

Signup portal display list of Verifiers and end user can choose one among them and start the verification process.


Claims in a user profile can be verified by any trusted verifier. 

Verified claims and the verification metadata itself could be stored in the ID registry. 

An authenticated user can go through the verification process in signup portal to update his/her profile with verification metadata and mark claims as verified.



** Verification process can be online or offline involving manual steps or consist of both online & manual steps. 




### Video based verification:

Video based online verification process is designed and supported with Signup portal. **Considering online verification in-scope for 1.1.0.

Online video based process verification allows for:

1. Liveliness check
2. Face match
3. Document verification
4. Disability check


So with this it is understood that every verification process can consist of any combination of steps. 

Signup service should be able to **start** the process and **end** the process when signalled by the chosen verifier. End step should expect verification details which should be updated in 
ID registry against the authenticated end user individual ID.





### How is the user authenticated context shared with the signup portal?
Authentication of user before verification process can be carried out in eSignet(OP). Authenticated user's transaction is shared as an id_token_hint to the signup portal. 
Signup portal now takes the role of an RP and starts OIDC flow in eSignet with "mosip:idp:acr:id-token" ACR. As the authroize request already contains id_token_hint, user will not be prompted to enter credentials, but still may prompt to user to provide consent only if required. 
Most of the time, "sub" claim in the userinfo response should suffice the requirement.


## Provision to integrate with any Identity verification workflow
Signup service has a provision to add any steps between **start** and **end** step in the verification workflow. We have defined [IdentityVerifierPlugin.java](../../signup-integration-api/src/main/java/io/mosip/signup/api/spi/IdentityVerifierPlugin.java) abstract class. 

Verifier should only take care of

1. Initializing every workflow run with required configuration based on the provided input. 
2. Verify the input frame based on the current step and publish the feedback or details about the next step to start in this run to kafka (publishAnalysisResult concrete method is already defined in the plugin abstract class).
3. Once the verifier decides to **end** the workflow run, it should hint the signup service by publishing **end** step details using the same publishAnalysisResult concrete method.
4. Signup service will invoke the getVerificationResult method implemented by the verifier to fetch the verification details. VerificationResult can either be failure or successful. The same will be conveyed to the end user.

### How to add Verifier and its workflow details?

1. Verifier details should be added [signup-identity-verifier-details.json](../../signup-service/src/main/resources/signup-identity-verifier-details.json)
2. Create a json file with workflow details, file should be named after the verifier ID as defined in the [signup-identity-verifier-details.json](../../signup-service/src/main/resources/signup-identity-verifier-details.json)

Refer [signup-idv_mock-identity-verifier.json](../../signup-service/src/main/resources/signup-idv_mock-identity-verifier.json) the sample workflow details file. Note the file name is prepended with constant "signup-idv_"

## Out of Scope features of verifier plugin

1. Option to retry on verification failure without having to re-authenticate.
2. Option to retry any step in the verification process.
3. handling timeouts in the verification process in a user-friendly manner.