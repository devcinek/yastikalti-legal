# YASTIK ALTI — PRIVACY POLICY

**Effective Date:** May 5, 2026
**Last Updated:** May 5, 2026
**Version:** 1.1

> In case of conflict between this English version and the Turkish version, the **Turkish text shall prevail**.

---

## 1. GENERAL PROVISIONS

### 1.1. Data Controller
This Privacy Policy ("**Policy**") explains how personal data is collected, processed, stored, shared and protected in connection with the **Yastık Altı** mobile application (the "**Application**").

- **Data Controller:** Doğan Cinek (individual developer), Republic of Türkiye
- **Contact:** devcinek@gmail.com
- **Application:** Yastık Altı (App Store: com.dogancinek.yastikaltin)

### 1.2. Legal Basis
This Policy has been prepared within the framework of **Turkish Personal Data Protection Law No. 6698** ("**KVKK**"), the **EU General Data Protection Regulation** ("**GDPR**") (to the extent applicable), the **California Consumer Privacy Act / California Privacy Rights Act** ("**CCPA/CPRA**") (to the extent applicable), and **Apple App Store Privacy Requirements**.

### 1.3. Acceptance and Binding Effect
By downloading, installing, opening, or using the Application in any manner, you **unconditionally** declare that you have read, understood, fully accepted this Policy and given **explicit consent** to the data processing activities described herein. If you do not accept this Policy, your sole remedy is to refrain from using the Application and remove it from your device. Any ambiguity in interpreting this Policy shall be resolved **excluding the contra proferentem rule**, in line with the Developer's reasonable commercial interests and mandatory provisions of Turkish law.

### 1.4. Scope
This Policy covers all components of the Application, including the iOS application, Apple Watch companion app, home and lock screen widgets, Live Activity, Siri/App Intents, the Multipeer Connectivity- and NearbyInteraction-based "Altın Günü" feature, CloudKit private database synchronization, CloudKit Family (shared) zone, and push notification infrastructure.

---

## 2. DATA COLLECTED AND COLLECTION METHODS

### 2.1. **Data Stored Locally on Your Device** (Not Sent to Developer Servers)

The following data is stored **only on your device** in the SwiftData/CoreData database and App Group `UserDefaults` and is **never sent to any server controlled by the Developer**:

| Data Category | Detail |
|---|---|
| **Gold transactions** | Purchase date, gram amount, paid amount (TRY/USD), jeweler name (optional), notes |
| **Silver transactions** | Same structure; silver type (Bullion/925/900/830/Gram), purity coefficient, workmanship delta |
| **Financial goals** | Goal type (gram/TL), target amount, start/end date |
| **User preferences** | Notification threshold rules (local copy), theme, language, persona, kumbara reminder date |
| **Widget dataset** | Total grams, portfolio value, gram price, USD/TRY — shared via App Group |
| **OCR / Receipt scan (if used)** | Photo and OCR extraction are **deleted from device immediately** after processing; only the text the user opts to save persists in SwiftData |

**Note:** This data is stored on Apple's iCloud infrastructure if the user's iCloud backup or CloudKit sync is enabled (see § 2.5). The Developer **has no access and cannot access** this data; SwiftData records are encrypted at the device/iCloud level.

### 2.2. **Data Processed Server-Side** (Limited, Anonymous or Anonymized)

| Data | Purpose | Storage | Retention |
|---|---|---|---|
| **FCM Push Token** | Anonymous device identifier issued by Apple/Google to deliver push notifications | Firebase Cloud Messaging (Google Ireland Ltd.) + Google Sheets (token only) | While the token is valid or until the user disables notifications |
| **Topic subscriptions** | Subscription state for `gold_daily`, `silver_daily`, `all_users` topics (anonymous) | Firebase Cloud Messaging | While subscription is active |
| **Threshold notification preferences** | Price/percentage threshold rules; no device identifier, only mapped to anonymous FCM token | Google Sheets (Apps Script) | Until user deletes |
| **Live Activity APNs token** | Ephemeral token issued by Apple to push Dynamic Island / Live Activity updates | Firebase Cloud Functions / Realtime Database (Google Ireland Ltd. or US region) | Auto-deleted when activity ends; at most **30 days** |
| **Live Activity baseline snapshot** | Spot price / workmanship snapshot at registration to compute change% in pushes | Firebase Realtime Database | Until activity ends; at most 30 days |
| **Crash reports** *(if any)* | Anonymous crash stack traces; no personal data | Apple App Store Connect or equivalent | 90 days |

**No device identifier (IDFA, IDFV) is collected.** No advertising tracking is performed. The Developer operates no mechanism to derive a user's real identity from these server records.

### 2.3. **Data Processed by Apple** (No Developer Access)

Apple processes the following data within its own privacy policy under App Store purchase, subscription management, iCloud, CloudKit and APNs infrastructures. The Developer has **no control, visibility, or access**:

- Apple ID email (**not transmitted** to Developer)
- Payment information (**not transmitted** to Developer; only "Premium active/inactive" status flag)
- StoreKit purchase receipt (verification only)
- Device model, iOS version, App Store Connect analytics (anonymous)
- iCloud / CloudKit records (Apple infrastructure, bound to Apple ID)
- APNs certificate and delivery metadata

### 2.4. **Categories Not Collected**

We **do not collect**:

- ❌ First name, last name, date of birth, government ID
- ❌ Email address (unless you contact us directly)
- ❌ Phone number
- ❌ Physical address, postal code
- ❌ Geolocation (GPS, IP-based, Wi-Fi-based)
- ❌ Microphone recordings (Siri utterances go to Apple; not transmitted to Developer)
- ❌ Photo library (unless user manually selects)
- ❌ Contacts, calendar, health data
- ❌ IDFA, IDFV
- ❌ Bank account, credit card information
- ❌ Passwords, biometric authentication data
- ❌ Voiceprints / biometric voice signatures
- ❌ Any personal information that could be sold to third parties

### 2.5. **iCloud / CloudKit Private Database Synchronization**

The Application uses **Apple CloudKit Private Database** to sync transactions and goals across the user's devices:

- Synchronization is **bound to the user's Apple ID** and occurs **exclusively on Apple infrastructure**;
- The Developer has **no access** to CloudKit Private DB content and such access is **technically impossible**;
- Sync requires that iCloud is enabled, "iCloud Drive" is permitted, and the iCloud toggle for Yastık Altı is on;
- The Developer is **not liable** for sync errors, delays, data inconsistencies, conflict-resolution losses, or outages of Apple's CloudKit service;
- To disable sync: iOS Settings → Apple ID → iCloud → Yastık Altı toggle off. New data will not be written to the cloud; existing cloud records remain subject to Apple's iCloud deletion policy.

### 2.6. **CloudKit Family Portfolio (CKShare) — CRITICAL NOTICE**

The "Family Portfolio" feature uses **Apple CloudKit Sharing** (CKShare). A host user creates a shared zone and may invite other users (invitees) via a CKShare URL.

**Data Flow and Visibility:**

| Visible Item | To Whom | Scope |
|---|---|---|
| All transaction records in the shared zone | Host + all accepted participants | Including grams, paid amount, jeweler, notes |
| Shared goals | Same | Goal name, amount, progress |
| Participant display name / Apple ID display email | Host + other participants | Surfaced by Apple's CKShare system |

**Joint Controller Provision (KVKK / GDPR):**

The host who creates a Family Portfolio and all invitees who accept are **joint data controllers** for the shared data. The Developer is **in no event liable** for any sharing within the Family Portfolio, third-party participant actions, false/misleading/unlawful data entries within the shared zone, or disputes between participants. The host:

- Represents that all invited participants are **over 18 or have valid parental consent**;
- Represents that all invited participants have accepted this Policy and the Terms of Use;
- Represents that no third-party personal data is included in shared content without that party's explicit consent;

and **agrees in advance, accepts, and undertakes** the foregoing, agreeing to **indemnify** the Developer against any claims arising from a breach of these representations (see Indemnification clause in the Terms of Use).

**Withdrawal and Deletion:**

- The host may delete the household; Apple will then delete the CloudKit zone;
- An invitee may decline a CKShare or leave the zone after acceptance; however, due to Apple's technical constraints, an invitee acting alone cannot delete a zone without the host;
- Latency and eventual-consistency behavior in Apple's infrastructure are not the Developer's responsibility.

### 2.7. **Apple Watch + WCSession**

The watchOS companion app (Yastık Altı Watch App) and Watch Complications extension exchange data between iPhone and watch **only via local WatchConnectivity (WCSession) `applicationContext`**:

- Synchronized fields: gram price, total portfolio value, profit/loss percent, USD/TRY, ounce prices, transaction count, last updated timestamp.
- **Data is not sent to Apple/Developer servers**; it is transmitted directly over the local Bluetooth/Wi-Fi channel between watch and phone.
- The cache on the watch (App Group `UserDefaults`) is wiped when the device is erased.

### 2.8. **Live Activity Push Infrastructure**

Data flow used for Live Activity (Dynamic Island) updates:

1. The iOS app sends Apple's **APNs Live Activity push token** to the Developer's Firebase Cloud Functions endpoint over HTTPS.
2. The Cloud Function records the token in Realtime Database alongside a baseline (snapshot of spot price at registration).
3. A scheduled function (every 10 minutes) reads RTDB and pushes via APNs ES256 JWT; failed tokens (BadDeviceToken, etc.) are silently cleaned up.
4. When the Live Activity ends, the token is unregistered; cleanup occurs within at most **30 days**.

The token is an anonymous Apple-issued identifier and cannot be mapped to a user's identity in isolation. No name, email, IP, or device fingerprint is transmitted in pushes.

### 2.9. **Altın Günü — Multipeer Connectivity, NearbyInteraction, Local Network**

The "Altın Günü" feature digitizes face-to-face gold-day sessions (a Turkish gold-saving custom). It requires:

- **Local Network permission** — to discover nearby devices on the same Wi-Fi via Bonjour;
- **NSNearbyInteractionUsageDescription (NI)** — proximity/distance measurement (UWB) to confirm physical transfer;
- **Multipeer Connectivity** — Apple's peer-to-peer protocol for messaging and session coordination.

**Data Flow:**

- During a session, the user's chosen **nickname**, randomly assigned **avatar emoji**, **gram amount**, **transaction time**, and **transfer status** are shared **only with the other devices in that session**.
- No data is sent to Developer servers or Apple servers (Apple may relay MPC traffic only).
- Shared data is wiped from each device's local state when the session ends; the session summary card (screenshot) may be saved to the user's own gallery.
- NI distance data stays on-device and is not transmitted to any party.

**User Responsibility:** All participants in an Altın Günü session are deemed to have accepted this Policy and the Terms of Use prior to joining. The Developer is **not responsible** for any content shared within a session or any physical gold exchange between participants. The "transfer complete" notification is **only a digital UI event**; physical gold exchange is **entirely a matter between the participants**.

### 2.10. **Siri / App Intents**

The Application supports voice queries via iOS Siri and App Shortcuts (e.g., "Hey Siri, Yastık Altı gram altın"). For these features:

- The user's voice recording is processed by **Apple's Siri infrastructure** and is **not transmitted** to the Developer (Apple Siri Privacy: https://www.apple.com/legal/privacy/data/en/siri/).
- When an intent runs, the app reads the **current portfolio/price snapshot** from the App Group; no network calls are made and no data is transmitted out.
- When voice-add transaction intents run, data is written only to the device's SwiftData / CloudKit infrastructure.

---

## 3. PURPOSES AND LEGAL BASES OF PROCESSING

### 3.1. Legal Bases under KVKK Art. 5 / GDPR Art. 6

| Data | Purpose | Legal Basis |
|---|---|---|
| Local transaction data | Portfolio computation, reporting | Performance of contract (KVKK 5/2-c, GDPR 6/1-b) |
| CloudKit Private Sync | Cross-device sync of user's own data | Contract performance + explicit consent (KVKK 5/1) |
| CKShare Family Portfolio | Shared zone with invitees | Explicit consent + joint controller arrangement (KVKK 5/1, GDPR 6/1-a + 26) |
| Apple Watch WCSession | Live data on watch | Performance of contract (KVKK 5/2-c, GDPR 6/1-b) |
| Live Activity push token | Dynamic Island / Live Activity updates | Explicit consent (KVKK 5/1, GDPR 6/1-a) |
| FCM token + topic + threshold | Push notification delivery | Explicit consent (KVKK 5/1, GDPR 6/1-a) |
| Multipeer / NI data | P2P Altın Günü session | Explicit consent (KVKK 5/1, GDPR 6/1-a) |
| Apple purchase status | Activation of Premium features | Performance of contract (KVKK 5/2-c, GDPR 6/1-b) |
| Crash reports | Debugging, product improvement | Legitimate interests (KVKK 5/2-f, GDPR 6/1-f) |

### 3.2. Automated Decision-Making and Profiling
The Application **does not employ automated decision-making** or profile users. The Sell/Buy advisor module computes deterministic technical indicators from historical prices; these indicators are **general information derived from publicly available market statistics, not personalized recommendations**. There is no automated decision-making mechanism producing adverse outcomes for the user.

---

## 4. DATA SHARING AND THIRD PARTIES

### 4.1. Third-Party Service Providers

| Service | Provider | Data Processed | Location |
|---|---|---|---|
| **App Store Distribution & Payment** | Apple Inc. (USA) | Apple ID, purchase receipt | Apple infrastructure, global |
| **iCloud + CloudKit Private/Shared DB** | Apple Inc. | User data records (bound to Apple ID) | Apple infrastructure, global |
| **APNs (incl. Live Activity)** | Apple Inc. | APNs token, push payload (anonymous baseline) | Apple infrastructure |
| **Push Notifications** | Google Ireland Ltd. (Firebase Cloud Messaging) | Anonymous FCM token | EU / US data centers |
| **Server logic (Apps Script)** | Google LLC | Token + threshold rules (anonymous) | USA |
| **Cloud Functions + Realtime DB** | Google LLC / Firebase | Live Activity token + baseline (anonymous) | USA or EU regions |
| **Market data** | Third-party financial API providers | Anonymous request IP | Various |
| **U.S. CPI (FRED® API)** | U.S. Bureau of Labor Statistics, via FRED® (Federal Reserve Bank of St. Louis) | Only public economic indicators are pulled; no personal data shared | USA |

> **FRED® Attribution:** The Application uses the FRED® API for U.S. inflation calculations. FRED® and the FRED logo are registered trademarks of the Federal Reserve Bank of St. Louis. The St. Louis Fed **does not endorse or sponsor** this application. Source: U.S. Bureau of Labor Statistics (public).

### 4.2. **Sale to / Sharing With Third Parties for Advertising: ZERO**

> The Developer **DOES NOT SELL, RENT, SHARE, OR PROCESS for advertising** user data with any third party.

No personal data is shared in exchange for commercial value, including under CCPA/CPRA "sale" or "sharing" definitions. ATT (App Tracking Transparency) consent is not requested.

### 4.3. Disclosures Required by Law
The Developer will share data with authorities only:

- Where required by lawful request from courts or prosecutors of the Republic of Türkiye;
- To comply with anti-money-laundering reporting obligations;
- To prevent **imminent and concrete** threats to the life or safety of users or third parties.

The Developer will not engage in voluntary disclosures and **reserves the right to refuse informal law-enforcement requests in the absence of a judicial order**.

### 4.4. International Transfers
The Application uses Apple iCloud/CloudKit, Firebase, Google Apps Script and App Store infrastructures, which involve data centers **outside Türkiye (EU and USA)**. These transfers occur:

- **Under GDPR:** via Standard Contractual Clauses (SCCs) or Apple/Google's certified compliance mechanisms;
- **Under KVKK:** with the user's explicit consent or via mechanisms recognized by the KVKK Authority as providing adequate protection.

By enabling push notifications, CloudKit sync, Family Portfolio, or Live Activity, you give your **explicit consent** to international transfer of the relevant anonymous record/token data. Consent may be withdrawn at any time by disabling the relevant feature; withdrawal **does not have retroactive effect** and does not invalidate prior processing.

---

## 5. CHILDREN'S PRIVACY

The Application **is not directed to children under 13** and does not knowingly collect data from users under 13.

- **COPPA Compliance (USA):** If we learn that we have collected data from a child under 13, we will **delete it immediately**.
- **GDPR / KVKK:** Parental/guardian consent is required for users under 16.
- **Family Portfolio / iCloud Family Sharing arrangements** for minor invitees are the responsibility of the inviting host.
- If you believe your child has provided data: notify **devcinek@gmail.com**.

---

## 6. RETENTION PERIODS

| Data Category | Retention |
|---|---|
| Local on-device data | Until user deletes the application or manually clears |
| iCloud / CloudKit records | Subject to Apple's iCloud deletion policy; user must delete via iCloud Manage Storage |
| CKShare shared zone | Until host deletes the household; departing invitees lose access but records remain in the zone |
| FCM token | While token is valid or until user disables notifications (cleared after at most 12 months of inactivity) |
| Threshold rules | Until user deletes |
| Live Activity APNs token + baseline | Until activity ends; at most 30 days |
| Multipeer / NI session data | Wiped from device memory immediately after session ends; never sent to any server |
| Crash reports | 90 days |
| Statutory obligations | As required by applicable law (e.g., commercial book-keeping: 10 years) |

---

## 7. USER RIGHTS

### 7.1. Rights under KVKK Art. 11
As a data subject, you may request the following from the Developer:

a) Whether your personal data is processed;
b) Information on how it is processed;
c) The purposes of processing and whether they are met;
ç) Recipients in Türkiye and abroad;
d) **Correction** of inaccurate/incomplete data;
e) **Deletion or destruction** under statutory conditions;
f) Notification of (d) and (e) actions to recipients;
g) Objection to adverse outcomes from automated analysis;
ğ) Compensation for damages arising from unlawful processing.

### 7.2. GDPR Rights
If you reside in the EU/EEA, additionally:

- Right of access (Art. 15)
- Right to rectification (Art. 16)
- Right to erasure / "right to be forgotten" (Art. 17)
- Right to restriction (Art. 18)
- Right to data portability (Art. 20)
- Right to object (Art. 21)
- Right not to be subject to automated decision-making (Art. 22)
- Right to lodge a complaint with a supervisory authority

### 7.3. CCPA/CPRA Rights (California residents)
- Right to know categories of data collected;
- Right to deletion;
- Right not to have personal data sold/shared (we do not engage in such sharing);
- Right to limit use of sensitive personal information;
- Right to non-discrimination.

### 7.4. Exercising Rights and Identity Verification
Send all requests to: **devcinek@gmail.com**

Your email **must** include the following; otherwise the request **may be rejected** for insufficient identification:

- Type of request (access, deletion, correction, etc.) and the data category at issue;
- **Identity verification:** the **last 6 characters** of your device FCM token (Settings → About → Diagnostics) **or** a screenshot of your App Store purchase receipt;
- A contact email address.

We respond within **30 days**. For requests that are unfounded, excessive, repetitive, or abusive, we may charge a **reasonable fee** or **refuse the request** as permitted by KVKK Art. 13/2 and GDPR Art. 12/5.

### 7.5. Limits on Family Portfolio Data Rights
Requests to delete/correct CKShare data through the Developer alone are **technically limited** because the shared zone resides on Apple's infrastructure and the controller is joint. For this data:

- An invitee may end their own participation (leave the zone);
- The host may delete the entire household to remove the zone;
- The Developer cannot intervene in Apple's CloudKit infrastructure; deletion requests should be addressed to Apple.

---

## 8. DATA SECURITY

### 8.1. Technical Measures
- iOS **Sandbox** and **Data Protection** (Class A) mechanisms;
- In-app data stored in iOS Keychain and encrypted SwiftData/SQLite;
- Server communication mandates **HTTPS / TLS 1.2+**;
- FCM token transmitted over Firebase's TLS-encrypted channel;
- Cloud Functions endpoints accept only the expected payload formats;
- APNs pushes signed with ES256 JWT;
- Multipeer Connectivity sessions encrypted in `MCEncryptionRequired` mode;
- Apps Script access logging enabled.

### 8.2. Administrative Measures
- No one other than the Developer has access to data;
- All third-party providers are governed by their own data processing agreements (Apple DPA, Google DPA).

### 8.3. Breach Notification
In the event of a data breach:

- Notification to the KVKK Authority within **72 hours** under KVKK Art. 12/5;
- Notification to the relevant supervisory authority within **72 hours** under GDPR Art. 33 if EU data subjects are affected;
- Affected users will be notified without undue delay via in-app notice and/or public announcement.

### 8.4. Force Majeure
The Developer is **in no way liable** for damages arising from outages, errors, data losses, leaks, or external attacks affecting third-party components such as Apple iCloud/CloudKit, Firebase, Apple Watch pairing, APNs, Multipeer/NI infrastructures. The terms of use and privacy policies of those components apply with respect to those providers.

---

## 9. COOKIES AND SIMILAR TECHNOLOGIES

As a mobile application, **no traditional web cookies** are used. The following local storage mechanisms are used:

| Mechanism | Purpose |
|---|---|
| `UserDefaults` | App preferences (slot selections, notification toggles, debug flags) |
| `App Group UserDefaults` | Sharing between main app ↔ widget ↔ watch (`group.com.dogancinek.yastikaltin`) |
| `SwiftData` (over CoreData) | Transaction and goal records |
| `iOS Keychain` | (If used) sensitive preference data |
| `Bundle Resources` | Historical price data (static), audio files |

---

## 10. APPLE ATT (App Tracking Transparency)

The Application **does not perform user tracking** under Apple's **App Tracking Transparency** framework. No ATT prompt is shown. No IDFA is collected.

App Privacy labels on the App Store:

- ✅ **Data Not Collected** — applicable to a large extent
- Collected: only **"Diagnostics → Crash Data"** (if any, anonymous) and **"Identifiers → Device ID"** (FCM/APNs token, not linked to user)

---

## 11. CHANGES TO THIS POLICY

The Developer reserves the right to update this Policy from time to time. Material changes will be:

- Announced **at least 7 days before** the effective date via in-app notification;
- Reflected in the "Last Updated" date;
- Subject to **renewed consent** where material (e.g., new data category, new third-party processor).

Continued use of the Application after the effective date means **acceptance** of the updated Policy. Your sole remedy if you do not accept any change is to discontinue use of the Application.

---

## 12. CONTACT AND COMPLAINTS

| Topic | Contact |
|---|---|
| Data subject rights, KVKK/GDPR/CCPA requests | devcinek@gmail.com |
| General questions, product support | devcinek@gmail.com |
| KVKK supervisory authority | Personal Data Protection Authority — www.kvkk.gov.tr |
| GDPR supervisory authority | Data Protection Authority of your EU member state of residence |

---

## 13. LANGUAGE AND CONSTRUCTION

This Policy is published in Turkish and English. **In case of conflict, the Turkish text prevails.** Ambiguities in interpretation shall be resolved without applying the contra proferentem rule, in line with the Developer's reasonable commercial interests and mandatory provisions of Turkish law; illustrative enumerations ("including but not limited to" and similar) shall not be construed restrictively.

---

**BY ACCEPTING THIS PRIVACY POLICY, YOU AFFIRM THAT YOUR PERSONAL DATA MAY BE PROCESSED AS DESCRIBED HEREIN, FREELY, INFORMEDLY, AND WITH EXPLICIT CONSENT.**
