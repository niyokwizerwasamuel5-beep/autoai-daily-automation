# 🔧 Complete Setup Guide

Step-by-step instructions to get AutoAI Daily fully operational.

## Table of Contents
1. [Account Creation](#account-creation)
2. [API Setup](#api-setup)
3. [Credential Configuration](#credential-configuration)
4. [Workflow Deployment](#workflow-deployment)
5. [Testing & Validation](#testing--validation)
6. [Troubleshooting](#troubleshooting)

---

## Account Creation

### Step 1: Create Accounts (if needed)

| Service | URL | Purpose | Free Tier |
|---------|-----|---------|-----------|
| OpenAI | https://platform.openai.com | AI script generation | $5 credits |
| ElevenLabs | https://elevenlabs.io | Voice generation | 10k chars/month |
| YouTube | https://youtube.com/create | Video hosting | Unlimited |
| Pictory AI | https://pictory.ai | Video creation | 3 videos/month |
| Make (formerly Integromat) | https://make.com | Workflow automation | 1000 ops/month |
| Google Cloud | https://console.cloud.google.com | Sheets & YouTube APIs | Free tier |

### Step 2: Verify Accounts
- Check email confirmations
- Enable 2FA on all accounts
- Note down usernames/IDs

---

## API Setup

### OpenAI API Configuration

**Location:** https://platform.openai.com/api-keys

**Steps:**
```
1. Click "Create new secret key"
2. Copy the key immediately (you won't see it again)
3. Store in secure location (password manager recommended)
4. Do NOT commit to git or share publicly

Format: sk-proj-xxxxxxxxxxxxxxxxxxxxxxxx
```

**Billing Setup:**
```
1. Go to Settings > Billing > Overview
2. Set usage limits to prevent overspending
   - Hard limit: $10/month recommended
   - Soft limit: $8/month for alerts
3. Add payment method
4. Check credit balance
```

**Model Access:**
```
1. Navigate to Settings > Organization settings
2. Confirm access to gpt-4-turbo-preview
3. Request access if needed (instant for most accounts)
```

---

### ElevenLabs Voice Setup

**Location:** https://elevenlabs.io

**Steps:**
```
1. Create account and verify email
2. Navigate to Voice Library (https://elevenlabs.io/voice-library)
3. Browse available voices:
   - Premium voices (best quality)
   - Standard voices (good quality, free)
4. Select voice and click to copy Voice ID
5. Store Voice ID: {format: alphanumeric, 24 chars}
```

**API Key Generation:**
```
1. Click Profile icon (top right)
2. Select "Account"
3. Scroll to "API Key"
4. Copy and store securely
5. Never share or commit to version control
```

**Example Voice IDs:**
```
- Rachel (Female, professional): 21m00Tcm4TlvDq8ikWAM
- Clyde (Male, friendly): 2EiwWnXFnvU5JabPgLCL
- Domi (Female, energetic): AmXWAOrPvzv9sQjq5b3c
```

---

### YouTube API Configuration

**Location:** https://console.cloud.google.com

**Step 1: Create Project**
```
1. Go to https://console.cloud.google.com
2. Click "Select a Project" > "New Project"
3. Name: "AutoAI Daily"
4. Create project (wait 30-60 seconds)
```

**Step 2: Enable APIs**
```
1. Search for "YouTube Data API v3"
2. Click "Enable"
3. Search for "Google Sheets API"
4. Click "Enable"
```

**Step 3: Create Credentials (OAuth 2.0)**
```
1. Go to APIs & Services > Credentials
2. Click "Create Credentials" > "OAuth client ID"
3. Select "Desktop application"
4. Fill form:
   - Name: "AutoAI Daily"
   - Authorized redirect URIs: http://localhost:8080
5. Click Create
6. Click Download JSON (store in safe location)
```

**Step 4: Get Channel ID**
```
1. Go to https://www.youtube.com/account
2. Look for "Channel ID"
3. Copy and store (format: UC... alphanumeric ~24 chars)
```

---

### Google Sheets Configuration

**Step 1: Create Spreadsheet**
```
1. Go to https://sheets.google.com
2. Create new spreadsheet: "AutoAI Tutorial Queue"
3. Set up columns:
   - Column A: Tool Name
   - Column B: Category
   - Column C: Features
   - Column D: Affiliate Link
```

**Step 2: Add Sample Data**
```
Row 1: Headers
Row 2: ChatGPT | Chatbot | Natural language processing | https://openai.com/?ref=autoai
Row 3: Midjourney | Image Gen | AI image creation | https://midjourney.com/?ref=autoai
Row 4: Pictory | Video | Automated video production | https://pictory.ai/?ref=autoai
```

**Step 3: Get Spreadsheet ID**
```
1. Open the spreadsheet
2. URL format: https://docs.google.com/spreadsheets/d/{ID}/edit
3. Copy the ID section (between /d/ and /edit)
4. Store for later configuration
```

**Step 4: Share with Service Account**
```
1. Download OAuth JSON credentials (see YouTube API step)
2. Extract service account email from JSON
3. Open spreadsheet
4. Click Share > Paste service account email
5. Grant Editor access
6. Save
```

---

### Pictory AI Setup

**Location:** https://pictory.ai

**Steps:**
```
1. Create account at https://pictory.ai/signup
2. Verify email address
3. Click Settings (gear icon, top right)
4. Scroll to "API Key"
5. Click "Generate API Key"
6. Copy and store securely
7. Verify "Tech News" template exists in Templates section
```

**Template Verification:**
```
1. Go to Templates
2. Search for "tech-news"
3. Verify template includes:
   - Title overlay
   - Stock footage integration
   - Subtitle/caption support
   - Audio sync capability
```

---

## Credential Configuration

### Step 1: Create .env File

**Location:** Root of your automation project

**Content:**
```bash
# ============================================
# AUTOAI DAILY - ENVIRONMENT CONFIGURATION
# ============================================

# OpenAI Configuration
OPENAI_API_KEY=sk-proj-your-actual-key-here
OPENAI_MODEL=gpt-4-turbo-preview

# ElevenLabs Configuration
ELEVENLABS_API_KEY=your-elevenlabs-key-here
ELEVENLABS_VOICE_ID=21m00Tcm4TlvDq8ikWAM

# YouTube Configuration
YOUTUBE_API_KEY=AIzaSyD-your-actual-key-here
YOUTUBE_CHANNEL_ID=UCrdp9Tbtvwhy_vLvpwusrYA
YOUTUBE_OAUTH_CREDENTIALS=/path/to/credentials.json

# Google Sheets Configuration
GOOGLE_SHEETS_ID=1A2B3C4D5E6F7G8H9I0J
GOOGLE_SHEETS_SHEET_NAME=Tools

# Pictory Configuration
PICTORY_API_KEY=your-pictory-key-here
PICTORY_TEMPLATE=tech-news

# RSS Configuration (no key needed, public feed)
RSS_FEED_URL=https://techcrunch.com/tag/artificial-intelligence/feed
RSS_LIMIT=3

# Schedule Configuration
SCHEDULE_HOUR=8
SCHEDULE_MINUTE=0
SCHEDULE_DAYS=monday,tuesday,wednesday,thursday,friday,saturday,sunday

# Execution Settings
MAX_TOKENS=800
TEMPERATURE=0.7
LOG_LEVEL=info
DRY_RUN=false
```

### Step 2: Secure Your .env

**CRITICAL: NEVER commit .env to Git**

```bash
# Add to .gitignore
echo ".env" >> .gitignore
echo ".env.local" >> .gitignore
echo "credentials.json" >> .gitignore

# Verify it's ignored
git status
```

### Step 3: Validate Credentials

```bash
# Test OpenAI connection
npm run test:openai

# Test ElevenLabs connection
npm run test:elevenlabs

# Test YouTube connection
npm run test:youtube

# Test Google Sheets connection
npm run test:sheets

# Test RSS feed
npm run test:rss

# Test all
npm run test:all
```

---

## Workflow Deployment

### Option 1: Make.com Deployment

**Step 1: Create Make Scenario**
```
1. Log in to https://make.com
2. Click "Create a new scenario"
3. Select "Start from blank"
4. Name: "AutoAI Daily News"
5. Click Create
```

**Step 2: Add Trigger**
```
1. Click the + to add first module
2. Search "Schedule"
3. Select "When" (Schedule trigger)
4. Set:
   - Interval: Daily
   - Time: 08:00
   - Timezone: UTC
5. Click OK
```

**Step 3: Add RSS Module**
```
1. Click + to add next module
2. Search "RSS"
3. Select "Read a feed"
4. Connection: Create new (none needed for public feed)
5. Feed URL: https://techcrunch.com/tag/artificial-intelligence/feed
6. Maximum items: 3
7. Click OK
```

**Step 4: Add OpenAI Module**
```
1. Click + for next module
2. Search "OpenAI"
3. Select "Create a completion"
4. Connection: Create new > add API key from .env
5. Model: gpt-4-turbo-preview
6. Prompt: "Create a 3-minute YouTube script from these news items: {{1.items}}. Format: [HOOK] [STORY1] [STORY2] [STORY3] [OUTRO]"
7. Max tokens: 800
8. Temperature: 0.7
9. Click OK
```

**Step 5: Add ElevenLabs Module**
```
1. Click + for next module
2. Search "ElevenLabs"
3. Select "Generate audio"
4. Connection: Create new > add API key from .env
5. Voice ID: {{env.ELEVENLABS_VOICE_ID}}
6. Text: {{2.choices[0].text}}
7. Stability: 0.75
8. Similarity boost: 0.85
9. Click OK
```

**Step 6: Add Pictory Module**
```
1. Click + for next module
2. Search "Pictory"
3. Select "Create video"
4. Connection: Create new > add API key from .env
5. Script: {{2.choices[0].text}}
6. Audio URL: {{3.audioUrl}}
7. Template: tech-news
8. Stock footage: technology,ai,robots,future
9. Click OK
```

**Step 7: Add YouTube Upload**
```
1. Click + for final module
2. Search "YouTube"
3. Select "Upload a video"
4. Connection: Create new > authorize YouTube account
5. Channel ID: {{env.YOUTUBE_CHANNEL_ID}}
6. Title: "AI News: {{1.items[0].title}} - {{NOW('MMM D, YYYY')}}"
7. Description: "Today's top AI stories:\n\n{{#each 1.items}}• {{this.title}}: {{this.link}}\n{{/each}}\n\n🚀 Try these AI tools:\n→ ChatGPT: https://openai.com/?ref=autoai\n→ Midjourney: https://midjourney.com/?ref=autoai\n→ Pictory: https://pictory.ai/?ref=autoai\n→ ElevenLabs: https://elevenlabs.io/?ref=autoai\n\n#AINews #ArtificialIntelligence #TechNews"
8. Tags: AI,news,technology,artificial intelligence,machine learning
9. Privacy: Public
10. Click OK
```

**Step 8: Test & Deploy**
```
1. Click "Run once" to test
2. Check logs for errors
3. Once successful, click "Turn on" to enable
4. Schedule is now active
```

---

### Option 2: Local Node.js Deployment

**Step 1: Install Dependencies**
```bash
npm install
```

**Step 2: Configure Environment**
```bash
# Copy template
cp .env.example .env

# Edit with your values
nano .env
```

**Step 3: Run Locally**
```bash
# One-time run
npm run execute

# Watch mode (run every day at 8 AM)
npm run watch
```

**Step 4: Deploy to Server**
```bash
# Option A: PM2 (Node process manager)
npm install -g pm2
pm2 start npm --name "autoai-daily" -- start
pm2 save
pm2 startup

# Option B: Docker
docker build -t autoai-daily .
docker run -d --env-file .env --name autoai autoai-daily

# Option C: Cloud Function
gcloud functions deploy autoai-daily --trigger-topic daily-schedule --runtime nodejs18
```

---

## Testing & Validation

### Test 1: Credential Validation

```bash
npm run validate:credentials
```

**Expected Output:**
```
✅ OpenAI API: Connected
✅ ElevenLabs API: Connected
✅ YouTube API: Connected (Channel: Your Channel)
✅ Google Sheets API: Connected (Accessible sheets: 1)
✅ RSS Feed: Connected (Items found: 42)
✅ Pictory API: Connected
```

### Test 2: Dry Run

```bash
npm run test:dry-run
```

**Expected Output:**
```
[DRY RUN] RSS would fetch 3 items
[DRY RUN] OpenAI would generate 823 tokens
[DRY RUN] ElevenLabs would generate audio
[DRY RUN] Pictory would create video
[DRY RUN] YouTube would upload video
No actual calls made. Execution would take ~8 minutes.
```

### Test 3: Full Execution

```bash
npm run execute
```

**Expected Output:**
```
[2026-03-09 14:30:45] Starting AutoAI Daily execution...
[2026-03-09 14:30:50] RSS: Fetched 3 news items
[2026-03-09 14:31:15] OpenAI: Generated 758-token script
[2026-03-09 14:31:45] ElevenLabs: Generated audio (180 seconds)
[2026-03-09 14:35:30] Pictory: Created video (1280x720, 187 seconds)
[2026-03-09 14:36:15] YouTube: Uploaded video (https://youtube.com/watch?v=ABC123)
[2026-03-09 14:36:15] ✅ COMPLETED: AI News: ChatGPT Update - Mar 09, 2026
```

### Test 4: Error Handling

```bash
npm run test:errors
```

Tests various failure scenarios:
- Invalid API keys
- Network timeouts
- Malformed responses
- Rate limiting
- Quota exceeded

---

## Troubleshooting

### Common Issues

#### Issue: "401 Unauthorized - Invalid API Key"

**Solution:**
```
1. Verify key is copied completely (no extra spaces)
2. Check key hasn't been regenerated
3. Confirm key has proper permissions
4. Test key directly: curl -H "Authorization: Bearer YOUR_KEY" https://api.example.com/test
5. Regenerate key if still failing
```

#### Issue: "429 Too Many Requests"

**Solution:**
```
1. Add delay between API calls (2-3 seconds)
2. Check for concurrent executions
3. Verify API quotas not exceeded
4. Set up exponential backoff in code
5. Contact service provider about rate limits
```

#### Issue: "Feed URL returns 403 Forbidden"

**Solution:**
```
1. Verify URL is accessible in browser
2. Add User-Agent header to request
3. Try alternative RSS feed
4. Check if feed requires authentication
5. Use RSS proxy service if blocked
```

#### Issue: "YouTube upload fails with quota exceeded"

**Solution:**
```
1. Check YouTube channel quotas (https://console.cloud.google.com/apis/dashboard)
2. Verify account has no content restrictions
3. Wait 24 hours for quota reset
4. Request quota increase from Google
5. Stagger uploads (every other day instead of daily)
```

#### Issue: "Script generation times out"

**Solution:**
```
1. Reduce maxTokens from 800 to 600
2. Simplify prompt (fewer instructions)
3. Increase timeout threshold
4. Use faster model: gpt-3.5-turbo
5. Check OpenAI service status
```

---

## Next Steps

✅ Complete all setup steps above
✅ Run validation tests
✅ Execute first test run
✅ Deploy to production
✅ Monitor first week of executions
✅ Adjust settings based on results
✅ Enable notifications for errors

**You're ready to automate! 🚀**