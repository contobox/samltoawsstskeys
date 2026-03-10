# SAML to AWS STS Keys Conversion
Browser Extension, which converts a SAML 2.0 assertion to AWS STS Keys (temporary credentials). Just log in to the AWS Web Management Console using your SAML IDP and the extension will fetch the SAML Assertion from the HTTP request. The SAML Assertion is then used to call the assumeRoleWithSAML API to create the temporary credentials. (AccessKeyId, SecretAccessKey and SessionToken).

> **Note:** This extension currently uses Manifest V2 and is not supported in Chrome 127+. Use a Chromium-based browser that still supports MV2 (e.g., Brave, Edge) or Mozilla Firefox. Alternatively, in Chrome you can re-enable MV2 support via `chrome://flags` by setting "Extensions Manifest V2 Deprecation" to Enabled.

The Chrome Extension can be downloaded here:
[Google Chrome Web Store](https://chrome.google.com/webstore/detail/ekniobabpcnfjgfbphhcolcinmnbehde/)

> The source of this extension is also used as [extension](https://addons.mozilla.org/en-US/firefox/addon/saml-to-aws-sts-keys/) for Mozilla FireFox. For specific FireFox related questions you can get in touch with my awesome friend @gbvanrenswoude.

# Table of Contents
* [Why this Chrome Extension?](#why)
* [Getting Started](#gettingstarted)
* [Frequently Asked Question](#faq)
* [Link to the default configs on Mac](#macln)
* [Todo](#todo)

## <a name="why"></a>Why this Chrome Extension?
If you don't have any user administration setup within AWS Identity & Access Management (IAM) but instead rely on your corporate user directory, i.e. Microsoft Active Directory. Your company uses a SAML 2.0 Identity Provider (IDP) to log in to the AWS Web Management Console (Single Sign On). Then this Chrome Extension is for you!

You run into trouble as soon as you would like to execute some fancy scripts from your computer which calls the AWS API's. When sending a request to the AWS API's you need credentials, meaning an AccessKey and SecretKey. You can easily generate these keys for each user in AWS IAM. However, since you don't have any users in AWS IAM and don't want to create users just for the sake of having an AccessKey and SecretKey you are screwed. But there is a way to get temporary credentials specifically for your corporate identity.

The Security Token Service (STS) from AWS provides an API action assumeRoleWithSAML. Using the SAML Assertion given by your IDP the Chrome Extension will call this API action to fetch temporary credentials. (AccessKeyId, SecretAccessKey and SessionToken). This way there is no need to create anonymous user in AWS IAM for executing scripts. This would be a real security nightmare, since it won't be possible to audit who did what. This Chrome Extension however will make it super easy for you to just use your corporate identity for executing scripts calling AWS API's.

## <a name="gettingstarted"></a>Getting Started from local
1. Clone this repository
2. Open a Chromium-based browser that supports Manifest V2 (e.g., Brave, Edge) and go to the extensions page (e.g., `brave://extensions/` or `edge://extensions/`)
3. Enable Developer Mode
4. Click on "Load unpacked extension..."
5. Select the folder where you cloned this repository
6. Enjoy!

## <a name="macln"></a>Link to the default configs on Mac 
```
rm ~/.aws/credentials
ln -s ~/Downloads/credentials ~/.aws/credentials
```

## <a name="faq"></a>FAQ: Frequently Asked Question
1. How long are the credentials valid?  
By default, the credentials are valid for 12 hours. This can be changed in the AWS IAM console or Extension settings. Note: the requested duration cannot exceed the MaxSessionDuration set on the IAM role.

## <a name="todo"></a>TODO
1. Migrate from [Manifest v2 to v3](https://blog.chromium.org/2020/12/manifest-v3-now-available-on-m88-beta.html)
