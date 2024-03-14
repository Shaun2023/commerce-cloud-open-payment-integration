## Introduction ##
The Postman Collection enables Cybersource to be used to Take Payments through OPF. 

The integration supports:

* Authorization of Cybersource Payments using the OPF "iFrame" UX Pattern
* Deferred Capture support
* Refunds
* Reversals
* Reauthorization of saved payment

In summary: to import the [Cybersource iFrame Postman Collection](iFrame-CAPTURE_PER_SHIPMENT-OPF_Environment_Configuration.json) this page will guide you through the following steps: 

a) Create Your Cybersource Test Account.

b) Create a Merchant Account Group in OPF Workbench.

c) Set up Your Cybersource Test Account to work with OPF.

d) Prepare the Postman Environment file so the collection can be imported with all your OPF Tenant and Cybersource Test Account unique values. 

## Create a Cybersource Account ##
You can sign up for a free Cybersource Test Account at https://ebctest.cybersource.com/ebc2.


## Creating the Merchant Account Group 
Ceate a new Account Group in the OPF Workbench.

i) In payment integrations.. click **Create**.
![](images/opf-payment-integrations.png)

ii) Add account name (can be anything) and set payment gateway to Cybersource.
![](images/stripe-elements-set-gateway.png)

iii) Click **configure** on Test column of newly created Account.
![](images/opf-account-group-id.png)

**You must set a merchant ID first.**
You can obtain from your account ID found at the following location in the Cybersource dashboard <https://>.

![](images/stripe-elements-get-account.png)

## Preparing the Postman environment_configuration file

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

**3. Account and Account Group**

The ``accountId`` and ``accountGroupId`` values identify the merchant account group can be found in the top left of your merchant configuration.

![](images/opf-account-group-id.png)

**4. merchantId** 

<https://dashboard.stripe.com/test/apikeys>

![](images/stripe-elements-get-secret-key.png)


**5. secretKey**

The secretKey can be obtained here in the Cybersource dashboard. In Test it starts with **pk_test**

<https://dashboard.stripe.com/test/apikeys>

![](images/stripe-elements-get-public-key.png)


**6. accessKey**

**7.profileId**

**8.apiKeyId**


**9.apiKeyValue**


IN OPF Workbench: For your new Cybersource merchant account, navigate to **Notification General** and copy the Notification URL.

![](images/opf-get-notification-url.png)

In Cybersource Dashboard: Navigate to <https://dashboard.stripe.com/test/webhooks> and click **Add an Endpoint**.

i) Paste in your endpoint URL copied from OPF.

![](images/stripe-elements-paste-webook.png)

ii) For simplicity, select “All events”.

![](images/stripe-elements-select-events.png)

iii) Click **Add Endpoint**.

![](images/stripe-elements-add-endpoint.png)

iv) Click **Reveal** the get the webhook secret, it starts with **whsec**.

![](images/stripe-elements-reveal-whsecret.png)

v) In the Environment file set the ``webhookSecret`` value to the key starting with **whsec_**.

**Summary**

The envirionment file is now ready for importing into Postman together with the Mapping Configuration Collection file. Ensure you select the correct environment before running the collection.

In summary, you should have edited the following variables: 

- **token** (https://github.com/opf-postman/commerce-cloud-open-payment-integration/blob/9817001311023efa2a961118788f4e3ee65bbab5/postman/stripe/Hosted%20Fields/Stripe-elements-HOSTED_FIELDS_environment_configuration.json#L6)
- **rootUrl** (https://github.com/opf-postman/commerce-cloud-open-payment-integration/blob/9817001311023efa2a961118788f4e3ee65bbab5/postman/stripe/Hosted%20Fields/Stripe-elements-HOSTED_FIELDS_environment_configuration.json#L11)
- **accountGroupId** (https://github.com/opf-postman/commerce-cloud-open-payment-integration/blob/9817001311023efa2a961118788f4e3ee65bbab5/postman/stripe/Hosted%20Fields/Stripe-elements-HOSTED_FIELDS_environment_configuration.json#L16)
- **accountId** (https://github.com/opf-postman/commerce-cloud-open-payment-integration/blob/9817001311023efa2a961118788f4e3ee65bbab5/postman/stripe/Hosted%20Fields/Stripe-elements-HOSTED_FIELDS_environment_configuration.json#L21)
- **2 x authentication_outbound_basic_auth_username_export\*** (e.g https://github.com/opf-postman/commerce-cloud-open-payment-integration/blob/9817001311023efa2a961118788f4e3ee65bbab5/postman/stripe/Hosted%20Fields/Stripe-elements-HOSTED_FIELDS_environment_configuration.json#L26 https://github.com/opf-postman/commerce-cloud-open-payment-integration/blob/9817001311023efa2a961118788f4e3ee65bbab5/postman/stripe/Hosted%20Fields/Stripe-elements-HOSTED_FIELDS_environment_configuration.json#L38)
- **2 x authentication_outbound_basic_auth_password_export\*** (e.g. https://github.com/opf-postman/commerce-cloud-open-payment-integration/blob/9817001311023efa2a961118788f4e3ee65bbab5/postman/stripe/Hosted%20Fields/Stripe-elements-HOSTED_FIELDS_environment_configuration.json#L32 https://github.com/opf-postman/commerce-cloud-open-payment-integration/blob/9817001311023efa2a961118788f4e3ee65bbab5/postman/stripe/Hosted%20Fields/Stripe-elements-HOSTED_FIELDS_environment_configuration.json#L44)
- **publickey** (https://github.com/opf-postman/commerce-cloud-open-payment-integration/blob/9817001311023efa2a961118788f4e3ee65bbab5/postman/stripe/Hosted%20Fields/Stripe-elements-HOSTED_FIELDS_environment_configuration.json#L86)
- **webhookSecret** (https://github.com/opf-postman/commerce-cloud-open-payment-integration/blob/9817001311023efa2a961118788f4e3ee65bbab5/postman/stripe/Hosted%20Fields/Stripe-elements-HOSTED_FIELDS_environment_configuration.json#L98)