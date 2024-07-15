## Introduction

The Postman Collection enables a [Afterpay / Clearpay Redirect Payment Page](https://developers.clearpay.co.uk/clearpay-online/reference/standard-checkout#redirect-method) to be used to Setup a loan agreement using a [Deferred Payment Flow](https://developers.clearpay.co.uk/clearpay-online/reference/deferred-payment-flow). 

The integration supports:

* Authorization of loan by redirecting to Clearpay/Afterpay payment pages
* Deferred Capture
* Refunds
* Voids


## Planned Backlog Items
* Clearpay messaging
* Support for checkout widget

## Known Issues
* Refunds are automated but currently require manual confirmation in OPF Workbench
* The integration has not undergone [Certification testing as per](https://developers.clearpay.co.uk/clearpay-online/docs/testing-your-clearpay-integration)

## Setup Instructions

### Overview
To import the [Afterpay Postman Collection](mapping_configuration.json) this page will take you through the following steps

a) Sign up for a Afterpay/Clearpay Account

b) Get your afterpay/clearpay credentials.

c) Create a Merchant Integration in OPF Workbench.

d) Prepare the [Postman Environment](environment_configuration.json) file so the collection can be imported with all your OPF Tenant and Afterpay/Clearpay unique values. 


### Create a Afterpay Account
Decide if you need an Afterpay (ROW) or Clearpay account (UK), the solution is branded differently in the UK.

You can sign up for a Afterpay Account at https://get.afterpay.com/app/.
You can sign up for a Clearpay Account at https://get.clearpay.co.uk/app/.

Signup is for the official account, so its expected the merchant will need to do this rather than a developer.

You can test the integration with [test payment details](https://developers.clearpay.co.uk/clearpay-online/docs/sandbox-testing#test-payment-details).


### Get the Sandbox Credentials
Sandbox credentials are only available after your retailer/merchant has registered and can be obtained from your Clearpay account manager as per: https://developers.clearpay.co.uk/clearpay-online/docs/sandbox-testing


### Creating the Merchant Account Group
Create a new Integration in the OPF Workbench and set the Merchant ID.

You can ude the Merchant ID supplied by your account manager. 


### Preparing the Postman environment_configuration file

**1. Token**

Get your access token using the auth endpoint https://{{authendpoint}}/oauth2/token and client ID and secret obtained from BTP Cockpit.

Copy the value of the access_token field (it’s a JWT) and set as the ``token`` value in the environment file.

IMPORTANT: Ensure the value is prefixed with **Bearer**. e.g. ``Bearer {{token}}``.

**2. Root url**

The ``rootUrl`` is the **BASE URL** of your OPF tenant.

E.g. if your workbench/OPF cockpit url was this …

<https://opf-iss-d0.uis.commerce.stage.context.cloud.sap/opf-workbench>.

The base Url would be

https://opf-iss-d0.uis.commerce.stage.context.cloud.sap.


**3. Integration and Configuration**

The ``accountId`` and ``accountGroupId`` values identify the merchant account group can be found in the top left of your merchant configuration.

**4. API Credentials**

The ``authentication_outbound_basic_auth_username_export_93`` is the merchant id.
The ``authentication_outbound_basic_auth_password_export_93`` is the sandbox secret key supplied by your account manager

### Allowlist
Add the following domains to the domain allowlist in OPF workbench

``global-api-sandbox.afterpay.com`` 
``global-api.afterpay.com``

### Summary

The envirionment file is now ready for importing into Postman together with the Mapping Configuration Collection file. Ensure you select the correct environment before running the collection.

In summary, you should have edited the following variables: 

#### Common
- ``token``
- ``rootUrl``
- ``accountGroupId``
- ``accountId``

#### Afterpay/Clearpay Specific
- ``authentication_outbound_basic_auth_username_export_93``
- ``authentication_outbound_basic_auth_password_export_93``

For sandbox testing, all other values can be left as defaults.  