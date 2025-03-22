# Click Jacking Checker 🛡️

A simple and intuitive tool to test if a website is vulnerable to clickjacking attacks. This tool loads the target website in an iframe, allowing you to visually determine if the site is vulnerable.

---

## Table of Contents
1. [What is Clickjacking?](#what-is-clickjacking)
2. [Impact of Clickjacking](#impact-of-clickjacking)
3. [Root Cause of Clickjacking](#root-cause-of-clickjacking)
4. [Recommendations to Prevent Clickjacking](#recommendations-to-prevent-clickjacking)
5. [How to Use the Tool](#how-to-use-the-tool)
6. [Disclaimer](#disclaimer)

---

## What is Clickjacking?

Clickjacking (also known as **UI Redress Attack**) is a malicious technique where an attacker tricks a user into clicking on something different from what the user perceives. This is typically done by embedding the target website in a transparent iframe and overlaying it with deceptive elements.

For example:
- An attacker could embed a banking website in an iframe and overlay a fake button that says "Claim Your Prize."
- When the user clicks the fake button, they are actually clicking on the "Transfer Money" button on the banking website.

---

## Impact of Clickjacking

1. **Unauthorized Actions**:
   - Attackers can trick users into performing actions they did not intend, such as transferring funds, changing account settings, or making purchases.

2. **Data Theft**:
   - Sensitive information (e.g., passwords, credit card details) can be stolen by tricking users into entering it into a hidden iframe.

3. **Reputation Damage**:
   - If users are victimized through your website, it can harm your organization's reputation and trustworthiness.

4. **Legal and Compliance Issues**:
   - Failure to protect against clickjacking can lead to violations of data protection regulations (e.g., GDPR, CCPA).

---

## Root Cause of Clickjacking

The primary root cause of clickjacking is the **lack of proper frame-busting mechanisms** on the target website. Specifically:
- Websites that do not implement the **`X-Frame-Options`** HTTP header or the **`Content-Security-Policy` (CSP)** header are vulnerable.
- Without these protections, browsers allow the website to be embedded in an iframe, making it susceptible to clickjacking attacks.

---

## Recommendations to Prevent Clickjacking

To protect your website from clickjacking, implement the following measures:

### 1. **Use the `X-Frame-Options` Header**
   - Set the `X-Frame-Options` header to `DENY` or `SAMEORIGIN`:
     ```http
     X-Frame-Options: DENY
     ```
     - `DENY`: Prevents the page from being displayed in a frame.
     - `SAMEORIGIN`: Allows the page to be displayed only in a frame on the same origin.

### 2. **Use the `Content-Security-Policy` (CSP) Header**
   - Use the `frame-ancestors` directive in the CSP header to control which sites can embed your page:
     ```http
     Content-Security-Policy: frame-ancestors 'none';
     ```
     - `'none'`: Prevents the page from being embedded in any frame.
     - `'self'`: Allows the page to be embedded only in frames on the same origin.

### 3. **Implement JavaScript Frame-Busting**
   - Add a frame-busting script to your website:
     ```javascript
     if (top !== self) {
         top.location = self.location;
     }
     ```
   - Note: This method is less reliable than HTTP headers and can be bypassed by attackers.

### 4. **Educate Users**
   - Inform users about the risks of clickjacking and advise them to be cautious when clicking on unfamiliar elements.

---

## How to Use the Tool

1. Open the **Click Jacking Checker** tool.
2. Enter the URL of the website you want to test (e.g., `https://example.com`).
3. Click **Test Website**.
4. Observe the iframe:
   - **If the website loads in the iframe**, it is **vulnerable** to clickjacking.
   - **If the iframe remains blank or shows an error**, the website is **protected**.

---

## Disclaimer

This tool is for **educational and testing purposes only**. It does not guarantee 100% accuracy in detecting clickjacking vulnerabilities due to browser restrictions and cross-origin policies. Always use additional security testing tools and manual verification for comprehensive assessments.

---
