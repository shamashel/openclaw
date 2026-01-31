---
name: qrcode
description: Generate QR codes for URLs, WiFi networks, contact cards, and plain text using qrencode. Use when the user wants to create a QR code to share information from terminal to phone, generate WiFi connection codes, or create scannable links.
metadata: {"openclaw":{"emoji":"🔳","requires":{"bins":["qrencode"]},"install":[{"id":"brew","kind":"brew","formula":"qrencode","bins":["qrencode"],"label":"Install qrencode (brew)"},{"id":"apt","kind":"apt","package":"qrencode","bins":["qrencode"],"label":"Install qrencode (apt)"}]}}
---

# QR Code Generator

Generate QR codes for easy sharing from terminal to mobile devices.

## Quick Start

Generate a QR code and display in terminal:
```bash
qrencode -t ANSIUTF8 "https://example.com"
```

Save as PNG:
```bash
qrencode -o ~/Downloads/qr-link.png "https://example.com"
```

## Common Use Cases

### Share a URL
```bash
qrencode -t ANSIUTF8 "https://github.com/openclaw/openclaw"
```

### WiFi Network (auto-connect on scan)
Format: `WIFI:T:WPA;S:<SSID>;P:<PASSWORD>;;`
```bash
qrencode -t ANSIUTF8 "WIFI:T:WPA;S:MyNetwork;P:MyPassword;;"
```

WiFi QR codes work on both iOS and Android - scanning opens the WiFi settings with the network pre-filled.

### Contact Card (vCard)
```bash
qrencode -t ANSIUTF8 "BEGIN:VCARD
VERSION:3.0
FN:John Doe
TEL:+1234567890
EMAIL:john@example.com
END:VCARD"
```

### Email (pre-filled message)
```bash
qrencode -t ANSIUTF8 "mailto:someone@example.com?subject=Hello&body=Message"
```

### Plain Text
```bash
qrencode -t ANSIUTF8 "Any text content here"
```

## Output Formats

- `-t ANSIUTF8` - Display in terminal (UTF-8 blocks)
- `-t ANSI` - Display in terminal (ASCII)
- `-o file.png` - Save as PNG image
- `-t SVG` - Output as SVG (redirect to file)
```bash
qrencode -t SVG -o ~/Downloads/qr.svg "https://example.com"
```

## Error Correction Levels

Increase redundancy for better scanning (useful for logos or damage resistance):
```bash
qrencode -l H -t ANSIUTF8 "important data"  # High correction
```

Levels: `L` (low, ~7%), `M` (medium, ~15%), `Q` (quartile, ~25%), `H` (high, ~30%)

## Size Control

Specify module size in pixels (for PNG output):
```bash
qrencode -s 10 -o ~/Downloads/qr-large.png "https://example.com"
```

## Margin

Adjust quiet zone around QR code:
```bash
qrencode -m 2 -t ANSIUTF8 "text"  # 2 modules margin (default is 4)
```

## Tips

- Terminal display (`-t ANSIUTF8`) works best in modern terminals (iTerm2, Kitty, Ghostty, Windows Terminal)
- For dark terminals, QR codes are readable as-is; light terminals may need `-t ANSI` or image output
- WiFi QR codes: Remove `P:password;;` for open networks
- Large text content may require higher error correction (`-l H`) to scan reliably
