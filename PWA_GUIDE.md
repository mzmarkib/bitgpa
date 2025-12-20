# PWA (Progressive Web App) Guide

## ✅ PWA Features Implemented

### 1. Web App Manifest (`manifest.json`)
- App name and short name
- Theme colors matching the app design
- Icons for home screen installation
- Display mode: standalone (app-like experience)
- App shortcuts for quick actions

### 2. Service Worker (`sw.js`)
- **Offline Support**: Caches critical assets for offline use
- **Cache Strategy**: Cache-first with network fallback
- **Automatic Updates**: Cleans up old caches on activation
- **Performance**: Serves cached assets instantly

### 3. Add to Home Screen Prompt
- Automatic prompt after 3 seconds (if not dismissed)
- User-friendly install button
- Dismiss option with session storage
- Won't show if app is already installed

### 4. Local Storage
- **Auto-save**: Saves GPA selections automatically
- **Auto-load**: Restores previous selections on page load
- **Storage Key**: `bitgpa_selections`
- **Data Stored**:
  - Subject code
  - Grade Point Value (GPV)
  - Attempt status (1st or 2nd)

## 📱 Installation Instructions

### For Users:

#### Android (Chrome)
1. Visit the website
2. Wait for the install prompt, OR
3. Tap the menu (⋮) → "Install app" or "Add to Home screen"
4. Confirm installation

#### iOS (Safari)
1. Visit the website
2. Tap the Share button (□↑)
3. Scroll down and tap "Add to Home Screen"
4. Tap "Add"

#### Desktop (Chrome/Edge)
1. Visit the website
2. Click the install icon in the address bar, OR
3. Wait for the install prompt
4. Click "Install"

## 🔧 Technical Details

### Service Worker Caching
The service worker caches the following on install:
- HTML, CSS, JavaScript
- JSON data files
- Fonts
- Icons
- Manifest

### Cache Versioning
- **Current Version**: `bitgpa-v1`
- When updating, change version number in `sw.js`
- Old caches are automatically cleaned up

### Local Storage Structure
```javascript
{
  "IT1105": {
    "gpv": "3.75",
    "isFirstAttempt": true
  },
  "IT1205": {
    "gpv": "4",
    "isFirstAttempt": false
  }
  // ... more subjects
}
```

## 🎨 Customization

### Icons
To use custom icons for PWA:
1. Create 192x192 and 512x512 PNG icons
2. Place in `img/icons/` directory
3. Update `manifest.json` with new icon paths

**Recommended Icon Sizes:**
- 192x192 (minimum)
- 512x512 (recommended)
- 144x144 (Android)
- 180x180 (iOS)

### Theme Color
Change in `manifest.json` and HTML meta tag:
```json
{
  "theme_color": "#0089D2"
}
```

### Prompt Timing
Adjust delay in `index.html`:
```javascript
setTimeout(() => {
    if(deferredPrompt && installPrompt) {
        installPrompt.style.display = 'flex';
    }
}, 3000); // Change 3000 to desired milliseconds
```

## 🐛 Troubleshooting

### Service Worker Not Registering
- Check browser console for errors
- Ensure HTTPS (or localhost for testing)
- Verify `sw.js` is accessible at root (`/sw.js`)

### Install Prompt Not Showing
- Clear browser cache
- Check if already installed
- Verify `manifest.json` is valid
- Ensure HTTPS (required for install prompt)

### Local Storage Not Working
- Check browser storage limits
- Verify localStorage is enabled
- Check browser console for errors

### Offline Not Working
- Clear browser cache and service worker
- Verify assets are being cached
- Check Network tab in DevTools

## 📊 Testing

### Test Service Worker
1. Open DevTools → Application → Service Workers
2. Check registration status
3. Test offline mode (Network tab → Offline)
4. Verify cached resources

### Test Install Prompt
1. Clear site data
2. Visit site on supported browser
3. Wait for prompt (or use browser menu)
4. Verify installation

### Test Local Storage
1. Select some grades
2. Check DevTools → Application → Local Storage
3. Refresh page
4. Verify selections are restored

## 🔐 Security Notes

- Service Worker requires HTTPS (except localhost)
- Local Storage is domain-specific
- No sensitive data stored (only grade selections)

## 📝 Browser Support

| Feature | Chrome | Firefox | Safari | Edge |
|---------|--------|---------|--------|------|
| Service Worker | ✅ | ✅ | ✅ (11.1+) | ✅ |
| Web Manifest | ✅ | ✅ | ✅ (iOS 11.3+) | ✅ |
| Install Prompt | ✅ | ✅ | ⚠️ (Manual) | ✅ |
| Local Storage | ✅ | ✅ | ✅ | ✅ |

## 🚀 Next Steps

1. Create proper PWA icons (192x192, 512x512)
2. Update `manifest.json` with actual icon paths
3. Test on various devices
4. Submit to app stores (if desired):
   - PWA Builder for Microsoft Store
   - Trusted Web Activity for Google Play

