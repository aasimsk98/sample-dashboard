# Reddit Sentiment Analytics Dashboard

Real-time sentiment analysis dashboard for Reddit posts and comments, with automatic updates every 5 minutes.

## 🚀 Features

- ✅ Real-time sentiment analysis using VADER and Transformer models
- ✅ Auto-refresh every 5 minutes
- ✅ Interactive filters (subreddit, content type, sentiment)
- ✅ Visual analytics with charts and graphs
- ✅ MongoDB integration for live data

## 📋 Local Development Setup

### 1. Install Dependencies
```bash
pip install -r requirements.txt
```

### 2. Configure MongoDB Credentials

Create a file named `mongo_credentials.txt` in the project root:
```
connection_string=mongodb+srv://username:password@cluster.mongodb.net/
```

### 3. Run the Dashboard
```bash
streamlit run reddit_dashboard_enhanced.py
```

## ☁️ Streamlit Cloud Deployment

### 1. Push to GitHub
```bash
git init
git add .
git commit -m "Initial commit"
git remote add origin https://github.com/yourusername/your-repo.git
git push -u origin main
```

**Important:** Make sure `.gitignore` is configured to exclude `mongo_credentials.txt`!

### 2. Deploy on Streamlit Cloud

1. Go to [share.streamlit.io](https://share.streamlit.io)
2. Click "New app"
3. Select your GitHub repository
4. Choose the main file: `reddit_dashboard_enhanced.py`
5. Click "Advanced settings"

### 3. Configure Secrets in Streamlit Cloud

In the "Secrets" section, add:

```toml
[mongo]
connection_string = "mongodb+srv://username:password@cluster.mongodb.net/"
```

**Format:**
- Use TOML format (not JSON)
- Section header: `[mongo]`
- Key: `connection_string`
- Value: Your full MongoDB connection string (in quotes)

### 4. Deploy!

Click "Deploy" and your dashboard will be live in a few minutes.

## 🔄 How Auto-Refresh Works

- Dashboard refreshes every **5 minutes** automatically
- MongoDB updates every **30 minutes** with new data
- Users see new data within 5 minutes of MongoDB update
- Manual refresh button available in sidebar

## 🔐 Security Notes

- ✅ Never commit `mongo_credentials.txt` to GitHub
- ✅ Always use Streamlit secrets for cloud deployment
- ✅ Connection strings are encrypted in Streamlit Cloud
- ✅ `.gitignore` prevents accidental credential commits

## 📊 Data Sources

- **MongoDB Database:** `reddit_sentiment`
- **Collections:** `posts`, `comments`
- **Update Frequency:** Every 30 minutes
- **Data Limit:** 3000 items per collection

## 🛠️ Tech Stack

- **Frontend:** Streamlit
- **Visualizations:** Plotly
- **Database:** MongoDB
- **NLP:** VADER + Transformer models
- **Auto-refresh:** streamlit-autorefresh

## 📝 Configuration

### Adjust Refresh Interval

To change the auto-refresh interval, modify:

```python
# In reddit_dashboard_enhanced.py
count = st_autorefresh(interval=300000, limit=None, key="datarefresh")
# 300000 ms = 5 minutes
# Change to 600000 for 10 minutes, etc.
```

### Adjust Cache Duration

```python
@st.cache_data(ttl=300)  # Cache for 5 minutes
def load_data():
    ...
```

## 🐛 Troubleshooting

### "No data found" Error
- Ensure MongoDB Producer/Consumer scripts are running
- Check MongoDB connection string in secrets
- Verify database name and collection names match

### Auto-refresh Not Working
- Install `streamlit-autorefresh`: `pip install streamlit-autorefresh`
- Check browser console for errors
- Try manual refresh button in sidebar

### Connection Timeout
- Verify MongoDB cluster is accessible
- Check IP whitelist in MongoDB Atlas (allow all: 0.0.0.0/0)
- Ensure credentials are correct in Streamlit secrets

## 📞 Support

For issues or questions, please open an issue on GitHub.

## 📄 License

MIT License
