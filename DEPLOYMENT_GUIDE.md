# 🚀 Vercel Deployment Guide for AHP Pitch Deck

## 📋 Deployment Options

### Option 1: Direct Upload (Current Setup)
Your video file will be uploaded directly to Vercel.

**Pros:**
- Simple setup
- No external dependencies
- Works immediately

**Cons:**
- 74MB video may cause slower loading
- Uses Vercel bandwidth
- May hit size limits on free plan

**Steps:**
1. Push your code to GitHub
2. Connect to Vercel
3. Deploy (video included automatically)

### Option 2: External Video Hosting (Recommended)

Upload your video to a CDN or video hosting service for better performance.

#### 🎥 Recommended Video Hosting Options:

1. **YouTube (Free)**
   - Upload to YouTube
   - Get embed URL
   - Update `index-external-video.html`

2. **Vimeo (Free/Paid)**
   - Better for business presentations
   - No ads on paid plans
   - Professional appearance

3. **AWS S3 + CloudFront**
   - Full control
   - Fast global delivery
   - Pay-as-you-use

4. **Cloudinary**
   - Video optimization
   - Automatic compression
   - Free tier available

## 🛠️ Setup Instructions

### For Direct Upload (Current):
```bash
# 1. Initialize git (if not already done)
git init
git add .
git commit -m "Initial AHP pitch deck"

# 2. Push to GitHub
git remote add origin YOUR_GITHUB_REPO_URL
git push -u origin main

# 3. Deploy on Vercel
# - Go to vercel.com
# - Import from GitHub
# - Deploy
```

### For External Video Hosting:

#### Using YouTube:
1. Upload `AHP MOD 2.0 v4.mp4` to YouTube
2. Get the video ID from the URL (e.g., `dQw4w9WgXcQ`)
3. Update `index-external-video.html`:
   ```javascript
   youtube: {
       type: 'iframe',
       src: 'https://www.youtube.com/embed/YOUR_VIDEO_ID'
   }
   ```
4. Rename `index-external-video.html` to `index.html`
5. Deploy to Vercel

#### Using AWS S3:
1. Create S3 bucket
2. Upload video with public read permissions
3. Update video source:
   ```javascript
   custom: {
       type: 'video',
       src: 'https://your-bucket.s3.amazonaws.com/AHP-MOD-2.0-v4.mp4'
   }
   ```

## 📁 File Structure for Deployment

```
AHP-Pitch-Decl-1/
├── index.html (main file)
├── vercel.json (Vercel configuration)
├── video/ (if using direct upload)
│   └── AHP MOD 2.0 v4.mp4
└── README.md
```

## ⚡ Performance Optimization

### For Direct Upload:
- Video is cached for 1 year (see vercel.json)
- Compressed automatically by Vercel
- Consider video compression before upload

### For External Hosting:
- Use video compression (H.264, MP4)
- Enable CDN caching
- Consider multiple quality options

## 🔧 Environment Variables (if needed)

If using external APIs, add to Vercel:
```
VIDEO_CDN_URL=https://your-cdn.com
API_KEY=your-api-key
```

## 🚀 Quick Deploy Commands

```bash
# Install Vercel CLI
npm i -g vercel

# Deploy directly
vercel

# Or deploy with custom settings
vercel --prod
```

## 📱 Testing Before Deployment

Test locally:
```bash
# Start local server
python -m http.server 8000

# Test at http://localhost:8000
```

## 🎯 Recommended Approach

For your 74MB video, I recommend:

1. **Start with direct upload** (current setup) for immediate deployment
2. **Migrate to YouTube/Vimeo** later for better performance
3. **Use the external video version** (`index-external-video.html`) for production

## 🔗 Useful Links

- [Vercel Documentation](https://vercel.com/docs)
- [Video Optimization Guide](https://web.dev/fast-playback-with-preload/)
- [YouTube Embed API](https://developers.google.com/youtube/player_parameters)
- [Vimeo Embed](https://developer.vimeo.com/player/embedding)

## 🆘 Troubleshooting

**Video not loading on Vercel:**
- Check file path case sensitivity
- Verify video file is in git repository
- Check browser console for errors

**Slow loading:**
- Consider video compression
- Use external hosting
- Enable lazy loading

**Mobile issues:**
- Test responsive design
- Check video format compatibility
- Verify touch controls work
