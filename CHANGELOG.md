# Free Code Signer — Changelog

## v1.7.1

### New
- Right-click file actions: **Open file location** and **Show certificate**.
- New certificate-details button next to the selected Windows certificate.
- New certificate-details window with Subject, Issuer, validity, serial number, SHA-1, SHA-256, public-key information, signature algorithm, private-key availability, EKU and certificate-chain status.
- Standard Windows certificate dialog can be opened from the details window.
- Signed Authenticode-file certificate display.
- Signed JAR certificate display when JDK/keytool is available.
- Global crash logging under `%LOCALAPPDATA%\FreeCodeSigner\CrashLogs`.
- New built-in Help content for certificate/file actions and crash logs.

### Fixed / improved
- Non-zero SignTool results no longer automatically mark every file in a batch as failed.
- Affected files are re-verified against the actual resulting Authenticode signature.
- Successfully signed files are recovered even when a YubiKey/PIV, smart-card or HSM provider reports an ambiguous SignTool/SignerSign error after writing the signature.
- Verification fallback no longer launches a separate SignTool process for every file.
- Live CLI output is buffered before updating the WinForms UI.
- The visible console is bounded to avoid excessive UI growth during large jobs.
- Unexpected UI/signing exceptions are written to crash logs where possible.
- Built-in Help and all new v1.7.1 strings are localized in all 25 interface languages.

### Compatibility
All major v1.7.0 functionality remains available:
- Microsoft SignTool / Windows Certificate Store
- Azure Artifact Signing
- Google Cloud KMS
- Jsign universal provider
- HSM / PKCS#11 / YubiKey workflows
- JAR signing via `jarsigner`
- Standard / Extended / Extended + JAR / Custom file profiles
- 25 interface languages

## v1.7.0
Major multi-provider signing update with Azure Artifact Signing, Google Cloud KMS, Jsign, JAR signing, file profiles, built-in Help and 25-language localization.
