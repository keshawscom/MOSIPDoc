# Partner Management

MOSIP's partner management is used to create and manage OIDC clients. Hence, three new APIs have been introduced in partner management,

* API to create an OIDC client
* API to update an OIDC client
* API to retrieve and OIDC client

<details>

<summary>How can we create a OIDC client using partner management?</summary>

In order to create a OIDC client,

* The relying party, needs to get onboarded into MOSIP using the partner management portal as a authentication partner
* The relying party needs to be mapped to a policy in MOSIP
* When the relying party is mapped to the policy, using the new [OIDC client create API](partner-management.md#oidc-client), a client can be created for the relying party.

**Notes:**

* A relying party can have multiple clients created against a approved mapped policy.
* When a eSignet client is created using partner management APIs, then the client ID is set as the SHA256 hash of the public key provided in the request.

</details>

There are also a few modifications in the policies in partner management for a partner opting for OIDC based authentication using eSignet.

Additional Authentication Types have been added for KYC authentication (_**kycauth**_), KYC Exchange (_**kycexchange**_) and Wallet Local Authentication (_**wla**_).

Below is a sample policy for a relying party who is interested in authentication using eSignet.

```json
{
  "authTokenType":"policy",
  "allowedKycAttributes":[
    {
      "attributeName":"fullName"
    },
    {
      "attributeName":"gender"
    },
    {
      "attributeName":"phone"
    },
    {
      "attributeName":"email"
    },
    {
      "attributeName":"dateOfBirth"
    },
    {
      "attributeName":"city"
    },
    {
      "attributeName":"face"
    },
    {
      "attributeName":"addressLine1"
    }
  ],
  "allowedAuthTypes":[
    {
      "authSubType":"IRIS",
      "authType":"bio",
      "mandatory":false
    },
    {
      "authSubType":"FINGER",
      "authType":"bio",
      "mandatory":false
    },
    {
      "authSubType":"",
      "authType":"otp",
      "mandatory":false
    },
    {
      "authSubType":"FACE",
      "authType":"bio",
      "mandatory":false
    },
    {
      "authSubType":"",
      "authType":"otp-request",
      "mandatory":false
    },
    {
      "authSubType":"",
      "authType":"kycauth",
      "mandatory":false
    },
    {
      "authSubType":"",
      "authType":"kycexchange",
      "mandatory":false
    },
    {
      "authSubType":"",
      "authType":"wla",
      "mandatory":false
    }
  ]
}
```

## Appendix - Create, Retrieve and Update OIDC Client APIs

{% openapi src="../../../.gitbook/assets/partner-management-service-openapi (1).json" path="/oidc/client" method="post" %}
[partner-management-service-openapi (1).json](<../../../.gitbook/assets/partner-management-service-openapi (1).json>)
{% endopenapi %}

{% openapi src="../../../.gitbook/assets/partner-management-service-openapi (1).json" path="/oidc/client/{client_id}" method="put" %}
[partner-management-service-openapi (1).json](<../../../.gitbook/assets/partner-management-service-openapi (1).json>)
{% endopenapi %}

{% openapi src="../../../.gitbook/assets/partner-management-service-openapi (1).json" path="/oidc/client/{client_id}" method="get" %}
[partner-management-service-openapi (1).json](<../../../.gitbook/assets/partner-management-service-openapi (1).json>)
{% endopenapi %}
