# Bristo 2FA Authenticator Project Documentation

## 1. Project Vision
The **Bristo 2FA Authenticator** is a secure, cloud-based web application designed to deliver a robust Two-Factor Authentication (TOTP) system. Our goal is to provide a highly secure, transparent, and user-friendly platform that generates time-based one-time passwords (TOTP) using a custom-built algorithm. The system includes a dual-backend architecture, an emergency login protocol, mandatory PIN verification for sensitive pages, and a transparency-focused approach to build user trust.

### 1.1 Objectives
- Deliver a secure TOTP-based 2FA solution.
- Split backend functionality into two servers: one for authentication and one for TOTP operations.
- Provide an emergency login system using a user-generated `username.elp` file.
- Require PIN verification to access sensitive pages like the Dashboard.
- Ensure transparency by encoding and securely storing user data (e.g., full names).
- Offer a modern, intuitive frontend with dedicated pages for user interaction and transparency.

## 2. Core Features
### 2.1 No Third Party TOTP Generation
- The system generates TOTP codes using a proprietary algorithm based on HMAC-SHA-256 and a time-based counter (30-second intervals).
- Codes are generated server-side and never stored, ensuring maximum security.
- Users receive a unique secret key during registration, used to generate and validate TOTP codes.

### 2.2 Dual-Backend Architecture
- **Authentication Server**: Handles user registration, credential-based login, emergency login via `username.elp`.
- **TOTP Server**: Manages TOTP code generation, PIN verification and validation, operating independently for enhanced security.

### 2.3 Emergency Login Protocol
- After registration, users generate and download a unique `username.elp` file containing an encrypted emergency key.
- The `username.elp` file enables emergency login if users lose access to their credentials or TOTP codes.
- The file is can not be renamed or edited, for security.

### 2.4 PIN Verification
- Users must enter a PIN to access sensitive pages (e.g., Dashboard for viewing TOTP codes).
- The PIN is set after registration and stored securely with encryption.

### 2.5 Transparency
- User data, such as full names, email, password, PIN etc. is Base64-encoded and encrypted (AES-256) before storage.
- A dedicated Transparency page displays encoded user data and anonymized system logs to foster trust.

## 3. Frontend Pages
The frontend provides a user-friendly, responsive interface with the following pages:
- **Index**: Landing page with an overview of the application and navigation links.
- **Dashboard**: Displays TOTP codes after successful PIN verification.
- **Profile**: Shows encoded user data (e.g., full name) and allows PIN updates.
- **ELP Generate**: Interface for generating and downloading the `username.elp` file during registration.
- **ELP Login**: Form for uploading the `username.elp` file for emergency login.
- **Normal Login**: Standard username/password login interface.
- **Register**: Form for creating an account with username, password, full name, and PIN.
- **Contact Us**: Form for users to submit inquiries or feedback.
- **Transparency**: Displays encoded user data and system logs for accountability.

## 4. System Architecture Overview
- **Backend**:
  - **Authentication Server**: Manages user authentication, emergency login, and PIN verification.
  - **TOTP Server**: Handles custom TOTP code generation and validation.
  - Both servers use Spring Framework for robust, secure backend operations.
- **Frontend**: Built with ReactJS and styled with Tailwind CSS for a modern, responsive user experience.
- **Communication**: Secured via HTTPS with JWT-based authentication for all API interactions.
- **Data Storage**: Separate databases for authentication (user data, PINs) and TOTP (secrets), with all sensitive data encrypted.

## 5. Security Measures
- **In Built TOTP Algorithm**: Uses HMAC-SHA-256 for secure, server-side code generation.
- **Emergency Login**: The `username.elp` file is encrypted and downloadable only once.
- **PIN Verification**: Mandatory for sensitive pages, stored with AES-256 encryption.
- **Data Encoding**: Full names, email, password and other sensitive data are Base64-encoded and AES-256 encrypted.
- **API Security**: All endpoints are protected with JWT tokens.
- **Rate Limiting**: Applied to login and TOTP validation to prevent brute-force attacks.

## 6. User Workflow
1. **Registration**:
   - Users provide a username, password, full name, and PIN.
   - or Register by OAuth i.e. Google
2. **Normal Login**:
   - Users log in with username and password.
   - or login by OAuth i.e. Google
   - After login, they access the Dashboard by entering their PIN to view TOTP codes.
3. **Emergency Login**:
   - Users upload their `username.elp` file to regain access if credentials or TOTP are unavailable.
4. **TOTP Usage**:
   - User provides secret key from their authentication provider
   - The TOTP Server generates a 6-digit code every 30 seconds, displayed on the Dashboard after PIN verification.
   - Users enter the code to validate their identity.
6. **Transparency**:
   - Users can view their encoded data and system logs on the Transparency page.

## 7. Team Guidance
- **Backend Team**: Focus on building the Authentication and TOTP servers with the in Built TOTP algorithm. Ensure secure data handling and API protection. Validate encryption, JWT implementation, and rate-limiting measures.
- **Frontend Team**: Develop responsive, user-friendly pages with a focus on PIN verification and file upload functionality.
- **QA Team**: Test all user flows, including registration, login, emergency login, and TOTP validation.

## 8. Future Enhancements
- Add support for backup codes for users who lose their `username.elp` file.
- Implement multi-language support for the frontend.
- Introduce push notifications for real-time alerts.

## 9. Contact
For questions or clarification, reach out to the project lead at `work.manish02@yahoo.com`.
