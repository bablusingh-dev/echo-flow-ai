# EchoFlow AI - Master Documentation Addendum

**Date**: May 2026  
**Document Status**: Active revision to *echoflow_ai_master_documentation.pdf*  
**Subject**: Architectural Revision of Bring Your Own Key (BYOK) storage and validation path.

---

## 1. Context of Revision

The initial architecture specified under **Section 1.2.1 (Unified BYOK Gateway & Hardware Wallet Integration)** and **Section 2.3 (State Management & Data Storage Architecture)** detailed client-side key storage leveraging hardware modules and device operating system-level encryption (`expo-secure-store`).

To simplify cross-device coordination, ensure keys can be easily checked/managed across platforms, and prevent reliance on device-locked keychains, the architecture has been revised to utilize an **Anonymous Device-ID Database-Backed Model**.

---

## 2. Updated Specifications

### 2.1 Section 1.2.1 Revision: Storage & Routing
* **No Client-Side Key Storage**: Client devices do not save API keys in local files or local SecureStore caches.
* **Anonymous Identification**: Users are identified solely by a hardware device signature retrieved securely at runtime (Android ID / iOS Vendor ID). No signin, signup, or profile forms are required.
* **Proxy-Based Key Storage**: User credentials are encrypted at the client boundary, transmitted over HTTPS, and stored in the Node.js Express proxy MongoDB database under the respective `deviceId`.
* **Server-Side Encryption**: Keys are encrypted on the server using `AES-256-GCM` before database persistence.

### 2.2 Section 2.3 Revision: Storage Technologies
* **Zustand Micro-Store**: Tracks state cache of key presence (e.g. `Gemini: Present (Valid)`) and `deviceId` without storing plain-text keys.
* **Expo SecureStore**: (Removed for API credentials) Placed in reserve.
* **Database Relays**:
  * **MongoDB (Backend)**: Master storage for encrypted credentials, rate limiting, and analytics.
  * **SQLite (Local Client)**: (Maintained) Logs local session metrics and real-time corrections.
