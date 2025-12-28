The error is a CORS (Cross-Origin Resource Security) issue. Your n8n webhook doesn't allow requests from your GitHub Pages domain. Here are solutions:

**Option 1: Fix n8n CORS Settings (Recommended)**
Configure your n8n webhook to allow CORS:
1. In n8n, edit your webhook workflow
2. Add a "Respond to Webhook" node or configure the webhook node
3. Add these headers:
   - `Access-Control-Allow-Origin`: `*` (or specifically `https://rifaterdemsahin.github.io`)
   - `Access-Control-Allow-Methods`: `POST, OPTIONS`
   - `Access-Control-Allow-Headers`: `Content-Type`

**Option 2: Use a Simple GET Request (Quick Fix)**
Let me create a version that uses GET requests instead, which might bypass the CORS preflight:I've updated the code to use GET requests with `no-cors` mode, which should bypass the CORS issue. However, note that with `no-cors` mode, you won't be able to verify the actual response status (it will always show success if no network error occurs).

**Best Long-term Solution:**
Configure your n8n webhooks to accept GET requests and/or add CORS headers. In your n8n workflow:
1. Change webhook to accept GET method
2. Or add a "Set Headers" step with:
   ```
   Access-Control-Allow-Origin: *
   Access-Control-Allow-Methods: POST, GET, OPTIONS
   ```

This will allow your page to work properly with full response verification!
