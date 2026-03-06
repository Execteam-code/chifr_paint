# Steganography Tool

**LSB Image Steganography with AES-256 Encryption**  
Hide encrypted text messages inside PNG images. Secure, lossless, undetectable by eye.

## Features
- **LSB Steganography**: Hides data in least significant bits of RGB pixels
- **AES-256-CBC**: Military-grade encryption with PBKDF2 key derivation
- **PNG Support**: Lossless format preserves hidden data
- **Console Interface**: Simple CLI with input validation
- **Cross-platform**: .NET 6+ (Windows/Linux/macOS)

## Installation

```bash
# Create new console project
dotnet new console -n SteganographyTool
cd SteganographyTool

# Replace Program.cs with the code
# Or download pre-built: dotnet publish -c Release -r win-x64 --self-contained
```

**Requirements:**
- .NET 6.0+ SDK
- Windows (System.Drawing.Common) or Linux/macOS (libgdiplus)

## Quick Start

### 1. Hide Text (Encrypt + Embed)
```bash
dotnet run
```
```
1 - Спрятать текст в PNG
input.png: image.png
output.png: secret.png  
Текст: Hello, World!
Пароль: mysecretpassword
✅ Текст зашифрован и спрятан!
```

### 2. Extract Text (Decode + Decrypt)
```
2 - Извлечь и расшифровать
image.png: secret.png
Пароль: mysecretpassword
✅ Hello, World!
```

## How It Works

```
Plain Text → AES-256 Encrypt → Base64 → LSB Embed → PNG
PNG → LSB Extract → Base64 Decode → AES Decrypt → Plain Text
```

1. **Encryption**: AES-256-CBC with random salt/IV, PBKDF2(1000 iterations)
2. **Embedding**: LSB of RGB channels (3 bits/pixel). Visual change: ±1 intensity
3. **Extraction**: Reads LSB until null terminator, auto-stops

## Security
```
Encryption: AES-256-CBC (FIPS-140)
Key Derivation: PBKDF2-SHA1 (1000 iterations)
Salt/IV: 32 bytes random each time
Steganalysis Resistance: Basic LSB (visual/statistical attacks detectable)
```

## Limitations
- **Capacity**: ~0.375 chars per pixel (text only)
- **Format**: PNG only (lossless required)
- **Detection**: Statistical analysis can detect LSB patterns
- **Size**: Large images needed for long messages

## Development Roadmap (7 Commits)
```
1. Init: Console menu
2. LSB hiding (EmbedText)
3. LSB extraction (ExtractText)  
4. Bit reversal fix
5. XOR encryption
6. AES-256 upgrade
7. UI polish + v1.0 release ✓
```

## Building
```bash
dotnet build --configuration Release
dotnet publish -c Release -r <RID> --self-contained
```

**RIDs**: `win-x64`, `linux-x64`, `osx-x64`

## License
MIT License - © 2026

```
SteganographyTool.exe image.png secret.png "My secret message" "password123"
```
