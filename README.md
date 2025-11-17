<h3 align="center">PhantomStego — Ultimate Steganography Tool</h3>

<p align="center">Professional cross-platform GUI tool for hiding and extracting any files inside images**  
Supports strong encryption, multiple steganography methods, auto-detection and zero dependencies hassle.</p>

<div align="center">

![Python](https://img.shields.io/badge/Python-3.8%2B-blue)
![Platform](https://img.shields.io/badge/Platform-Windows%20%7C%20Linux%20%7C%20macOS-green)
![License](https://img.shields.io/badge/License-MIT-yellowgreen)

</div>


## Key Features

| Feature                        | Description                                                                 |
|-------------------------------|-----------------------------------------------------------------------------|
| **EXIF Embedding**            | Hide unlimited data in JPEG EXIF metadata (invisible to most viewers)      |
| **LSB Steganography**         | Classic Least Significant Bit method for PNG/BMP (up to ~25% of image size)|
| **Polyglot Files**            | Universal container with custom magic bytes                                 |
| **PNG Comment Chunk**         | Hide data in official PNG text/comment chunks                               |
| **AES-256 + PBKDF2**          | Military-grade encryption with proper key derivation                       |
| **Multi-Layer Encryption**    | AES → XOR → XOR(reverse key) for extra paranoia                            |
| **Auto-Detection**            | Extract mode automatically tries all methods                               |
| **Polymorphic Markers**       | Random signature to defeat signature-based detection                       |
| **Standalone Encryptor**      | Encrypt/decrypt any file without steganography                              |
| **Zero Install**              | Dependencies auto-installed on first launch                                 |

## Installation

```bash
git clone https://github.com/yourusername/phantomstego.git
cd phantomstego
python phantom_stego.py
```

## How PhantomStego + Delivery Tool Work Together (Full Workflow)

These two tools form a **complete, stealthy payload delivery pipeline**.  
PhantomStego hides any file inside an innocent-looking image.  
Delivery Tool creates a tiny loader that downloads the image, extracts the hidden payload, decrypts (if needed), and executes it — all silently.

### End-to-End Attack Chain

1. **Prepare your payload**  
   Any executable or shellcode (e.g., `beacon.exe`, `meterpreter.dll`, `revshell.exe`).

2. **Hide the payload with PhantomStego**
   - Open **PhantomStego** → ** Hide Payload** tab
   - Payload File → select your `beacon.exe`
   - Output File → `evil.jpg`
   - Method → **EXIF Embedding** or **Polyglot** (both support unlimited size)
   - (Optional) Enable encryption → AES-256 or Multi-Layer + strong password
   - Click **HIDE PAYLOAD**  
     → Result: normal-looking `evil.jpg` with your payload hidden inside

3. **Host the steganographic container**  
   Upload `evil.jpg` to any web server:  
   `https://yourserver.com/evil.jpg`

4. **Generate the loader with Delivery Tool**
   - Open **Delivery Tool** → ** Generate Script** tab
   - Server URL → `https://yourserver.com/evil.jpg`
   - Payload Size → exact size of original payload in bytes (e.g., `512000`)
   - Enable encryption + **same password** (if used in step 2)
   - Payload Type → **Shellcode** (in-memory) or **Executable** (drop & run)
   - Delivery Method → **PowerShell (.ps1)** recommended
   - Evasion → enable **AMSI bypass** (and ETW bypass if needed)
   - Obfuscation Level → **High** or **Medium**
   - Click **GENERATE SCRIPT**  
     → Get tiny loader: `loader.ps1`, `loader.bat`, `update.html`, etc.

5. **Deliver only the tiny loader**  
   Send the victim just the small script (a few KB):  
   - `loader.ps1`  
   - `loader.bat`  
   - `update.html`  
   - or any other format

   When executed:
   → Downloads `evil.jpg`  
   → Extracts hidden payload from the end of the file  
   → Decrypts (if encrypted)  
   → Executes in memory or drops & runs — **completely silent**

### Why This Combo Is Extremely Powerful
- Victim receives only a harmless-looking script/HTML/BAT (a few KB)
- No direct payload transfer — everything hides behind a normal image
- Bypasses most AV/EDR file scans and network monitoring
- Works over HTTP/HTTPS, no special ports needed
- Full encryption + obfuscation + AMSI/ETW bypass

**PhantomStego** = Hide in plain sight  
**Delivery Tool** = Fetch & execute silently  
**Together** = Professional-grade stealth C2 delivery

> For educational and authorized penetration testing only.

Legal Disclaimer
This tool is provided strictly for educational, penetration testing, and authorized research purposes.
The author is not responsible for any misuse or illegal activities.

⚠ Warning: This code is for educational purposes and security testing in controlled environments only. Unauthorized use may be illegal.
Thanks for exploring!
