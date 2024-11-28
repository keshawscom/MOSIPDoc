# Features

## Unified Login

eSignet offers a convenient feature called Unified Login, which allows users to access applications and various services through a single interface thus eliminating the need for multiple logins. Additionally, eSignet enables seamless login to any government service by utilizing a single credential through the existing ID repository.

## Password-less Authentication

eSignet implements a password-less login method that leverages authentication factors supported by our system. This approach enhances security by mitigating the potential risks associated with password-related security vulnerabilities, such as weak passwords, password reuse, and phishing attacks.

## Support for various Authentication Modalities

### OTP Authentication

OTP authentication offers an additional level of security due to the short validity period of the OTP. In the case of logging into eSignet with OTP as the chosen method, our system generates a unique OTP and delivers it to the user via a registered communication channel, such as SMS or email. Upon receiving the OTP, the user can input it into the login interface. The system then compares the entered OTP with the generated one. If they match, the user is granted access to the system.

### Biometric Authentication

eSignet can connect to any biometric device that complies with IEEE P3167 SBI 2.0 standards, perform secure biometric capture, and enable authentication against an underlying ID system that can perform biometric authentication.

### Wallet-based Authentication

Mobile wallet-based authentication can be utilized to scan a QR code and finalize the authentication process using the previously activated credentials for online login. Additionally, facial authentication can happen on the wallet to make sure the presence is verified.

### Password-based Authentication

eSignet also offers password authentication as one of its authentication factors. With eSignet's integration capabilities, existing ID repositories storing user accounts with passwords can now be easily integrated with eSignet. This integration enables OpenID based login, allowing users to access relying party services seamlessly.

[How to enable password-based authentication in eSignet?](../../faq/#how-to-configure-password-authentication-in-esignet)

## Knowledge Based Identification

eSignet has expanded its authentication options to include Knowledge-Based Identification (KBI) as one of its factors. With eSignet's integration capabilities, existing ID repositories storing user-specific details can now be easily integrated with eSignet thereby enabling service providers to authenticate users.

#### KBI form configuration for eSignet UI

Knowledge based Identification has been developed in such a way that the form filled by the user on the UI can be configured. Please refer to the link [here](https://docs.esignet.io/end-user-guide/knowledge-based-authentication) for more information about KBI with a use case of Insurance VC Issuance.

Please refer to the [FAQ](../../faq/#how-to-configure-kbi-form-in-esignet-ui) section for more details on how to configure the KBI form in eSignet UI.

#### Authenticator plugin implementation for KBI with Sunbird RC

Authenticator plugin: This Authenticator plugin allows the user to identify the user with the details provided in the KBI form in the eSignet UI and Identifies the user based on the details from the registry called Sunbird RC.

For more technical details about Sunbird  RC find the below information and refer to the link provided below:

#### **Sunbird RC version:** v2.0.0-rc3

The authenticator plugin for the Sunbird registry only supports the “Knowledge Based Identification” (KBI) of the end user. The fields part of the KBI is completely dependent on the registry schema. Fields configured to be part of the KBI form should identify the end user. Denies the identification if more than one entry is found in the registry. Support is added for text and date fields. For more details on 'eSignet and Sunbird RC Integration Implementation' please refer [here](https://github.com/mosip/digital-credential-plugins/blob/master/sunbird-rc-esignet-integration-impl/README.md).&#x20;

#### Verifiable Credentials&#x20;

Verifiable credentials (VCs) are digital representations of physical credentials like passports or licenses. They are digitally signed, making them tamper-resistant and instantly verifiable. Issued by trusted entities, VCs are stored in digital wallet apps and used by individuals to access various services.

{% hint style="info" %}
📝**Note:** VCI is supported up to [eSignet v1.4.2](https://docs.esignet.io/versions/v1.4.2) but will no longer be supported in future versions.
{% endhint %}

Verifiable Credentials Issuance (VCI) is now supported by[ Inji Certify](https://docs.mosip.io/inji/inji-certify/overview), to know more about VCI please refer [here](https://docs.mosip.io/inji/inji-certify/overview#verifiable-credentials-issuance-through-inji-certify).

## Consent

User consent refers to the voluntary and informed agreement provided by an individual, often referred to as a user, to a specific action, process, or request. Users should have a clear understanding of what they are consenting to. User consent is particularly important in the context of data privacy, where it is required in many jurisdictions for organizations to obtain explicit consent from individuals before collecting, processing, or sharing their data.

Consent mechanisms are often used in the form of checkboxes, pop-up notifications, or consent forms on applications to ensure that the users understand and agree to data processing practices.\
\
eSignet stores the consent in a built-in **consent registry** which is specifically designed to store user consent on claims and scopes that are requested during the first login into a relying party's application using eSignet.

## Language Support for eSignet

The eSignet user interface (UI) offers comprehensive language support to facilitate effective communication. By default, eSignet includes language bundles for Arabic, English, Hindi, Kannada, and Tamil. Moreover, it can be easily customized to incorporate additional languages as necessary to accommodate specific country requirements.

Furthermore, eSignet has undergone meticulous testing to ensure seamless compatibility with right-to-left (RTL) languages. This means that users can rely on eSignet to confidently navigate and interact with RTL content.

{% hint style="info" %}
📝 **Note:** \
1\. To add more language bundles in eSignet, you can go through the below article.

[How to add a new language to eSignet?](https://docs.esignet.io/faq#how-to-add-a-new-language-in-esignet)

2. To remove a language from eSignet, you can go through the below article.

[How to remove a language from the eSignet default setup?](../../faq/#how-to-remove-a-language-from-the-esignet-default-setup)
{% endhint %}

