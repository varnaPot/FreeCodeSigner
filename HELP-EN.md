# Free Code Signer v1.7.0 — User Guide

[← Back to README](README.md) · [Slovenska pomoč](HELP-SL.md) · [Download v1.7.0](https://github.com/varnaPot/FreeCodeSigner/releases/tag/v1.7.0)

## 1. Quick Start

1. Start Free Code Signer.
2. Select the root folder containing files to sign.
3. Select the signing method.
4. Configure or select the certificate/signing provider.
5. Choose a file profile or edit the extension list manually.
6. Configure timestamping if required.
7. Scan the folder.
8. Review the detected files and their current signature state.
9. Start signing.
10. Review the result/report.

![Main interface](screenshots/fcs_170_1.png)

## 2. Signing method

Choose the signing backend appropriate for your environment.

![Signing method selection](screenshots/fcs_170_6_signing_method.png)

### Microsoft SignTool / Windows Certificate Store

Use this mode for traditional Windows Authenticode signing.

Typical use cases:

- locally installed code-signing certificate
- certificate stored in Windows Certificate Store
- YubiKey/PIV-backed certificate
- compatible HSM exposed through Windows cryptographic providers

### Azure Artifact Signing

Use Azure Artifact Signing when the signing identity and private key are protected by Microsoft's cloud signing infrastructure.

![Azure Artifact Signing](screenshots/fcs_170_8_azure.png)

Typical configuration includes the Azure signing resource/profile and the authentication method required by your environment.

### Google Cloud KMS

Use Google Cloud KMS when the private signing key is stored and protected in Google Cloud.

![Google Cloud KMS](screenshots/fcs_170_9_google.png)

Jsign is used as the integration layer for the signing workflow.

### Jsign

Use the generic Jsign mode for compatible KMS, HSM, PKCS#11, hardware-token and remote-signing configurations.

![Jsign configuration](screenshots/fcs_170_10_jsign.png)

![Jsign provider configuration](screenshots/fcs_170_11_jsign.png)

Additional provider options:

![Jsign options](screenshots/fcs_170_12_jsign_options.png)

## 3. JAR files

Java `.jar` files do not use Windows Authenticode.

Free Code Signer therefore handles them through Java `jarsigner`.

Requirements:

- compatible JDK
- `jarsigner` available/configured
- certificate/key access suitable for the selected signing backend

When using the **Extended + JAR** profile, JAR files can be included together with other supported file types in the same workflow while still being signed through the appropriate Java mechanism.

## 4. File profiles and extensions

You can use predefined profiles or maintain the extension list manually.

![File profiles](screenshots/fcs_170_13_extensions.png)

### Standard

For the most common Windows code-signing file types.

### Extended

For a broader set of compatible formats.

### Extended + JAR

Adds Java JAR handling to the extended selection.

### Custom

Use this when you want full manual control over the extension list.

Manual editing remains available even when predefined profiles are provided.

## 5. Advanced settings

Some providers require extra parameters.

![Advanced settings](screenshots/fcs_170_7_advanced_settings.png)

Only configure values required by your selected provider. Avoid storing secrets in plain text whenever the provider offers a safer authentication mechanism.

## 6. Timestamping

A trusted timestamp proves when a file was signed.

![Timestamp settings](screenshots/fcs_170_14_timestamp.png)

Why it matters:

- the signature can remain valid after the signing certificate expires
- verification can establish that the certificate was valid at the time of signing
- a timestamp should normally be used for production code signing

Timestamp availability and supported algorithms depend on the signing backend and timestamp service.

## 7. Signature verification

Free Code Signer can inspect signatures before and after signing.

Check the result carefully, especially when:

- changing certificate/provider
- enabling a new cloud backend
- signing a new file type
- deploying a new timestamp service
- signing JAR files for the first time

## 8. Built-in offline Help

Press **F1** or click **Help**.

![Built-in Help](screenshots/fcs_170_3_help.png)

The in-application help is available without an internet connection.

## 9. Language

Free Code Signer includes 25 interface languages.

![Language selection](screenshots/fcs_170_4_languages.png)

The last selected language is saved and restored automatically.

English interface example:

![English interface](screenshots/fcs_170_5_english.png)

Supported languages:

Bulgarian, Croatian, Czech, Danish, Dutch, English, Estonian, Finnish, French, German, Greek, Hungarian, Irish, Italian, Latvian, Lithuanian, Maltese, Polish, Portuguese, Romanian, Slovak, Slovenian, Spanish, Swedish and Ukrainian.

## 10. Security guidance

Recommended practice:

- keep private keys inside the certificate store, hardware token, HSM or cloud KMS
- do not place PINs/passwords/client secrets in screenshots or public logs
- prefer short-lived/provider-managed authentication where available
- protect access to cloud signing resources using least privilege
- verify signatures before publishing the signed binaries
- use timestamping for production releases

Free Code Signer is designed so that sensitive signing credentials do not need to be stored in the normal application settings.

## 11. Troubleshooting

### Certificate is not found

- verify that the certificate is installed/available to the current user
- check hardware token/HSM middleware
- confirm that the certificate is valid for code signing
- reconnect/unlock the device if required

### SignTool is not found

Install/configure Microsoft SignTool from a compatible Windows SDK or point Free Code Signer to the appropriate executable.

### Jsign is not found

Check the configured Jsign path and required Java runtime.

### JDK / jarsigner is not found

Install a compatible JDK and verify that `jarsigner` is available.

### Azure authentication fails

Check Azure authentication, permissions, resource/profile settings and network access.

### Google Cloud KMS authentication fails

Check Google Cloud authentication, project/resource identifiers, key permissions and Jsign configuration.

### Timestamp fails

Try the operation again, verify internet access and ensure that the timestamp service is reachable and compatible with the selected signing mode.

## 12. About

![About dialog](screenshots/fcs_170_2_about.png)

## Download

**[Download Free Code Signer v1.7.0](https://github.com/varnaPot/FreeCodeSigner/releases/tag/v1.7.0)**

---

Free Code Signer is freeware.  
© 2026 RED ZION d.o.o.
