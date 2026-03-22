# APK Penetration Testing Tool

A comprehensive static analysis tool for Android APK files following the OWASP Mobile Application Security (MAS) standard.

## Features

### 1. Manifest Analysis
- Dangerous permission detection
- Exported components (activities, services, receivers, providers)
- Debuggable flag check
- Backup configuration analysis
- Cleartext traffic detection
- Network security config verification
- Test-only flag detection

### 2. Code Analysis
- Hardcoded secrets detection (API keys, tokens, passwords, AWS credentials)
- Weak cryptographic algorithm identification (DES, RC4, MD5, SHA1)
- Logging statement detection
- URL enumeration (HTTP/HTTPS)

### 3. Architecture Analysis
- Third-party library detection (OkHttp, Retrofit, Apache HttpClient)
- ProGuard/R8 configuration check
- WebView usage analysis

## Requirements

- Python 3.7+
- `apktool` - For APK decompilation
- `jadx` - Optional, for better Java decompilation

### Installation

```bash
# Install apktool (Ubuntu/Debian)
sudo apt-get install apktool

# Or download manually
wget https://github.com/iBotPeaches/Apktool/releases/download/v2.7.0/apktool_2.7.0.jar -O apktool.jar
sudo mv apktool.jar /usr/local/bin/apktool
sudo chmod +x /usr/local/bin/apktool

# Install jadx (optional)
git clone https://github.com/skylot/jadx.git
cd jadx
./gradlew build
./build/install/jadx/bin/jadx -v
```

## Usage

```bash
python apk_pentest.py <apk_file>
```

### Options

- `<apk_file>` - Path to the APK file to analyze (required)

### Example

```bash
python apk_pentest.py target_app.apk
```

## Output

The tool creates:
- `apk_analysis/<app_name>_extracted/` - Extracted APK contents
- Console output with colored findings
- Summary statistics (High/Medium/Low/Info findings count)

## Finding Severity

| Severity | Description |
|----------|-------------|
| **High** | Critical security issues requiring immediate attention |
| **Medium** | Security concerns to be addressed soon |
| **Low** | Minor issues for regular maintenance |
| **Info** | Informational findings for review |

## Security Checks Performed

### Permissions Flagged
- READ_CONTACTS, WRITE_CONTACTS
- READ_SMS, SEND_SMS, RECEIVE_SMS
- READ_CALL_LOG, RECEIVE_CALLS
- CAMERA, RECORD_AUDIO
- ACCESS_FINE_LOCATION, ACCESS_COARSE_LOCATION
- READ_EXTERNAL_STORAGE, WRITE_EXTERNAL_STORAGE
- GET_ACCOUNTS, READ_PHONE_STATE
- And more...

### Secret Patterns Detected
- API Keys
- AWS Access/Secret Keys
- Private Keys (RSA, DSA, EC)
- Google API Keys
- Firebase Keys
- Slack/GitHub Tokens
- Bearer/Basic Auth credentials
- Database connection strings

### Weak Crypto Algorithms
- DES
- RC4/Arc4
- MD5
- SHA-1
- ECB mode
- NoPadding

## License

This tool is provided for security testing purposes only. Always obtain proper authorization before testing any application.

## Disclaimer

This tool performs static analysis and may not detect all vulnerabilities. Manual testing is recommended for comprehensive security assessments.
