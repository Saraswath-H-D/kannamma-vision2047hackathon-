# Twilio + Flask Setup Guide

This guide will help you connect Twilio with your Flask backend for IVR calls.

## Step 1: Get Twilio Credentials

1. **Sign up/Login to Twilio**: Go to https://www.twilio.com/
2. **Get your Account SID and Auth Token**:
   - Go to https://console.twilio.com/
   - Your Account SID and Auth Token are on the dashboard
   - **⚠️ Keep these secret - never share them publicly!**

3. **Get a Twilio Phone Number**:
   - Go to Phone Numbers → Manage → Buy a number
   - Choose a number (can be trial number for testing)
   - Copy the phone number (format: +1234567890)

## Step 2: Configure Backend Environment

1. **Create `.env` file** in the `backend/` directory:
   ```bash
   cd backend
   cp .env.example .env
   ```

2. **Edit `.env` file** and add your Twilio credentials:
   ```env
   TWILIO_ACCOUNT_SID=ACxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
   TWILIO_AUTH_TOKEN=your_auth_token_here
   TWILIO_PHONE_NUMBER=+1234567890
   ```

## Step 3: Get HTTPS URL for Webhook

Twilio requires HTTPS URLs for webhooks. You have two options:

### Option A: Local Development (using ngrok)

1. **Install ngrok**: 
   - Download from https://ngrok.com/download
   - Or install via package manager:
     ```bash
     # Windows (chocolatey)
     choco install ngrok
     
     # Mac (homebrew)
     brew install ngrok
     
     # Linux
     wget https://bin.equinox.io/c/bNyj1mQVY4c/ngrok-v3-stable-linux-amd64.tgz
     tar -xzf ngrok-v3-stable-linux-amd64.tgz
     ```

2. **Start your Flask server**:
   ```bash
   cd backend
   python app.py
   ```
   Server should be running on `http://localhost:5000`

3. **Start ngrok** in a new terminal:
   ```bash
   ngrok http 5000
   ```

4. **Copy the HTTPS URL** from ngrok output:
   ```
   Forwarding  https://abc123.ngrok.io -> http://localhost:5000
   ```
   Your URL will be: `https://abc123.ngrok.io`

5. **Update `.env` file**:
   ```env
   IVR_CALLBACK_BASE_URL=https://abc123.ngrok.io
   ```

### Option B: Production (Deployed Server)

If you've deployed your Flask app (e.g., Heroku, AWS, DigitalOcean):

1. Use your production HTTPS URL
2. Update `.env`:
   ```env
   IVR_CALLBACK_BASE_URL=https://your-domain.com
   ```

## Step 4: Configure Twilio Webhook

1. **Go to Twilio Console**: https://console.twilio.com/
2. **Navigate to Phone Numbers**: Phone Numbers → Manage → Active numbers
3. **Click on your phone number**
4. **Scroll to "Voice & Fax" section**
5. **In "A CALL COMES IN" field**, enter:
   ```
   https://your-ngrok-url.ngrok.io/api/ivr/webhook
   ```
   Or for production:
   ```
   https://your-domain.com/api/ivr/webhook
   ```
6. **Set HTTP method**: POST
7. **Click "Save"**

## Step 5: Test the Connection

1. **Restart your Flask server** (to load new .env variables):
   ```bash
   cd backend
   python app.py
   ```

2. **Test via API** (using curl or Postman):
   ```bash
   # First, login to get JWT token
   curl -X POST http://localhost:5000/api/auth/login \
     -H "Content-Type: application/json" \
     -d '{"asha_id":"ASHA001","password":"password123"}'
   
   # Use the access_token from response, then initiate a call
   curl -X POST http://localhost:5000/api/ivr/initiate-call \
     -H "Content-Type: application/json" \
     -H "Authorization: Bearer YOUR_ACCESS_TOKEN" \
     -d '{"mother_id":"mother-id-here","call_type":"reminder"}'
   ```

3. **Check Twilio Console**:
   - Go to Monitor → Logs → Calls
   - You should see call attempts and their status

## Step 6: Verify Webhook is Working

1. **Make a test call** from your dashboard
2. **Check Flask server logs** - you should see webhook requests
3. **Check Twilio logs** - should show call status

## Troubleshooting

### Issue: "Mother not found" error
- **Problem**: Phone number format mismatch
- **Solution**: Ensure phone numbers in database match Twilio format
  - Database should store: `9876543210` (10 digits)
  - Twilio sends: `+919876543210` or `919876543210`
  - The code handles normalization automatically

### Issue: Webhook not receiving requests
- **Problem**: ngrok URL changed or incorrect
- **Solution**: 
  - Free ngrok URLs change on restart
  - Update `.env` and Twilio webhook URL
  - Or use ngrok authtoken for stable URLs: `ngrok config add-authtoken YOUR_TOKEN`

### Issue: "Twilio credentials not configured"
- **Problem**: Environment variables not loaded
- **Solution**: 
  - Ensure `.env` file is in `backend/` directory
  - Restart Flask server
  - Check variable names match exactly

### Issue: CORS errors
- **Problem**: Frontend can't connect to backend
- **Solution**: Update `FRONTEND_URL` in `.env` to match your frontend URL

## Security Notes

⚠️ **Important Security Practices**:

1. **Never commit `.env` file** to git (it's already in .gitignore)
2. **Never share** your Twilio credentials publicly
3. **Use environment variables** in production, not hardcoded values
4. **Rotate credentials** if accidentally exposed
5. **Use HTTPS** in production (required by Twilio)

## Next Steps

Once connected:
- Test IVR calls from the dashboard
- Check call logs in the dashboard
- Monitor Twilio usage and costs
- Customize voice messages in `backend/services/ivr_service.py`

