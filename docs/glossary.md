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

-------------------------------------------------------------------------------










# ID registry plugin and eKYC plugin

eSignet extended the platform’s capabilities to include support for:

- Video-based eKYC (Electronic Know Your Customer)  via the eSignet plugin
- ID Registry Plugin: Now any ID Repository system can integrate with esignet


# ID registry plugin

Now esignet's Signup service will integrate with any Id registry system. eSignet now does away with tight integration with MOSIP ID-repository and and gives way to any ID Repository system to be integrated with esignet through 'ID Registry plugin, on the same lines as signup services.

...


<!-- 

Tight integration of signup service with MOSIP ID-repository should be removed. Follow the same eSignet plugin approach to integrate signup service with any ID registry systems.

In signup service version < 1.1.0, Integration was used to create user identity entry and update user identity. Validation of the input user identity data was carried out in signup service before posting the request to MOSIP ID repository. ID repository also validated the identity data in the request using MOSIP defined Identity schema.

Once the data is validated and saved in ID repo, the same was published to MOSIP IDA. Only after the identity data is published to IDA, end user will be able to authenticate via eSignet using the created identity. So it is required for signup service to check the status of the identity in ID registry before confirming registration completion to the end user.

Note: eSignet connects to MOSIP IDA via 'Authenticator' plugin.

-->

...


## Overview
Edits...


## Signup Portal

- User can update profile on Signup portal, verification is done by matching against verification metadata (claims), **User must be authenticated.

- Portal now allows for multiple verifiers, therefore a User can now choose from the list of verifiers.

- Claims in a user profile can be verified by any trusted verifier (Define trusted verifier). **Verified claims and the verification metadata itself could be stored in the ID registry.



** Verification process can be online or offline involving manual steps or consist of both online & manual steps. 


## eKYC Plugin
With eKYC plugin now an external 'eKYC Entity/Partner' can be integrated with eSignet at eKYC Verification Partner/Organization.

This will allow:

- Video based verification
- Add any steps between **start** and **end** step in the verification workflow


### Video based verification:

Signup portal now allows for Video based online verification process. **Considering online verification in-scope for 1.1.0.

Online video based process verification allows for:

1. Liveliness check
2. Face match
3. Document verification
4. Disability check


Point worth noting here is that the verification process can consist of any combination of steps and the process and is agile enough to handle this. This means:

- Signup service is able to **start** the process and **end** the process when signalled by the chosen verifier (Can we call Relying Party or eKYC partner).

- The ending step expects verification details which should be updated in ID registry against the authenticated end user individual ID.
<!-- This point is not clear -->


## Provision to integrate with any Identity verification workflow
Signup service has a provision to add any steps between **start** and **end** step in the verification workflow. We have defined [IdentityVerifierPlugin.java](../../signup-integration-api/src/main/java/io/mosip/signup/api/spi/IdentityVerifierPlugin.java) abstract class.

What is it that Verifier should only take care of?

1. Initializing every workflow run with required configuration based on the provided input. 
2. Verify the input frame based on the current step and publish the feedback or details about the next step to start in this run to kafka (publishAnalysisResult concrete method is already defined in the plugin abstract class).
3. Once the verifier decides to **end** the workflow run, it should hint the signup service by publishing **end** step details using the same publishAnalysisResult concrete method.
4. Signup service will invoke the getVerificationResult method implemented by the verifier to fetch the verification details. VerificationResult can either be failure or successful. The same will be conveyed to the end user.



### How to add Verifier and its workflow details?

1. Verifier details should be added [signup-identity-verifier-details.json](../../signup-service/src/main/resources/signup-identity-verifier-details.json)
2. Create a json file with workflow details, file should be named after the verifier ID as defined in the [signup-identity-verifier-details.json](../../signup-service/src/main/resources/signup-identity-verifier-details.json)

Refer [signup-idv_mock-identity-verifier.json](../../signup-service/src/main/resources/signup-idv_mock-identity-verifier.json) the sample workflow details file. Note the file name is prepended with constant "signup-idv_"




### How is the user authentication context shared with the signup portal?

Authentication of user before verification process can be carried out in eSignet(OP). Authenticated user's transaction is shared as an id_token_hint to the signup portal. 

Signup portal now takes the role of an RP and starts OIDC flow in eSignet with "mosip:idp:acr:id-token" ACR.

As the authroize request already contains id_token_hint, user will not be prompted to enter credentials, **but still may prompt to user to provide consent only if required. 

Most of the time, "sub" claim in the userinfo response should suffice the requirement.









## Out of Scope features of verifier plugin

1. Option to retry on verification failure without having to re-authenticate.
2. Option to retry any step in the verification process.
3. handling timeouts in the verification process in a user-friendly manner.
















# References

Identity Assurance Flow(eKYC verification):

Overview:

eSignet has been enhanced to integrate the OpenID Connect (OIDC) protocol extension for identity assurance and verification metadata, enabling a video-based eKYC verification process during user signin. This enhancement allows relying parties (e.g., banks, insurance companies, and other regulated entities) to authenticate users and verify their identity claims with a high level of confidence, combining video verification with traditional methods like document scanning and biometric checks.

OpenID Connect Assurance Extension:

The OpenID Connect Assurance Extension is an enhancement to the OpenID Connect (OIDC) protocol that adds assurance data to identity claims. While OpenID Connect enables secure authentication, the assurance extension provides additional metadata about the trustworthiness and verification of claims. This assurance data includes:

Verification Status: Whether the claim is self-asserted or verified (e.g., by government-issued IDs, document validation, or biometric checks).

Verification Process Details: Information about how the claim was verified, such as the method used (e.g., in-person document check, video verification, or biometric validation).

Assurance Level: The level of confidence or trust in the claim's accuracy.

This extension is particularly useful in scenarios requiring strong identity verification, such as eKYC (electronic Know Your Customer) processes in regulated industries like banking and finance.

How it enables video EKYC verification?
The OpenID Connect assurance extension enables video eKYC verification by securely transmitting verified identity claims along with assurance metadata, which details the verification process. This allows relying parties (RPs) to remotely and confidently verify a user's identity using live video and facial recognition, ensuring claims such as name, address, and date of birth are trustworthy. The protocol supports regulatory compliance (e.g., KYC/AML) by providing documented verification details, enhancing the confidence in identity claims. It offers flexibility, supporting various verification methods like document checks and biometric scans, and scales based on risk or regulatory requirements. Users also provide consent for sharing verified claims, ensuring transparency in the verification process.

Consent for Data Sharing:
During the eKYC process, consent is requested from the user to share any identity claims/data that is either not present within the system or is unverified. This step ensures that users are aware of and agree to the sharing of their information, with the assurance that their claims will be treated securely.

Relying parties (RPs) can determine which identity claims are essential and which are voluntary, based on the specific requirements of the service or regulatory standards. Essential claims  are mandatory for the verification process, and users are required to consent to these claims if they are not already verified. If essential claims are not consented to, the eKYC process will halt to ensure compliance with identity verification standards.

Voluntary claims may be shared at the user’s discretion, with users being asked to consent only to the claims they are willing to provide. This maintains flexibility for users, allowing them to control the extent of their data shared during the verification process.

To know more about the technical details for identity assurance please refer here.

...

eSignet implements OpenID Connect and OAuth 2.0 flows to work its magic. We have chosen the most secure and trustworthy flows to ensure user privacy and data security.

It relies on SBI (Secure Biometric Interface) to enable an ecosystem of biometric players. To have a look at the supported devices, click here.

eSignet leverages emerging standards for using verifiable credentials with OpenID and for wallet integration.

With eSignet v1.5.0, the support is added for identity assurance <link to text under features> under OpenID Connect for verifying user claims and data 

To learn more about the open standards followed by eSignet, read:

OAuth 2.0

OpenID Connect

IEEE SA P3167 SBI 2.0

Identity Assurance 1.0 

As eSignet incorporates OpenID Connect, a wide range of client libraries are available for seamless integration. Therefore, it is recommended to avoid creating custom code for the integration process.

eSignet implements and supports only the flows mentioned below:

Standards

Flow

Client authentication

OAuth 2.0

Authorization Code with PKCE

private-key-jwt

OIDC

Authorization Code with PKCE

private-key-jwt

Identity Assurance 1.0

Authorization Code with PKCE

private-key-jwt

With the principle of security by design, the support is provided for confidential clients only. The authorization code flow involves exchanging an authorization code for a token. This exchange requires client application authentication. Our supported client authentication method is private-key-jwt only which ensures that the token is given to a legitimate client. We also support the PKCE security extension for exchanging an authorization code for a token, which guarantees that the authorization code was obtained by the same client application performing the exchange.

Note: In eSignet, currently S256 Challenge method is supported in PKCE implementation.

eSignet as OAuth 2.0 server
eSignet OAuth2.0 implementation is not a full-fledged authorization server and supports only the bare minimum required for OIDC flow.

eSignet system does not support roles, as it is designed to be integrated with national level identity solution which can be used by the residents of the country, where roles are not required.




...

The image below is a block diagram of the eSignet comprising various components along with the different layers and external systems.

Open image-20241209-065520.png
image-20241209-065520.png
Relying Party System
The Relying Party Systems depend on identity providers, such as eSignet, to authenticate and verify the identities of users before granting them access to protected resources or services.

Clients utilizing OpenID Connect within the OAuth 2.0 framework are commonly referred to as Relying Parties (RPs).

In the case of VC issuance, they are simply OAuth 2.0 clients. To ensure enhanced security, eSignet exclusively supports confidential clients.

Digital Wallet
Digital Wallets are software-based platforms used to securely store and share the certified credentials of the wallet holder. These credentials are verified claims about the individual, typically certified by the identification system.

The eSignet VCI service offers a feature that allows the issuance of verifiable credentials to any digital wallet that adheres to the OpenID4VCI protocol.

eSignet UI
This is the user interface component of eSignet, developed using React JS. Its main functionality is to handle user authentication and obtain user consent. eSignet UI seamlessly integrates with the UI REST endpoints provided by esignet-service.

One notable feature of the eSignet UI is its support for multiple languages.

eSignet UI also offers QR code-based login with support for multiple digital wallets.

In addition, eSignet UI is compatible with MOSIP SBI 2.0 for biometric capture.

Furthermore, the eSignet UI provides flag-based captcha validation for OTP login.

Lastly, the landing page of the eSignet UI showcases the available ".well-known" endpoints.

<Below red coded section to go with info icon under above section in page>

Here are a few frequently asked questions on the eSignet UI.

How to enable multiple digital wallet support for authentication?

How to configure the expected quality score, timeouts, and number of bio attributes to be captured?

How to enable or disable the captcha? 

eSignet Service
This service is the primary backend Spring Java application that incorporates various layers and integrates with other components mentioned on this page.

Core components: The eSignet core library is used to manage core service interfaces, constants, exceptions, validators, and utility methods.

Service layer: This layer represents the implementation of the interfaces defined in the eSignet core library. Each protocol implementation is a separate service, such as the complete OIDC protocol implementation being part of the oidc-service and VCI protocol implementations residing in the vci-service.

Service modules utilize caching to enhance transaction access and update speeds, as well as to prevent the need for persistent storage of transaction details.

Persistent storage is only used for OIDC client registration details.

Kafka is employed to support asynchronous operations during wallet-based logins.

Rest APIs: The eSignet-service module exposes REST endpoints for the functionality implemented in the service layer modules.

Key Manager

Key Manager is used for secure key management and cryptography functionalities required by the eSignet service component.

It can be integrated with an HSM (hardware security module) for the secure storage of keys.

Typically, Key Manager is run as a service, but it is used as a library in the eSignet Service to minimize the effort of managing extra containers.

It depends on the data layer for maintaining the metadata on keys.

Plugins: Integration points with external systems are designed to be pluggable, allowing easy integration with any ID system. The pluggable integration points are as follows:

Authenticator - for identity verification

AuditPlugin - for auditing all events

KeyBinderPlugin - for key binding of a user and wallet

All plugin interfaces are defined in the esignet-integration-api module.

Sign Up Portal
The Sign Up Portal is a comprehensive module designed to facilitate the user registration process for accessing digital services. It consists of two core components: the Sign Up Service and the Sign Up User Interface (UI).

Sign Up Service: This is the backend component that manages the registration logic. It supports the creation of new user accounts by processing user inputs, performing necessary validations, securely storing user data to ID registry, and integrating with external systems as needed. The service is built with flexibility in mind, allowing it to connect seamlessly to any external ID registry system through a well-defined ID registry plugin <add a link to the ID registry plugin guide under integration guide>. To know more about signup service please refer here.<Link to signup service section>

Sign Up UI: The Sign Up UI is the front-end component that provides a web-based interface through which end users can submit their registration details.To know more about signup UI please refer here. <Link to signup UI section>

Together, the Sign Up Portal streamlines the user registration process, enabling new users to quickly gain access to digital services via eSignet.

Currently, sign up portal supports below features:

Register User

Reset password

Online video based identity verification workflow integration via plugin

To know more about the components and integration of sign up portal with eSignet please refer here.<Link to Sign up Portal Section>

Identification System (ID system)
This system refers to any operational or fundamental identification system that houses the user's demographic and biometric details (if applicable). It could be a database or a system equipped with suitable mechanisms to facilitate identity verification and the sharing of verified user data.  



Overview
The signup portal offers features for creating a user profile and also a way to verify the data used to create it. The dataset in the profile can be used as a credential in eSignet. This enables a country to Fastrack and, at the same time, simplify the digital path of the end user.

The user profile created via the signup portal is stored in an ID registry. The signup portal connects to the ID registry via a runtime plugin, making it completely flexible to use any kind of ID registry. The signup portal comes with an out-of-the-box MOSIP ID repository plugin. 

Note: The Signup portal can also used with any existing ID registries only leveraging the eKYC verification feature.

Sign Up Service
The Sign Up Service in the context of a sign-up portal typically refers to the backend system responsible for handling and processing user registration requests. It integrates with the ID Authentication service and ID repository under MOSIP, that allows the migration of existing accounts or the creation of new user accounts and credentials. 

Sign up 

Generates ID objects based on the user inputs.

Shares ID object with ID repository for account creation.

ID Repository
Maintains the identity object schema.

Validates declared Handle and Password objects.

For more details, visit ID Repository.

ID Authentication Service
Manages user credentials

Validates uniqueness of handle

Validates end-user login requests

Explore ID Authentication

Please refer the sequence diagram below for user account creation and authentication with IDA:

Open image?url=https%3A%2F%2F3349261888-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FylzvZHp30DQ3rNCClELV%252Fuploads%252FF7OAawQqMFBQlQJPbRTq%252Fesing_2.drawio%2520%283%29.png%3Falt%3Dmedia%26token%3D0292ee0d-0b0f-4b1f-9573-03e0064b7d83&width=768&dpr=4&quality=100&sign=e6105907&sv=2

How It Works?
Sign Up service shares the user selected Handle, Password and other details as an Identity object to the ID Repository.

In ID Repository, using ID schema validates Identity object and identifies valid selected Handles.

ID repository shares selected Handles with ID Authentication to create credential for each.

IDA service verifies, if the hash of the Handles is unique before creating corresponding credentials.

Sign Up User Flow
Open image?url=https%3A%2F%2F3349261888-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FylzvZHp30DQ3rNCClELV%252Fuploads%252FTUrlFhizjECGLpwOhALi%252FSign-on-service.png%3Falt%3Dmedia%26token%3Dda19d0c7-fed0-4cc9-a6f8-ba57506fbe43&width=768&dpr=4&quality=100&sign=3ee78fec&sv=2



...



