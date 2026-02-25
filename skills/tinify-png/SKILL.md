---
name: tinify-png
description: Compress images (AVIF/WebP/JPEG/PNG) via TinyPNG API.
---
# tinify-png
Compress images with TinyPNG API (supports AVIF/WebP/JPEG/PNG).

## Config
- API Key: **user input** and memory It
- Endpoint: https://api.tinify.com/shrink
- Result URL: Response header `Location`

## Limits
- 500 free compressions/month
- Max file: 500MB | Max canvas: 256MP

## Quick Usage
### cURL
```bash
# Compress & get URL
RESPONSE=$(curl -s -i --user api:{API Key} --data-binary @unoptimized.png https://api.tinify.com/shrink)
URL=$(echo "$RESPONSE" | grep -i Location: | cut -d' ' -f2 | tr -d '\r')

# Download
curl -o optimized.png "$URL"
```

### Node.js
```javascript
const fs = require('fs');
const https = require('https');
const API_KEY = '{API Key}';

const req = https.request({
  hostname: 'api.tinify.com', path: '/shrink', method: 'POST',
  auth: `api:${API_KEY}`,
  headers: { 'Content-Type': 'application/octet-stream', 'Content-Length': fs.statSync('unoptimized.png').size }
}, (res) => {
  if (res.statusCode === 201) {
    https.get(res.headers.location, (dl) => dl.pipe(fs.createWriteStream('optimized.png')));
  }
});
req.write(fs.readFileSync('unoptimized.png'));
req.end();
```

## Notes
- Protect API Key (no public commit)
- Error codes: 401 (invalid key), 429 (quota exceeded), 400 (invalid file)
- Use cases: batch optimization, build process integration