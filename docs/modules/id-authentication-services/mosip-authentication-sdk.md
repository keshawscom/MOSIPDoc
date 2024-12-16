---
icon: id-card-clip
---

# MOSIP Authentication SDK

### **Overview**

The **MOSIP Authentication SDK** is a Python wrapper that simplifies interaction with the **MOSIP Authentication Service**, enabling seamless integration of robust identity verification workflows into Python applications. Currently, this SDK supports OTP authentication and demographic authentication, but future updates will include support for biometric authentication as well. Developers are relieved from managing intricate details like request/response structures, encryption/decryption mechanisms, and error handling, allowing for quick and efficient implementation.

While **eSignet**, MOSIP's OAuth- and OIDC-based solution, is recommended for most online and scalable authentication needs due to its modern, standards-compliant design, the MOSIP Authentication SDK is critical for scenarios requiring offline capabilities, such as data collection during registration or use cases in regions with limited real-time connectivity. This flexibility makes the SDK an invaluable tool for addressing diverse identity verification requirements across online and offline environments.

### **Why Use This SDK?**

1. **Ease of Integration**: Reduces the learning curve for working with MOSIP’s APIs.
2. **Consistency**: Provides a uniform interface for different authentication operations.
3. **Security**: Handles encryption and decryption of requests and responses in compliance with MOSIP standards.
4. **Flexibility**: Supports multiple authentication methods, including demographic and biometric authentication.

### **Key Features**

1. **Simplified API Interaction**: Abstracts the complexity of direct API calls to MOSIP services.
2. **Support for Multiple Authentication Workflows**: Includes controllers for both KYC-based and general authentication.
3. **Comprehensive Configuration**: Allows customization via a configuration file (authenticator-config.toml).
4. **Secure Handling**: Automatically encrypts requests and decrypts responses to ensure secure communication.
5. **Error Management**: Provides clear error messages and handling mechanisms.

### **Controllers**

The SDK provides two primary controllers, each designed for a specific authentication workflow:

1. kyc-auth-controller\
   Used for **Know Your Customer (KYC)** authentication. This controller facilitates verification using demographic data or OTP verification.\
   **Reference**: [KYC Auth Controller API Documentation](https://mosip.github.io/documentation/1.2.0/authentication-service.html#tag/kyc-auth-controller)
2. auth-controller\
   Used for general authentication of individuals, allowing verification based on a wide range of identifiers such as demo authentication and OTP authentication.\
   **Reference**: [Auth Controller API Documentation](https://mosip.github.io/documentation/1.2.0/authentication-service.html#operation/authenticateIndividual)

### **Method Reference**

The SDK provides two key methods for authentication workflows:

1. kyc **Method**: Used for KYC-based authentication by verifying an individual's demographic data and OTP.
2. auth **Method**: Handles general authentication requests with similar parameters as kyc.

Both methods require the individual's ID (individual\_id), ID type (individual\_id\_type), demographic data (DemographicsModel), and optionally an OTP, biometric data, and consent confirmation. These methods streamline identity verification processes for diverse use cases. please refer below to know more about the methods:

#### kyc Method

Authenticates an individual using KYC-based workflows.

```python
kyc(
    individual_id: str,
    individual_id_type: str,
    demographic_data: DemographicsModel,
    otp_value: Optional[str] = None,
    biometrics: Optional[List[BiometricModel]] = None,
    consent: bool = False
) -> Response
```

#### auth Method

Performs a general authentication request.

```python
auth(
    individual_id: str,
    individual_id_type: str,
    demographic_data: DemographicsModel,
    otp_value: Optional[str] = None,
    biometrics: Optional[List[BiometricModel]] = None,
    consent: bool = False
) -> Response
```

**Common Parameters**

* individual\_id _(str)_: The unique ID of the individual (e.g., VID, UIN).
* individual\_id\_type _(str)_: Specifies the type of ID used (e.g., VID, UIN).
* demographic\_data _(DemographicsModel)_: A model containing demographic details such as name and address.
* otp\_value _(Optional\[str])_: The One-Time Password (OTP) for authentication, if applicable.
* consent _(bool)_: Indicates if the individual has given consent for authentication.

#### **Configuration**

During installation, the SDK must be configured by updating the authenticator-config.toml file. This file contains essential details, including:

* **Service Endpoints**
* **Encryption Keys**
* **Timeout Settings**
* **Logging Settings**

For step-by-step instructions, refer to the **Configuration Guide** (Link to be updated).

### **Installation**

Install the SDK using pip:

```
pip install git+https://github.com/mosip/ida-auth-sdk.git@v0.9.0
```

### **Usage**

Users who wish to try out this SDK should follow these steps:

1. **Initialize the Authenticator**: Set up the authentication instance.
2. **Create Demographic Data**: Prepare the required demographic information.
3. **Perform Authentication**: Execute the authentication request using the SDK.
4. **Handle the Response**: Process and utilize the response received from the authentication service.

Refer to the model implementation below for detailed guidance on performing these steps during the installation process.

**Basic Example:**

```python
from mosip_auth_sdk import MOSIPAuthenticator
from mosip_auth_sdk.models import DemographicsModel, BiometricModel

# Initialize the authenticator
authenticator = MOSIPAuthenticator(config={
    # Configuration settings (refer to authenticator-config.toml for details)
})

# Create demographic data
demographics_data = DemographicsModel(
    name="John Doe",
    address="123 Main Street"
    # Add other fields as required
)

# Perform KYC authentication
response = authenticator.kyc(
    individual_id="123456789",
    individual_id_type="VID",
    demographic_data=demographics_data,
    otp_value="1234",
    consent=True
)

# Handle the response
if response.status_code == 200:
    decrypted_data = authenticator.decrypt_response(response.json())
    print("Authentication successful:", decrypted_data)
else:
    print("Authentication failed:", response.json())
```

#### **Error Handling**

The SDK provides clear error messages and codes to help diagnose issues effectively. Review the errors field in the response for details.

#### **Encryption and Decryption**

All communication with the MOSIP service is securely encrypted. Use the decrypt\_response method to handle responses.

### **License**

TBD

### **Conclusion**

The **MOSIP Authentication SDK** simplifies the integration of robust authentication workflows into Python applications, ensuring secure, efficient, and compliant identity verification. By abstracting the complexities of direct API interaction, the SDK empowers developers to focus on building impactful solutions without worrying about intricate implementation details.
