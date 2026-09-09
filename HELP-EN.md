# Free Code Signer v1.7.1 — User Guide

[← Back to README](README.md) · [Slovenska pomoč](HELP-SL.md) · [Download v1.7.1](https://github.com/varnaPot/FreeCodeSigner/releases/tag/v1.7.1)

## 1. Quick Start

1. Start Free Code Signer.
2. Select the root folder containing files to sign.
3. Select the signing method.
4. Configure or select the certificate/signing provider.
5. Choose a file profile or edit the extension list manually.
6. Configure timestamping if required.
7. Scan the folder.
8. Review detected files and their current signature state.
9. Start signing.
10. Review the result/report.

![Main interface](screenshots/fcs_170_1.png)

## 2. File actions

Version 1.7.1 adds useful right-click actions to the file list.

### Open file location

Right-click a file and choose **Open file location** to open Windows Explorer and select the file.

### Show certificate

For files with an available signing certificate, right-click the file and choose **Show certificate**.

The action is disabled when no signing certificate is available.

For signed JAR files, certificate display is available when JDK/keytool is configured.

## 3. Selected certificate details

A certificate-details button is available next to the selected Windows certificate.

The details window can show:

- Subject
- Issuer
- validity period
- serial number
- SHA-1 thumbprint
- SHA-256 fingerprint
- public-key algorithm and key size
- certificate signature algorithm
- private-key availability
- Enhanced Key Usage (EKU)
- certificate-chain status

The standard Windows certificate dialog can also be opened from the details window.

## 4. Signing method

Choose the signing backend appropriate for your environment.

![Signing method selection](screenshots/fcs_170_6_signing_method.png)

### Microsoft SignTool / Windows Certificate Store

Use this mode for traditional Windows Authenticode signing, including compatible YubiKey/PIV and HSM-backed certificates.

### Azure Artifact Signing

![Azure Artifact Signing](screenshots/fcs_170_8_azure.png)

Use Azure Artifact Signing when the signing identity/private key is protected by Microsoft's cloud signing infrastructure.

### Google Cloud KMS

![Google Cloud KMS](screenshots/fcs_170_9_google.png)

Use Google Cloud KMS when the private signing key is protected in Google Cloud. Jsign is used as the integration layer.

### Jsign

![Jsign configuration](screenshots/fcs_170_10_jsign.png)

![Jsign provider configuration](screenshots/fcs_170_11_jsign.png)

![Jsign options](screenshots/fcs_170_12_jsign_options.png)

Use generic Jsign mode for compatible KMS, HSM, PKCS#11, hardware-token and remote-signing configurations.

## 5. JAR files

Java `.jar` files do not use Windows Authenticode.

Free Code Signer therefore handles them through Java `jarsigner`.

Requirements:

- compatible JDK
- `jarsigner` / `keytool` available
- certificate/key access suitable for the selected signing backend

## 6. File profiles and extensions

![File profiles](screenshots/fcs_170_13_extensions.png)

Available profiles:

- **Standard**
- **Extended**
- **Extended + JAR**
- **Custom**

Manual editing remains available.

## 7. Advanced settings

![Advanced settings](screenshots/fcs_170_7_advanced_settings.png)

Only configure values required by the selected provider. Avoid storing secrets in plain text whenever a safer provider-managed mechanism is available.

## 8. Timestamping

![Timestamp settings](screenshots/fcs_170_14_timestamp.png)

A trusted timestamp proves when a file was signed and is normally recommended for production code signing.

## 9. Signature verification and v1.7.1 recovery logic

Free Code Signer verifies the actual resulting signature after signing.

If SignTool or a hardware provider returns a non-zero result, FCS does **not** automatically mark every file in that batch as failed.

Instead, the affected files are inspected again:

- if the expected signature is valid, the file is treated as successfully signed;
- if the signature is missing/invalid, the file remains failed.

This improves reliability with YubiKey/PIV, smart-card and HSM workflows where a provider can occasionally report an error after a valid signature has already been written.

## 10. Large-batch stability

Version 1.7.1 includes several improvements for large signing jobs:

- CLI output is buffered before being appended to the WinForms interface;
- the visible console has a bounded size;
- verification fallback no longer launches a separate SignTool process for each file;
- unexpected exceptions are captured in crash logs where possible.

## 11. Crash logs

Unexpected application errors are recorded under:

`%LOCALAPPDATA%\FreeCodeSigner\CrashLogs`

If the application closes unexpectedly, include the newest crash-log file when reporting the problem.

## 12. Built-in offline Help

Press **F1** or click **Help**.

![Built-in Help](screenshots/fcs_170_3_help.png)

The in-application help works without an internet connection.

## 13. Languages

Free Code Signer includes 25 interface languages:

Bulgarian, Croatian, Czech, Danish, Dutch, English, Estonian, Finnish, French, German, Greek, Hungarian, Irish, Italian, Latvian, Lithuanian, Maltese, Polish, Portuguese, Romanian, Slovak, Slovenian, Spanish, Swedish and Ukrainian.

![Language selection](screenshots/fcs_170_4_languages.png)

The last selected language is restored automatically.

## 14. Security guidance

Recommended practice:

- keep private keys inside the certificate store, hardware token, HSM or cloud KMS;
- do not place PINs/passwords/client secrets in screenshots or public logs;
- use least privilege for cloud signing resources;
- verify signatures before publishing binaries;
- use timestamping for production releases.

## 15. Troubleshooting

### Certificate is not found
Check the Windows certificate store, hardware-token/HSM middleware and certificate validity.

### SignTool is not found
Install/configure Microsoft SignTool from a compatible Windows SDK.

### Jsign is not found
Check the configured Jsign path and required Java runtime.

### JDK / jarsigner / keytool is not found
Install a compatible JDK and verify that the required tools are available.

### Azure authentication fails
Check authentication, permissions, resource/profile settings and network access.

### Google Cloud KMS authentication fails
Check Google Cloud authentication, project/resource identifiers, key permissions and Jsign configuration.

### Timestamp fails
Verify internet access and timestamp-service availability.

## Download

**[Download Free Code Signer v1.7.1](https://github.com/varnaPot/FreeCodeSigner/releases/tag/v1.7.1)**

---

Free Code Signer is freeware.  
© 2026 RED ZION d.o.o.
