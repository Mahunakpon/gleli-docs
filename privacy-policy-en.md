---
title: "Privacy Policy — Gléli"
lang: en
---

# Privacy Policy — Gléli

**Last updated: August 5, 2026**

---

## 1. Introduction

This privacy policy describes how the **Gléli** mobile application, dedicated to agricultural management (pineapple/market gardening) in Benin, collects, uses, stores, and shares your personal data.

**Data controller:** Biogaz Bénin Sarl, Maison GNANGA, en face de la Mosquée, Rue 115, Cotonou, Bénin, RB/COT/19B2460 — hereinafter "Gléli", "we".

**Scope:** this policy covers the Gléli mobile application (Android/iOS), its associated backend server, and all third-party services used to operate the application (listed in detail in section 7). It applies to every user who creates a Gléli account, regardless of their role (farm owner, manager, technician, sales staff, invited member).

Gléli is an **offline-first** application: most of your data is stored locally on your device, then synchronized with our server whenever you have an internet connection, in order to enable collaboration between members of the same farm and to back up your data in case your device is lost.

---

## 2. Data we collect

Below, category by category, we describe what data is collected, for what purpose, where it is stored, and with whom it is shared.

### 2.1 Identity and contact information

**What:** name, phone number, email address, country, date of birth (optional), job title (optional), password, unlock PIN code.

**Purpose:** creating and managing your account, authentication, communicating with you (support, notifications).

**Storage:** locally on your device (database protected by the operating system) and on our server (PostgreSQL database), except for the PIN code, which stays **strictly local to your device** and is never transmitted to our server.

**Password and PIN protection:** your password is protected server-side by an industry-standard cryptographic hashing function (bcrypt); it is never stored or transmitted in plain text. Your PIN code is likewise hashed before local storage and never leaves your device.

**Sharing:**
- Other members of your farm (colleagues with a management role) can see your name, phone, and email in the member-management tool — this is not sharing with an external third party, but a functional sharing within your own team.
- **EmailJS** (third-party email delivery service) receives your name, phone, and email when: you contact support, you send (with your explicit confirmation) a technical bug report, or you receive a verification code by email during sign-up. See section 7.

### 2.2 Biometrics (fingerprint / face recognition)

**What:** use of your fingerprint or facial recognition to unlock the application, if your device supports it and you choose to enable it.

**Purpose:** convenient login, as an alternative to the PIN code.

**Storage and sharing:** **no biometric data is ever collected, stored, or transmitted by Gléli.** Biometric authentication is handled entirely by your device's operating system (via Android/iOS secure APIs — Secure Enclave or Keystore); Gléli only receives a "success" or "failure" result from this check, never the fingerprint or facial image itself. This data therefore never reaches our servers or any third-party service.

### 2.3 Location (GPS)

**What:** one-time GPS coordinates (latitude/longitude), captured at "balanced" accuracy (roughly hundred-meter range, not navigation-grade precision).

**Purpose:** to geolocate your farm plots, timestamp and geolocate your farming operations (planting, treatment, harvest, etc.), verify the location at the time of a technician-visit signature, and record the departure point of a goods transport — useful for agricultural traceability and compliance checks (e.g. detecting an operation logged outside the relevant plot's area).

**When:** location is only requested at the precise moment of these actions (creating/editing a plot, logging an operation, signing a visit, starting a transport) — **never in the background, never as continuous tracking.** The app only requests foreground location permission, never background permission.

**Storage:** locally, then synchronized to our server (PostgreSQL) so other members of your farm have the same information, and for data backup purposes.

**Sharing:** no sharing with any external third party. The Map screen can display your current live position (a "center on me" button) on-screen only, without ever recording or transmitting it.

### 2.4 Photos

**What:** photos of plants (disease diagnosis), photos of documents (regulatory files, invoices, etc.), and possibly photos attached to sales or technical visits.

**Purposes and sharing:**
- **AI-based plant disease diagnosis**: when you photograph a plant for diagnosis, the photo is sent to our server and then to **Anthropic** (provider of the Claude AI model) for analysis. Anthropic only receives the image submitted for that analysis — see section 7 for details. The photo, along with the diagnosis result, is then retained (see section 4) so you can review your diagnosis history.
- **Regulatory record documents** (photos or PDFs of certificates, invoices, etc.): stored so you can retrieve and share them for inspections or traceability exports.
- All these photos are stored on your device and uploaded to **Cloudflare R2** (file storage service, see section 7) so they remain accessible from your other devices and are backed up.
- **Traceability labels** (printable QR code for your harvest lots): generated locally on your device, without being sent to our server. The QR code image itself is generated by a public third-party service (api.qrserver.com) from the lot code — this is not personal data (it is an agricultural lot identifier), but it does technically pass through this third-party service when displayed or printed.

Plant disease diagnosis concerns **plant health**, not your own personal health — it is in no way human health data.

### 2.5 Audio (voice messages)

**What:** voice messages you record and send to other users via Gléli's built-in messaging feature (one-to-one or group conversations).

**Purpose:** communication between colleagues on the same farm, or between Gléli contacts.

**Storage:** recorded locally on your device, then uploaded to **Cloudflare R2** so the recipient(s) can access the message. Conversation metadata (participants, groups, timestamps) is synchronized to our server.

**Sharing:** no sharing with any third party other than Cloudflare R2 (technical file hosting, see section 7) — the content of your messages is never used by anyone other than the recipients you chose.

### 2.6 Financial data

**What:** amounts and information related to your sales, loans, repayments, and payments (including the chosen payment method — Mobile Money, cash, bank transfer, cheque), plus the information required to process a Mobile Money payment through our partner **CinetPay**, and your purchases of AI-diagnosis credits via **RevenueCat**.

**Purpose:** managing your commercial activity (sales, loans), processing Mobile Money payments and payouts, and purchasing credits for AI diagnosis beyond the free monthly quota.

**Storage:**
- Your sales, loans, repayments, and payments are stored locally then synchronized to our server.
- Transactions processed through CinetPay (Mobile Money phone number, amount, currency, beneficiary name) are recorded on our server and replicated locally on the devices of authorized members of your farm.

**Sharing:**
- **CinetPay** (Mobile Money payment provider) receives the Mobile Money phone number, amount, currency, and, for a supplier payout, the beneficiary's name. Gléli never handles or stores any bank card data — only Mobile Money payments are supported.
- **RevenueCat** (in-app purchase management) only receives an anonymized internal identifier tied to your account — never your name, phone, or email. Actual payment information (bank card, etc.) is handled directly by Google Play or the App Store, never by Gléli or RevenueCat.

### 2.7 Phone contacts

**What:** with your explicit permission, Gléli may read the names and phone numbers in your phone's contact list to help you find people already on Gléli.

**Purpose:** to make it easier to add business contacts/partners already registered on Gléli.

**Storage and sharing:** this check is performed **entirely on your device**: your contact list is never sent to our server or to any third party. If you choose to invite a contact who isn't registered, the invitation is sent by SMS through your phone's native messaging app — not through our servers.

### 2.8 Plant disease diagnoses

See section 2.4 for details of the photo flow. The textual diagnosis data (detected disease name, symptoms, recommended treatments) is stored locally and on our server, associated with your farm, so you can review your diagnosis history. This is agronomic data (crop health), not human health data.

### 2.9 Technical identifiers

**What:** a unique identifier generated for your device, session (login) and session-renewal tokens, and technical information sent in the event of an application error (error log, screen name involved).

**Purpose:** keeping your session securely logged in, and detecting and fixing application bugs.

**Storage:** login tokens are stored in the secure storage area provided by your device's operating system (never in a regular database). The device identifier and renewal tokens are linked to your account on our server to allow secure session renewal.

**Sharing:** **Sentry** (application error-monitoring service) receives technical error logs when the application crashes, so we can fix bugs. We have configured Sentry so that it never receives a password, PIN code, session token, or other secret, even during a crash — see section 7.

---

## 3. Legal basis for processing

Depending on the nature of the data and the context, we rely on the following legal bases:

- **Consent**: for creating your account, enabling biometric authentication, accessing your phone contacts, and sending a technical bug report (always opt-in, never automatic).
- **Performance of a contract** (Gléli's terms of use, which you accept at sign-up): for all business features required for the app to function — managing your plots, operations, stock, sales, transport, processing, traceability, and messaging between members of your farm.
- **Legitimate interest**: for application security (technical error logs, geographic anti-fraud detection when logging operations) and service improvement.
- **Legal obligation / regulatory traceability**: certain traceability data (harvest lots, processing, transport, compliance self-assessments) is kept to meet food-traceability requirements (e.g. EU regulation 178/2002, HACCP/ISO 22000/GlobalG.A.P. frameworks you choose to use within the app).

---

## 4. Data retention

We keep your data for as long as your account is active, in order to provide the service. Beyond that, here is the current state of affairs — **we would rather be transparent about what still needs improving than claim a purge policy that doesn't yet exist**:

- **Photos (AI diagnosis, record documents) and voice messages stored on Cloudflare R2**: as of today, **no automatic purge is in place** — these files are kept indefinitely on our storage space, even after a related plot or record is deleted. This is a point we are committed to improving (setting up a retention and automatic cleanup policy).
- **AI diagnosis results (text)**: kept indefinitely in our database, so you can review your full diagnosis history.
- **Account, plot, operation, sales, transport, processing, and traceability data**: kept for as long as your account is active, and beyond that according to the legal retention periods applicable to food-traceability records with evidentiary value.
- **PIN code and biometric data**: the PIN stays local to your device and is removed if you uninstall the app; biometric data is never stored by Gléli at all (see 2.2).
- **Account deletion requests** (see section 5): we process your request manually; as of today, this process does not yet include an automated, exhaustive purge of all associated files (photos, audio) on our storage — a fully automated deletion workflow is under construction.

---

## 5. Your rights

### 5.1 Right of access and data portability

You can export a copy of your data in JSON format at any time, directly from the app (Profile → Support & data → "Export my data (backup)"). This export includes your account information, farms, plots, operations, stock, sales, and other business data tied to your active farm.

### 5.2 Right to erasure ("right to be forgotten")

You can request the deletion of your account and personal data from within the app (Profile → Support & data → "Delete my account").

**How this works today:** your request is sent to our team by email and **processed manually**, usually within 30 days. We want to be upfront that this process is not yet fully automated — we are working on a complete, automated deletion mechanism (including files stored on Cloudflare R2). If you are the sole owner of a farm shared with other members, the app recommends designating a new manager before sending your request, so your colleagues don't lose access to the farm.

Simply logging out of the app does not delete any data — that is a separate action from account deletion.

### 5.3 Right to rectification

You can correct your identity information (name, email, phone, country, date of birth, etc.) at any time directly from your profile in the app. For any correction you cannot make yourself, contact us at mailingiec@gmail.com.

### 5.4 Other requests

For any question about your rights, or to request that we restrict or object to the processing of your data, contact us at mailingiec@gmail.com (see section 8).

---

## 6. Data security

We implement the following measures to protect your data:

- **Encryption in transit**: exchanges between the app and our server, as well as with our third-party providers, use HTTPS (TLS encryption).
- **Biometrics never transmitted**: as detailed in section 2.2, no biometric data ever leaves your device — it is handled exclusively by the operating system.
- **Secure session tokens**: your login tokens are stored in the secure storage area provided by your operating system (never in a plain, regular database), and renewed through a secure rotation mechanism.
- **Passwords protected by cryptographic hashing** server-side (industry standard) — never stored or transmitted in plain text.
- **PIN code** protected by cryptographic hashing, strictly local to your device, never transmitted to our server.
- **Per-farm access isolation**: access to stored files (photos, documents, audio) is restricted to authorized members of the relevant farm, via temporary access links (valid for 15 minutes) rather than permanent links.
- **Application error monitoring** configured to actively exclude any secret (passwords, PIN codes, tokens) from what could be sent to our error-monitoring tool (Sentry), even when the app crashes.

No method of transmission or storage is ever completely foolproof, so we cannot guarantee absolute security, but we are committed to continuously maintaining and improving these protections.

---

## 7. Sharing data with third parties

We never sell your personal data. We share certain data, strictly to the extent necessary, with the following providers in order to operate Gléli:

| Third-party service | Role | Data received |
|---|---|---|
| **EmailJS** | Sending emails (support, bug reports, sign-up verification codes) | Name, phone, email, content of your message or bug report |
| **Anthropic** (Claude model) | AI-based analysis of plant photos for disease diagnosis | The plant photo submitted for diagnosis |
| **Cloudflare R2** | File storage (diagnosis photos, record documents, voice messages) | The files themselves, tied to your farm |
| **CinetPay** | Processing Mobile Money payments and payouts | Mobile Money phone number, amount, currency, beneficiary name (for payouts) |
| **RevenueCat** | Managing in-app purchases (AI diagnosis credits) | An anonymized internal identifier for your account (never your name, phone, or email) |
| **Sentry** | Application error monitoring and diagnostics | Technical error logs, excluding any password, PIN code, or session token |
| **Neon (PostgreSQL)** | Hosting our server-side database | All the synchronized data described in section 2 (technical hosting only, no use of the data by Neon itself) |
| **Google Play / Apple App Store** | Processing payments for in-app purchases | Your payment information (bank card, etc.) — never passed to Gléli or RevenueCat |
| **api.qrserver.com** | Generating the QR code image on traceability labels | The harvest lot code (an agricultural identifier, not personal data) |

Each of these providers is bound by its own terms of service and privacy policy, which you are welcome to review. We choose our providers with their data-protection commitments in mind.

---

## 8. Contact

For any question about this privacy policy or the processing of your personal data, contact us:

- **Email:** mailingiec@gmail.com
- **From the app:** Profile → Support & data → "Contact Gléli support"

We are committed to responding to any request within a reasonable timeframe.

---

*This policy may be updated to reflect changes to the application or to applicable regulations. Any substantial change will be communicated to you.*

