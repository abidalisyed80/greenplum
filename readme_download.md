**Installing Greenplum Database on Ubuntu 18.04 LTS - .deb PACKAGE Downloader**

Follow these steps to Download the Greenplum Database Versoin 6.24.4 for Ubuntu 18.04 LTS.

## 1. Download Greenplum Database Package

1. Signup and verify your account on [Pivotal Network](https://network.pivotal.io).
2. Login into the newly created account.
3. Go to your profile > edit profile.
4. Get the **LEGACY API TOKEN [DEPRECATED]** (e.g., txogurBEeWk7nSTL12456).
5. Install curl on your system: `sudo apt install curl`.
6. Run the command below on the terminal to activate your **LEGACY API TOKEN**:
   ```bash
   curl -X GET https://network.pivotal.io/api/v2/products/vmware-greenplum/releases/1485474/product_files/1753189/download -H "Authorization: Token txogurBEeWk7nSTL12456"

The response should be like below:
```json
{"status":403,"message":"We are reviewing the transaction that you have submitted. Confirm that you provided a valid first name, last name, address and country when you registered. Please note that it will take 24 hours for the review process to confirm your eligibility. Contact Support after 24 hours if you have any questions. Quote message ID \"Error 621\" and provide the email address you used when registering."}
```
7. Now wait 12-24 hours.
8. After 24 hours, login back into Pivotal Network.
9. In a new tab, open the following link: Greenplum Database.
10.    Select the desired Greenplum version from the drop-down menu (e.g., 6.24.4) and select 'Greenplum Database Server'.
       You will see a warning below:
```bash
Warning: Before you can download any components of this release you will need to sign an end user license agreement (EULA). After signing the EULA you will be able to download the components of this release until a new major version of this product is released (for generally available products), until any new release of this product is released (for alpha or beta products) or when the EULA itself changes. Click here to sign the EULA.
```
11. Click on the EULA link.
12. Go to your profile > Accepted EULAs. The requested version's EULAs must appear in the list. If not, then wait until it appears there.
13. Once EULAs are activated against the desired version, click the 'Download' blue cloud icon to download the installer file.

## 2. Installation and Configuration

Follow the instructions provided in the README.md file for installing and configuring Greenplum Database  v 6.24.4 on Ubuntu 18.04 LTS
