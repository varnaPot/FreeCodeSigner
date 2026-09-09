# Free Code Signer

**Free 25-language Windows code-signing GUI for Microsoft SignTool, Azure Artifact Signing, Google Cloud KMS, Jsign, HSM/YubiKey, PKCS#11 and JAR signing.**

Free Code Signer is a Windows desktop application for local, hardware-backed and cloud-based code signing.

It keeps the familiar Microsoft SignTool workflow while adding modern cloud/KMS/HSM options, JAR signing and easier batch signing of multiple file types.

[Download v1.7.0](https://github.com/varnaPot/FreeCodeSigner/releases/tag/v1.7.0) · [English Help](HELP-EN.md) · [Slovenska pomoč](HELP-SL.md) · [varnaPot.si](https://www.varnapot.si/)

> **Freeware:** Free Code Signer may be used and distributed free of charge according to `LICENSE.txt`.  
> The source code is not distributed as part of the public release.

## Free Code Signer v1.7.0

![Free Code Signer v1.7.0](screenshots/fcs_170_1.png)

## Highlights

- Microsoft SignTool / Windows Certificate Store
- Azure Artifact Signing
- Google Cloud KMS
- Jsign integration
- HSM, PKCS#11 and compatible hardware-backed signing
- YubiKey / PIV workflows
- Java JAR signing via `jarsigner`
- Batch signing of multiple supported file types
- Standard, Extended, Extended + JAR and Custom file profiles
- Timestamping and signature verification
- Built-in offline Help with **F1**
- **25 interface languages**
- Last selected language is remembered automatically
- Sensitive credentials do not need to be stored in the normal application configuration

## Signing methods

Free Code Signer v1.7.0 supports several signing methods from the same interface.

![Signing method selection](screenshots/fcs_170_6_signing_method.png)

### Microsoft SignTool

Use certificates available through Windows Certificate Store, including compatible hardware-backed certificates such as YubiKey/PIV.

### Azure Artifact Signing

Use Microsoft Azure Artifact Signing for cloud-based signing where the private signing key remains protected by the Azure signing infrastructure.

![Azure Artifact Signing settings](screenshots/fcs_170_8_azure.png)

### Google Cloud KMS

Use signing keys protected by Google Cloud KMS through the Jsign integration.

![Google Cloud KMS settings](screenshots/fcs_170_9_google.png)

### Jsign

Jsign expands compatibility with compatible cloud KMS providers, HSM devices, PKCS#11 devices, hardware tokens and remote signing services.

![Jsign configuration](screenshots/fcs_170_10_jsign.png)

![Jsign provider settings](screenshots/fcs_170_11_jsign.png)

![Jsign options](screenshots/fcs_170_12_jsign_options.png)

## JAR signing

Java `.jar` files are signed using Java `jarsigner`.

Because JAR signing is not Windows Authenticode signing, Free Code Signer handles JAR files through a separate Java signing workflow.

A compatible JDK is required when JAR signing is used.

## File profiles

Free Code Signer provides predefined file-selection profiles:

- **Standard**
- **Extended**
- **Extended + JAR**
- **Custom**

Manual extension editing remains available.

![File extension profiles](screenshots/fcs_170_13_extensions.png)

## Advanced settings

Provider-specific and advanced signing parameters are available when required.

![Advanced settings](screenshots/fcs_170_7_advanced_settings.png)

## Timestamping

Timestamping can preserve the validity of a signature after the signing certificate itself expires, provided the signature was valid at signing time and the timestamp remains trusted.

![Timestamp settings](screenshots/fcs_170_14_timestamp.png)

## Built-in Help

Version 1.7.0 includes complete offline help directly in the application.

Press **F1** or click **Help**.

![Built-in Help](screenshots/fcs_170_3_help.png)

The help covers:

- Quick Start
- Microsoft SignTool
- Azure Artifact Signing
- Google Cloud KMS
- Jsign
- JAR signing
- file profiles
- timestamping
- signature verification
- troubleshooting
- security

Detailed GitHub documentation:

- [English Help](HELP-EN.md)
- [Slovenska pomoč](HELP-SL.md)

## Languages

Free Code Signer includes **25 interface languages**:

Bulgarian, Croatian, Czech, Danish, Dutch, English, Estonian, Finnish, French, German, Greek, Hungarian, Irish, Italian, Latvian, Lithuanian, Maltese, Polish, Portuguese, Romanian, Slovak, Slovenian, Spanish, Swedish and Ukrainian.

![Language selection](screenshots/fcs_170_4_languages.png)

The selected language is remembered between application sessions.

English interface:

![English interface](screenshots/fcs_170_5_english.png)

## About

![About Free Code Signer](screenshots/fcs_170_2_about.png)

## Security

Free Code Signer is designed so that sensitive signing credentials do not need to be stored in its normal configuration.

Depending on the selected provider, authentication should remain managed by the operating system, certificate store, hardware token, HSM or cloud provider.

Sensitive information such as private keys, PINs, passwords, access tokens and client secrets should not be stored as plain application settings.

## Requirements

Requirements depend on the selected signing method:

| Signing method | Typical requirement |
|---|---|
| Microsoft SignTool | Windows + Microsoft SignTool / Windows SDK |
| Hardware certificate | Compatible certificate/token middleware |
| Azure Artifact Signing | Azure account and configured Artifact Signing resources |
| Google Cloud KMS | Google Cloud authentication/configuration and Jsign |
| Jsign | Compatible Java runtime/Jsign setup and provider configuration |
| JAR | Compatible JDK with `jarsigner` |

The original Windows Certificate Store / Microsoft SignTool workflow remains available.

## Download

**[Download Free Code Signer v1.7.0](https://github.com/varnaPot/FreeCodeSigner/releases/tag/v1.7.0)**

## License

Free Code Signer is **freeware** and may be used and distributed free of charge according to the included license terms.

The public release does **not** include the source code.

See `LICENSE.txt` for details.

---

**Free Code Signer**  
© 2026 RED ZION d.o.o.
