# Deployment Guide - Revenue Analytics Dashboard

## 🚀 Quick Deploy to Streamlit Cloud

### Prerequisites
- GitHub account
- OpenAI API key from [platform.openai.com](https://platform.openai.com/api-keys)
- This repository pushed to your GitHub account

### Step 1: Prepare Your Repository
1. **Fork or clone this repository** to your GitHub account
2. **Verify security**: Ensure `.env` and `.streamlit/secrets.toml` are in `.gitignore` ✅
3. **Push your code** to GitHub (API keys will NOT be included - this is secure)

### Step 2: Deploy to Streamlit Cloud
1. **Visit [share.streamlit.io](https://share.streamlit.io)**
2. **Sign in** with your GitHub account
3. **Click "New app"**
4. **Select your repository** and `main` branch
5. **Set Main file path**: `app.py`
6. **Click "Deploy"** (app will fail initially - this is expected)

### Step 3: Configure API Key (Critical Step)
1. **Go to your app settings** on Streamlit Cloud
2. **Click "Secrets"** in the left sidebar
3. **Add your API key**:
   ```toml
   OPENAI_API_KEY = "your_actual_api_key_here"
   ```
4. **Save the secrets** - app will automatically restart

### Step 4: Configure Private Access
1. **In app settings**, go to "Sharing"
2. **Set visibility to "Private"** 
3. **Share the URL** only with authorized users
4. **Users access via**: `https://yourapp.streamlit.app`

## 🔒 Security Features

### ✅ What's Secure
- API keys never committed to Git
- Local `.env` and `.streamlit/secrets.toml` are git-ignored
- Streamlit Cloud secrets are encrypted
- Private deployment with controlled URL access

### ⚠️ Important Notes
- **Never commit API keys** to version control
- **Share app URL carefully** - anyone with URL can access
- **Monitor API usage** in OpenAI dashboard
- **Rotate API keys** periodically for security

## 🛠️ Local Development

### Setup
```bash
# Clone repository
git clone <your-repo-url>
cd streamlit_json_new_with_upload_button_2

# Install dependencies
pip install -r requirements.txt

# Configure API key (choose one method)
```

### Method 1: Using .env file
```bash
# Edit .env file (already exists)
OPENAI_API_KEY=your_actual_api_key_here
```

### Method 2: Using Streamlit secrets
```bash
# Edit .streamlit/secrets.toml (already exists)
OPENAI_API_KEY = "your_actual_api_key_here"
```

### Run locally
```bash
streamlit run app.py
```

## 🌐 Alternative Deployment Options

### Option A: Heroku (More Control)
1. Create `Procfile`:
   ```
   web: streamlit run app.py --server.port=$PORT --server.address=0.0.0.0
   ```
2. Set environment variable in Heroku dashboard
3. Deploy with custom domain if needed

### Option B: DigitalOcean/VPS (Full Control)
1. Set up server with Docker
2. Configure nginx reverse proxy
3. Use environment variables for API key
4. Implement custom authentication if needed

## 📊 Usage & Monitoring

### API Key Management
- **All users share your API key** (centralized billing)
- **Monitor usage** at [platform.openai.com/usage](https://platform.openai.com/usage)
- **Set usage limits** to prevent unexpected charges
- **Consider GPT-4 vs GPT-3.5** for cost optimization

### User Access Control
- **Streamlit Cloud**: Share URL with authorized users
- **Custom domain**: Point CNAME to Streamlit Cloud URL
- **Analytics**: Monitor usage via Streamlit Cloud dashboard

## 🆘 Troubleshooting

### Common Issues

**"OpenAI API key not configured"**
- Check secrets.toml format in Streamlit Cloud
- Ensure no extra spaces or quotes issues
- Verify API key is valid and has credits

**App won't start**
- Check requirements.txt for missing dependencies
- Verify Python version compatibility
- Check Streamlit Cloud logs for detailed errors

**Authentication errors**
- Verify API key permissions in OpenAI dashboard
- Check if API key has sufficient credits
- Ensure key hasn't been rotated/expired

### Support
- Check Streamlit Cloud documentation
- Monitor OpenAI API status
- Review app logs in Streamlit Cloud dashboard

## 📋 Deployment Checklist

- [ ] Repository pushed to GitHub without API keys
- [ ] Streamlit Cloud app created and connected
- [ ] API key configured in Streamlit Cloud secrets
- [ ] App visibility set to private
- [ ] URL shared with authorized users only
- [ ] API usage monitoring set up
- [ ] Local development environment tested

---

**⚡ Your app will be live at: `https://yourapp.streamlit.app`**

All GPT-4 summaries and chatbot features will use your centralized API key. Users can access the full dashboard without needing their own OpenAI accounts.