# Testing Guide - After Setup

## 🧪 Quick Test Checklist

### Test 1: Flask API is Running
```bash
# Open browser or use curl
http://localhost:5000/api/health
```
**Expected:** Response (or 404 if endpoint doesn't exist - that's OK)

### Test 2: ngrok Tunnel is Active
1. Open: http://127.0.0.1:4040
2. **Expected:** See ngrok dashboard with active tunnel

### Test 3: Access Flask via ngrok
```bash
# Replace with your ngrok URL
https://abc123.ngrok.io/api/health
```
**Expected:** Same response as Test 1

### Test 4: Twilio Webhook Test
1. Go to Twilio Console → Phone Numbers
2. Click your number
3. Scroll to bottom → "Test" button
4. **Expected:** Should show webhook response

### Test 5: Full IVR Call Test
1. Login to dashboard
2. Create/select a mother
3. Initiate call
4. **Check:**
   - ✅ ngrok shows POST request to `/api/ivr/webhook`
   - ✅ Flask terminal shows request logs
   - ✅ Twilio console shows call status
   - ✅ Dashboard shows call log entry

## 🔍 What to Look For

### In Flask Terminal:
```
127.0.0.1 - - [DATE] "POST /api/ivr/webhook HTTP/1.1" 200 -
```

### In ngrok Interface:
- Request to `/api/ivr/webhook`
- Status: 200 OK
- Response time

### In Twilio Console:
- Call status: "completed", "no-answer", etc.
- Call duration
- Webhook response

### In Dashboard:
- New call log entry
- Mother flagged (if call failed)
- Updated call status

## ✅ Success = All Tests Pass!



