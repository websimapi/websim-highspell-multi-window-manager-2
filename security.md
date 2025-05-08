# Security Considerations for Highspell Multi-Window Manager

## Overview
This document outlines the security aspects of the Highspell Multi-Window Manager application, focusing on user data safety and login security.

## Iframe Security Analysis

### Cross-Origin Isolation
- The application loads external content (highspell.com) in iframes
- **Same-Origin Policy Protection**: Browsers enforce the Same-Origin Policy which prevents the parent window from accessing content inside cross-origin iframes
- **Data Isolation**: Each iframe maintains its own security context, cookies, and session information

### Login Security
- **Credentials Safety**: Login credentials entered in the iframes are processed directly by the target website (highspell.com)
- **No Credential Interception**: The parent window cannot access or intercept credentials entered in cross-origin iframes
- **Session Independence**: Each iframe maintains its own independent session with the target website

## Data Storage Security

### PIN Protection
- User data is protected with a 4-digit PIN
- PIN is hashed using SHA-256 before storage (one-way encryption)
- Stored data is encrypted using AES encryption with the PIN as the key
- Without the correct PIN, saved data cannot be decrypted

### Local Storage Considerations
- Data is stored in the browser's localStorage
- **Encryption**: All sensitive data is encrypted before storage
- **Storage Isolation**: The localStorage is bound to the domain of this application, not accessible by the loaded websites

## Communication Model

### PostMessage Security
- The application uses the postMessage API for potential communication with iframes
- In the current implementation, meaningful two-way communication is limited due to cross-origin restrictions
- Mock data is used for demonstration since cross-origin iframe content cannot be accessed directly

## Security Limitations

### Known Considerations
- PIN complexity is limited to 4 digits (10,000 possible combinations)
- Data remains in localStorage until manually cleared
- If a malicious actor gains physical access to the user's device, localStorage data could potentially be compromised

## Recommendations for Users

1. Use unique PINs for each window storing sensitive information
2. Clear browser data after using public or shared computers
3. Be aware that the application does not control the security of the loaded website itself
4. Consider using the browser's built-in password manager for additional security
5. Verify the URL shown in the iframes before entering sensitive information

## Conclusion

The current implementation provides a reasonable level of security for users logging into applications within the iframes. The Same-Origin Policy ensures that credentials and session data within iframes remain protected from the parent window. Local data storage is secured through encryption, though users should be mindful of physical device security.

