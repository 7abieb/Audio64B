
# Audio Encryption Tool (Base64)

[![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white)](https://html5.org/)
[![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=for-the-badge)](https://opensource.org/licenses/MIT)
[![Made with ❤️ by Oak AI](https://img.shields.io/badge/Made%20with-%E2%9D%A4%EF%B8%8F-brightgreen?style=for-the-badge)](https://oak.ai/)

A modern, client-side web tool for encrypting audio files (like MP3, M4A, WAV) into secure Base64 strings using AES-256-GCM encryption. You can easily share the Base64 code (e.g., via text messages or files) and decrypt it back to a playable audio file with a password. No servers involved—everything runs in your browser!

Built with HTML, CSS, and JavaScript, featuring a responsive UI with icons from Font Awesome.

## Features

- Secure Encryption: Uses the browser's Web Crypto API for AES-256-GCM symmetric encryption with PBKDF2 key derivation (100,000 iterations for strong password hashing).
- Base64 Output: Encrypts binary audio data into a copy-paste-friendly Base64 string. Share it anywhere as text!
- Easy Decryption: Paste the Base64 string and password to restore the original audio file.
- Modern UI: Clean, gradient-based design with hover effects, icons, and responsive layout (works on desktop, tablet, and mobile).
- User-Friendly Tools: Copy to clipboard, download Base64 as TXT, and direct audio downloads.
- Format Support: Handles common audio formats (MP3, M4A, WAV, OGG, etc.) as binary blobs.
- Offline & Private: 100% client-side—no data leaves your device. Works offline after loading.

## Quick Start

1. Download/Clone the Repo:

                            Copy
Download

                            git clone https://github.com/yourusername/audio-encryption-tool.git
   cd audio-encryption-tool
                        


2. Open in Browser:
- Save `index.html` (the main file) and open it in a modern browser (Chrome, Firefox, Edge, Safari).
- No installation needed! Just double-click the HTML file.

## Usage

### Encrypt Audio to Base64
1. Click "Select Audio File" and choose your audio (e.g., MP3 or M4A).
2. Enter a strong password in the input field.
3. Click "Encrypt to Base64".
4. The encrypted Base64 string appears in the textarea:
- Copy it: Click "Copy Base64 to Clipboard" to paste into emails, notes, or code.
- Download it: Click "Download Base64 as TXT" to save as a file.
5. Share the Base64 string securely (it's password-protected).

### Decrypt Base64 to Audio
1. Paste the Base64 string into the large textarea.
2. Enter the exact same password.
3. Click "Decrypt to Audio".
4. If successful, click "Download Decrypted Audio" to get the original file (e.g., `decrypted_audio.mp3`).
5. Play the file in any media player (VLC, browser, etc.). Rename the extension if needed (e.g., to `.m4a`).

Example Workflow:
- Encrypt a 5MB MP3 → Get a ~7MB Base64 string (due to encoding overhead).
- Share the string → Recipient pastes it and decrypts → Original MP3 restored.

Status Messages: Green for success, red for errors (e.g., wrong password or invalid Base64).

## Screenshots

### Encryption Section
![Encryption UI](screenshots/encryption.png)
*(Select file → Enter password → Get Base64 output with copy/download options)*

### Decryption Section
![Decryption UI](screenshots/decryption.png)
*(Paste Base64 → Enter password → Download audio)*

*(Add actual screenshots to a `screenshots/` folder in your repo for better visuals.)*

## Technical Details

- Encryption Process:
1. Generate random salt (16 bytes) and IV (12 bytes).
2. Derive a 256-bit AES key from the password using PBKDF2 (SHA-256, 100k iterations).
3. Encrypt the audio file bytes with AES-GCM.
4. Combine: salt + IV + encrypted data.
5. Encode the combined bytes as Base64.

- Decryption Process:
1. Decode Base64 to bytes.
2. Extract salt, IV, and encrypted data.
3. Derive the same key from password + salt.
4. Decrypt with AES-GCM.
5. Output as an audio Blob (MIME type: `audio/mpeg` for broad compatibility).

- Dependencies:
- Font Awesome (CDN for icons).
- Native browser APIs: Web Crypto, Blob, URL.createObjectURL, Clipboard API.

- Browser Support: Modern browsers (Chrome 37+, Firefox 34+, Safari 7.1+, Edge 12+). Requires HTTPS for Web Crypto in some cases (use `localhost` for local testing).

- File Size: Base64 adds ~33% overhead. Browser memory limits apply (test with files <50MB).

## Limitations

- File Size: Large files (>100MB) may cause browser slowdown or crashes due to memory constraints.
- No Metadata Preservation: Original filename and exact MIME type aren't stored (decrypted files default to `.mp3` extension; rename if needed).
- Password Security: Use strong, unique passwords. No password recovery—wrong password = failed decryption.
- Browser-Only: Not a native app; won't work in outdated browsers or without JavaScript enabled.
- No Streaming: Full file must load into memory for encryption/decryption.
- Validation: Basic Base64 checks; invalid input may show errors like "Invalid Base64 format" or "Invalid encrypted file".

## Security Notes

- This tool provides strong, standards-compliant encryption but is not a replacement for professional tools (e.g., for enterprise use).
- Always use a secure password (at least 12 characters, mix of types).
- The Base64 string itself isn't encrypted—protect it like any sensitive data.
- Client-side means your device handles everything, but ensure your browser is up-to-date.
- For audits: Review the JavaScript code—it's transparent and uses audited browser APIs.

## Contributing

Contributions are welcome! Fork the repo, make changes, and submit a pull request. Ideas for improvements:
- Add file metadata storage (e.g., original name/type).
- Support multi-file batch processing.
- Integrate with local storage for saving sessions.

Report issues or feature requests in the [Issues](https://github.com/yourusername/audio-encryption-tool/issues) tab.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Acknowledgments

- Built with inspiration from modern web security practices.
- Icons: [Font Awesome](https://fontawesome.com/).
- Thanks to Oak AI for the initial development assistance.
