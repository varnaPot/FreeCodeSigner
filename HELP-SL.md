# Free Code Signer v1.7.1 — Navodila za uporabo

[← Nazaj na README](README.md) · [English Help](HELP-EN.md) · [Prenos v1.7.1](https://github.com/varnaPot/FreeCodeSigner/releases/tag/v1.7.1)

## 1. Hiter začetek

1. Zaženi Free Code Signer.
2. Izberi korensko mapo z datotekami.
3. Izberi način podpisovanja.
4. Nastavi oziroma izberi certifikat ali ponudnika.
5. Izberi profil datotek ali ročno uredi končnice.
6. Po potrebi nastavi časovni žig.
7. Skeniraj mapo.
8. Preglej najdene datoteke in stanje podpisov.
9. Začni podpisovanje.
10. Preglej rezultat in poročilo.

![Glavno okno](screenshots/fcs_170_1.png)

## 2. Dejanja nad datotekami

Različica 1.7.1 dodaja uporabne možnosti ob desnem kliku na datoteko.

### Odpri pot datoteke

Z desnim klikom izberi **Odpri pot datoteke**. Windows Explorer odpre mapo in označi izbrano datoteko.

### Prikaži potrdilo

Če ima datoteka podpisni certifikat, je na voljo možnost **Prikaži potrdilo**.

Če podpisnega certifikata ni, je možnost onemogočena.

Pri podpisanih JAR datotekah je prikaz certifikata na voljo, kadar sta nastavljena JDK in `keytool`.

## 3. Podrobnosti izbranega certifikata

Ob izbranem Windows certifikatu je nov gumb za prikaz podrobnosti.

Okno lahko prikaže:

- komu je certifikat izdan,
- izdajatelja,
- obdobje veljavnosti,
- serijsko številko,
- SHA-1 thumbprint,
- SHA-256 fingerprint,
- algoritem in velikost javnega ključa,
- algoritem podpisa certifikata,
- informacijo o zasebnem ključu,
- Enhanced Key Usage (EKU),
- stanje verige certifikatov.

Iz okna je mogoče odpreti tudi standardni Windows prikaz certifikata.

## 4. Način podpisovanja

![Izbira načina podpisovanja](screenshots/fcs_170_6_signing_method.png)

### Microsoft SignTool / Windows Certificate Store

Za klasično Windows Authenticode podpisovanje, vključno z združljivimi YubiKey/PIV in HSM certifikati.

### Azure Artifact Signing

![Azure Artifact Signing](screenshots/fcs_170_8_azure.png)

Za podpisovanje z Microsoftovo cloud podpisno infrastrukturo.

### Google Cloud KMS

![Google Cloud KMS](screenshots/fcs_170_9_google.png)

Za ključe, zaščitene v Google Cloud KMS. Jsign deluje kot povezovalni sloj.

### Jsign

![Nastavitve Jsign](screenshots/fcs_170_10_jsign.png)

![Ponudnik Jsign](screenshots/fcs_170_11_jsign.png)

![Možnosti Jsign](screenshots/fcs_170_12_jsign_options.png)

Za združljive KMS, HSM, PKCS#11, hardware-token in remote-signing scenarije.

## 5. JAR datoteke

Java `.jar` datoteke ne uporabljajo Windows Authenticode.

Free Code Signer jih podpisuje prek Java `jarsigner`.

Potrebno je:

- združljiv JDK,
- dostopen `jarsigner` in `keytool`,
- ustrezen dostop do certifikata oziroma ključa.

## 6. Profili datotek

![Profili datotek](screenshots/fcs_170_13_extensions.png)

Na voljo so:

- **Standardno**
- **Razširjeno**
- **Razširjeno + JAR**
- **Po meri**

Ročno urejanje končnic ostane na voljo.

## 7. Napredne nastavitve

![Napredne nastavitve](screenshots/fcs_170_7_advanced_settings.png)

Vnesi samo podatke, ki jih zahteva izbrani ponudnik. Gesel, PIN-ov in drugih skrivnosti ne shranjuj v navadnem besedilu, kadar je na voljo varnejši način avtentikacije.

## 8. Časovni žig

![Nastavitve časovnega žiga](screenshots/fcs_170_14_timestamp.png)

Za produkcijske podpise je časovni žig praviloma priporočljiv.

## 9. Preverjanje podpisa in nova logika v1.7.1

Free Code Signer po podpisovanju preveri **dejanski nastali podpis**.

Če SignTool ali hardware provider vrne non-zero rezultat, FCS ne označi več avtomatsko celotnega batcha kot neuspešnega.

Namesto tega ponovno preveri prizadete datoteke:

- če je pričakovani podpis veljaven, je datoteka obravnavana kot uspešno podpisana;
- če podpis manjka oziroma ni veljaven, ostane rezultat napaka.

To je posebej uporabno pri YubiKey/PIV, smart-card in HSM okoljih, kjer lahko provider v določenih primerih vrne napako tudi po tem, ko je bil veljaven podpis že zapisan.

## 10. Stabilnost pri velikem številu datotek

V1.7.1 vključuje več izboljšav:

- CLI izpis se bufferira pred prikazom v WinForms UI;
- velikost vidnega konzolnega izpisa je omejena;
- fallback preverjanje ne zaganja več ločenega SignTool procesa za vsako datoteko;
- nepričakovane izjeme se, kjer je mogoče, zapišejo v crash log.

## 11. Crash logi

Nepričakovane napake programa se zapisujejo v:

`%LOCALAPPDATA%\FreeCodeSigner\CrashLogs`

Če se program nepričakovano zapre, je za diagnostiko pomembna najnovejša datoteka iz te mape.

## 12. Vgrajena offline pomoč

Pritisni **F1** ali klikni **Pomoč**.

![Vgrajena pomoč](screenshots/fcs_170_3_help.png)

Pomoč deluje tudi brez internetne povezave.

## 13. Jeziki

Free Code Signer vključuje 25 jezikov:

bolgarščina, hrvaščina, češčina, danščina, nizozemščina, angleščina, estonščina, finščina, francoščina, nemščina, grščina, madžarščina, irščina, italijanščina, latvijščina, litovščina, malteščina, poljščina, portugalščina, romunščina, slovaščina, slovenščina, španščina, švedščina in ukrajinščina.

![Izbira jezika](screenshots/fcs_170_4_languages.png)

Zadnji izbrani jezik se samodejno obnovi ob naslednjem zagonu.

## 14. Varnost

Priporočamo:

- zasebne ključe hrani v Certificate Store, hardware tokenu, HSM ali cloud KMS;
- PIN-ov, gesel in client secretov ne objavljaj v screenshotih ali logih;
- za cloud vire uporabljaj načelo najmanjših potrebnih pravic;
- pred objavo preveri digitalni podpis;
- pri produkcijskih izdajah uporabljaj timestamp.

## 15. Pogoste težave

### Certifikata ni mogoče najti
Preveri Windows Certificate Store, middleware hardware tokena/HSM in veljavnost certifikata.

### SignTool ni najden
Namesti oziroma nastavi Microsoft SignTool iz združljivega Windows SDK.

### Jsign ni najden
Preveri pot do Jsign in Java okolje.

### JDK / jarsigner / keytool ni najden
Namesti združljiv JDK.

### Azure prijava ne uspe
Preveri avtentikacijo, pravice, resource/profile in omrežno povezavo.

### Google Cloud KMS prijava ne uspe
Preveri Google Cloud prijavo, identifikatorje virov, pravice do ključa in Jsign nastavitve.

### Timestamp ne uspe
Preveri internetno povezavo in dostopnost timestamp strežnika.

## Prenos

**[Prenesi Free Code Signer v1.7.1](https://github.com/varnaPot/FreeCodeSigner/releases/tag/v1.7.1)**

---

Free Code Signer je freeware.  
© 2026 RED ZION d.o.o.
