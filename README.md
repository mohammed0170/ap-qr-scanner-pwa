# AP QR Scanner

**A simple browser-based QR scanner for Extreme AP4020 access points.**

AP QR Scanner lets you scan the QR codes printed on **Extreme AP4020 boxes** using a device camera. It automatically extracts the **Serial Number** and **MAC Address**, stores the results locally in the browser, and exports the collected APs to a CSV file.

This is particularly useful when installing or preparing **multiple APs** and you need to collect their MAC addresses for **DHCP reservations** or their Serial Numbers for **ExtremeCloud IQ**.

## Works on phones, tablets and PCs

AP QR Scanner is a **web-based application**. No mobile or desktop application needs to be installed.

It can be used on:

- iPhone with Safari
- Android phones with Chrome or another modern browser
- iPad and Android tablets
- Windows PCs with a webcam
- macOS computers with a webcam
- Linux computers with a webcam
- Other devices with a modern web browser and a camera accessible to that browser

The requirement is simple:

**If the device can access the web application through a modern browser and the browser can access a camera, it can be used to scan QR codes.**

For a phone, this normally means using the rear camera. On a PC or laptop, it can use the built-in webcam or another camera available to the browser.

## What it does

Instead of manually typing information from each AP box:

1. Open AP QR Scanner in your web browser.
2. Tap or click **Scan QR Code**.
3. Allow the browser to access the camera.
4. Point the camera at the QR code on the AP4020 box.
5. The application reads the QR code automatically.
6. The **Serial Number** and **MAC Address** are displayed.
7. Select **Save & Scan Next**.
8. Scan the next AP.
9. Continue until all APs have been scanned.
10. Select **Export CSV** when finished.

For example, a QR code may contain:

```text
PROG#:TEST-AP-0001;DESCRIPTION:AP4020-WW;PART#:AP4020-WW;MAC:02a1b2c3d4e5;SYSTEM:TEST-SYSTEM-001;
```

The application extracts:

```text
Serial Number: TEST-AP-0001
MAC Address: 02a1b2c3d4e5
```

The other fields are ignored.

The values above are **fictional test data**.

## Why it is useful

If you have 50, 100 or more APs to install, manually recording every Serial Number and MAC Address is slow and prone to typing errors.

AP QR Scanner lets you scan the AP boxes one after another and create a clean inventory list.

The application displays a running counter, for example:

**Scanned: 50**

You can then export the complete list as a CSV file.

## DHCP reservations

The exported MAC address list can be used when preparing DHCP reservations for the new access points.

The application does **not** directly configure your DHCP server. It collects the MAC addresses and provides them in a CSV file for use with your existing DHCP process.

## ExtremeCloud IQ

The Serial Number column can be used when preparing an AP inventory for **ExtremeCloud IQ**.

Instead of manually reading the Serial Number from every AP box, scan the QR code and export the collected Serial Numbers.

The application does **not** connect to or upload information to ExtremeCloud IQ. The CSV is provided for you to use with your existing ExtremeCloud IQ workflow.

## Camera access

The browser must be allowed to use the device camera.

Camera access is requested **only when you start scanning**.

When the browser asks whether the website can use the camera, select **Allow**.

If camera access was previously denied, enable camera permission for the website in your browser settings and try again.

### On a phone or tablet

Use the rear camera where available and hold the QR code inside the on-screen scanning box.

### On a PC or laptop

Use the built-in webcam or another camera connected to the computer. Make sure the browser has permission to use it.

## HTTPS requirement

Camera access in modern browsers normally requires a **secure HTTPS website**.

For example, a GitHub Pages address can be used.

Do not expect camera access to work correctly by simply double-clicking `index.html` and opening it as `file://...`.

## Works offline after caching

The application is designed so that the app files can be cached by the browser for later use.

For the most reliable setup, open the web application once while connected to the internet so the application and QR scanning library can be cached.

After that, scanning can continue without a live internet connection, provided the browser still has access to the cached application and the device camera.

## Your AP information stays on the device

There is no:

- Login
- User account
- Cloud database
- Subscription
- Server-side AP inventory

The QR code is processed in the browser.

The Serial Numbers and MAC Addresses are stored locally in the browser on that device.

The application does not send your AP inventory to a server.

The exported CSV is created only when you choose **Export CSV**.

**Important:** browser storage is local to the particular browser/device. If you clear the browser's site data, use private/incognito browsing, or change to another browser/device, the saved inventory may not be available there.

## Duplicate protection

The application prevents accidental duplicate entries.

A scan is rejected if either the Serial Number or MAC Address has already been scanned.

The duplicate is not added to the inventory.

## Editing and deleting

Every saved AP can be edited if a correction is required.

You can also delete an individual AP.

There is a **Clear All** option for deleting the complete inventory.

The application asks for confirmation before deleting all records.

## CSV export

The exported file contains exactly:

```text
Serial Number,MAC Address
```

Example:

```csv
Serial Number,MAC Address
TEST-AP-0001,02a1b2c3d4e5
TEST-AP-0002,02A1B2C3D4E6
TEST-AP-0003,02A1B2C3D4E7
```

The filename uses the current date:

```text
AP_Inventory_YYYY-MM-DD.csv
```

## QR code format

The scanner looks for these two fields:

```text
PROG#
MAC
```

Additional fields are allowed and are ignored.

## If a QR code is invalid

The application will not save an incomplete AP.

If the QR code does not contain `PROG#` or `MAC`, it will display an error explaining that both fields are required.

## Typical installation workflow

For example, imagine an installation with **50 Extreme AP4020 boxes**.

**AP 1 → Scan → Save**

**AP 2 → Scan → Save**

**AP 3 → Scan → Save**

Continue until all APs have been scanned.

The application then shows the number of APs scanned. Select **Export CSV** to create one file containing the Serial Numbers and MAC Addresses for the entire batch.

The file can then be used as part of your DHCP reservation and ExtremeCloud IQ preparation processes.

## Test data

The Serial Numbers, MAC Addresses and SYSTEM values shown in this README are **fictional test values**.

Example:

```text
Serial Number: TEST-AP-0001
MAC Address: 02a1b2c3d4e5
SYSTEM: TEST-SYSTEM-001
```

`AP4020-WW` is used only as an example product description/part number.

## Requirements

You need:

- A device with a modern web browser
- A camera accessible to that browser
- Camera permission enabled for the website
- An HTTPS address for the web application when using a normal hosted website

No native app installation is required.

## Version 1

Version 1 focuses on four things:

- **Scan** AP QR codes
- **Store** Serial Numbers and MAC Addresses locally
- **Prevent** duplicate AP records
- **Export** the inventory to CSV

It deliberately does not include a login, cloud database, DHCP configuration or direct ExtremeCloud IQ integration.


## MAC Address format

The scanner accepts a MAC address from the QR code with or without separators.

For example, both are accepted:

```text
02a1b2c3d4e5
02:a1:b2:c3:d4:e5
```

Valid 12-character MAC addresses are normalised to the standard colon-separated format:

```text
02:a1:b2:c3:d4:e5
```

The CSV export therefore uses the colon-separated format, which is commonly used when entering or importing MAC addresses into DHCP systems.
