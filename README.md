# Hisab – GST Billing (v1.1.0)

Offline GST billing app for shops. Works on Android phones, iPhones/iPads, Windows, Mac, Linux and Chromebooks. Installs from the browser like a normal app and works without internet after the first open.

## Files
| File | Purpose |
|---|---|
| `index.html` | The complete app (screens, GST maths, PDF bills, storage) |
| `manifest.webmanifest` | App name and icons used when installing |
| `sw.js` | Keeps the app working offline |
| `icons/` | App icons |
| `keygen.html` | **Your** tool for making license keys (owner only) |

Keep all files together in one folder. Do not rename them.

## Step 1 – Put the app online (one time, free)
The app must be opened from an **https** link once, so phones and computers can install it.

**Option A – GitHub Pages (free)**
1. Create a free account at github.com.
2. Click **New repository**, name it `hisab`, choose **Public**, click **Create**.
3. Click **uploading an existing file**, drag in `index.html`, `manifest.webmanifest`, `sw.js`, `README.md` and the `icons` folder. Click **Commit changes**.
4. Open **Settings → Pages**. Under *Branch* choose `main` and `/ (root)`, click **Save**.
5. After 1–2 minutes your link appears, for example `https://yourname.github.io/hisab/`.

**Option B – Your own website (e.g. jslbharat.com)**
Upload the folder through cPanel File Manager or FTP into a folder such as `public_html/billing/`. Your link becomes `https://jslbharat.com/billing/`. The site must use https.

## Step 2 – Install on each device
- **Android (Chrome):** open the link → tap **Install app** in the app header, or ⋮ menu → **Install app / Add to Home screen**.
- **iPhone / iPad (Safari):** open the link → Share button → **Add to Home Screen**.
- **Windows / Mac / Linux (Chrome or Edge):** open the link → click the install icon at the right end of the address bar, or **Install app** in the app header.

After installing, the app opens from its own icon and works offline.

## Step 3 – First use
1. Enter the business name, address, state, GST registration type and GSTIN. The app checks the GSTIN is valid.
2. Go to **Items** and add your products. Type the item name: the app suggests the HSN code and GST rate for common items. Tap a suggestion to fill them. For anything else, use the *Search HSN on the official GST portal* link.
3. Go to **Bill**, tap items, enter customer details if needed, and tap **Save bill**.
4. Print, share the PDF (WhatsApp etc.), or send as WhatsApp text.

## Features
- Tax invoice / Bill of supply (composition) / Cash memo (unregistered)
- CGST + SGST for same-state sales, IGST automatically for other states (from the customer GSTIN or place of supply)
- GST rates 0%, 0.25%, 3%, 5%, 18%, 40%; prices with or without GST
- GSTIN check-digit validation, amount in words, round off
- PDF bills (58 mm, 80 mm, A4) made on the device, no internet needed
- Cancel bills (number kept, excluded from totals)
- Sales summary and GST report CSV for your CA
- Items import/export by CSV: columns `name, hsn, gst_rate, price, unit, name_odia`
- English and Odia
- Backup and restore

## Important
- **GST rates:** the built-in suggestions cover common items as per CBIC Notification 9/2025-Central Tax (Rate), effective 22 September 2025. GST depends on the exact product description, and rates can change. Each business must confirm its own rates with a CA or the GST portal.
- **Data** is stored only on the device. Use **Settings → Download backup** every week. Clearing browser data or uninstalling the app deletes the data.
- **E-invoicing (IRN)** is not included. Businesses whose turnover requires e-invoicing need an IRP-connected system.
- **Printing:** the app uses the device's normal print option. For Bluetooth thermal printers on Android, install the free *RawBT* app or use a printer whose Android app adds itself as a print service.

## Licensing (30-day trial + license keys)
Every new installation gets a **30-day free trial**. After that, the shop can still view old bills, reports and take backups, but cannot make new bills until it enters a license key.

**Your secret file:** `hisab-signing-key-PRIVATE.json` (sent separately, NOT inside the app folder).
- It is the only thing that can create keys. Keep copies in two safe places (e.g. Google Drive + a pen drive).
- **Never upload it to GitHub or your website. Never send it to anyone.**

**Before you start selling:** open `index.html` and put your WhatsApp number in the line
`const VENDOR = { name: "Hisab Billing", phone: "" };` for example `phone: "9876543210"`, and change the name if you like. Customers then see a button to message you.

**Selling a key (2 minutes):**
1. The customer opens Hisab → Settings → License, and sends you the **Business ID** shown there (their GSTIN, or their phone number if they have no GSTIN).
2. You take payment (UPI etc.).
3. Open `keygen.html` (from your website link or your own device), load your signing-key file (tick *Remember* on your own phone so you only do this once).
4. Enter the Business ID, pick *+1 year*, tap **Create key**, then **Send on WhatsApp**.
5. The customer pastes the key in Settings → License → **Activate**.

Notes:
- A key works only for that one GSTIN/phone, on any number of that shop's devices, and survives reinstalling or restoring a backup.
- If a shop changes its GSTIN or phone in Business details, it needs a new key from you.
- Moving the phone's date backwards does not extend a trial or license.
- `keygen.html` can safely sit on your website: it is useless without your private file. Keys you issue are listed on that page; download the list regularly.
- Honest limit: no copy protection is unbreakable. A skilled programmer could edit the app's code to remove the check. This system stops normal sharing and copying, which is what matters for small-shop customers.

## Updating the app later
Upload the changed files to the same place, and change `VERSION` at the top of `sw.js` (for example to `hisab-1.0.1`). Devices update the next time the app is opened with internet.
