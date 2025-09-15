# MSQ Pay - API & Gateway Guide

## 📌 Introduction

**MSQ Pay** is a powerful payment processing API designed to simplify financial transactions for businesses of all sizes.
This guide covers **key features, integration steps, API usage examples, and best practices** for secure implementation.

---

## 🚀 Environments

| Environment | Public IP        | API Base URL         | Admin URL              | Gateway URL          |
| ----------- | ---------------- | -------------------- | ---------------------- | -------------------- |
| Development | `3.38.125.104`   | `api.dev.msq.market` | `dev-admin.msq.market` | `dev-pay.msq.market` |
| Staging     | `43.201.210.181` | `api.stg.msq.market` | `stg-admin.msq.market` | `stg-pay.msq.market` |
| Production  | `13.125.119.187` | `api.msq.market`     | `admin.msq.market`     | `pay.msq.market`     |

📺 [Gateway Demo (Video)](https://www.loom.com/share/b6e027fc8c30444fa9042afd1403e22a)

---

## 🛠 Getting Started

1. **Register Your Platform**

   * Go to the **Admin URL** and create a new account.
   * Navigate to **Platforms → Add new Platform**, fill in details, and submit for approval.
   * Once approved, you will receive **API credentials** for authentication.

2. **Prepare Wallet API**

   ```http
   POST {API Base URL}/wallet/prepare
   ```

   **Example Request**

   ```json
   {
     "dapp": {
       "name": "MetaStar",
       "url": "https://metastarglobal.io/"
     },
     "type": "send_transaction",
     "transaction": {
       "tokens": { "P2U": 10 },
       "to": "MSQf5de8c3babdd54ee3969976f904c2400"
     },
     "order_id": "order_12345"
   }
   ```

   **Example Response**

   ```json
   {
     "gateway_link": "https://pay.msq.market/?request_key=d3b07384...",
     "status": "prepared",
     "order_id": "order_12345"
   }
   ```

   Redirect the user to the `gateway_link` for payment.

---

## 🔍 Verifying Payments

You can verify payments in **3 different ways**:

1. **Wallet Result API**

   ```http
   POST {API Base URL}/wallet/result
   ```

   Response contains `status: completed` or `prepared`.

2. **WebSocket Listener**

   * Listen for `MSQPAY_TRANSACTION_SUCCESS` events.
   * Recommended for mobile apps or when redirect is not possible.

3. **Callback URL**

   * Set a callback URL during platform registration.
   * MSQ Pay will send POST requests after every successful transaction.
   * Always validate by **checking the allowed IP** (`13.125.119.187`).

---

## 💻 Code Samples

Examples are available for multiple languages:

* **PHP**
* **ASP.NET (C#)**
* **Node.js**
* **Python**

See the full guide for code snippets and integration details.

---

## 🔐 Security Recommendations

* Always **validate the request IP** (`13.125.119.187` in Production).
* Use HTTPS for all API communications.
* Store API credentials securely and rotate periodically.
* Use callback + WebSocket for robust verification.

---

## 📖 Documentation

For detailed examples and advanced use cases, please refer to the full PDF guide:
**MSQ Pay - API & Gateway Guide**.

