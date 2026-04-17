# Poker Leaderboard - Security Setup

## Overview
Your Poker Leaderboard app now includes password protection for sensitive admin operations. Only you can add/remove players and save games.

## Protected Operations
🔐 The following actions now require a secret code:

1. **Add Player** - Protected
2. **Remove Player** - Protected  
3. **Save Game** - Protected

## Default Secret Code
- **Code:** `1234`

## How to Change Your Secret Code

1. Open `index.html` in a text editor
2. Find this line (around line 450):
   ```javascript
   const SECRET_CODE = '1234'; // Change this to your secret code
   ```
3. Replace `'1234'` with your desired code:
   ```javascript
   const SECRET_CODE = 'mySecretCode123'; // Change this to your secret code
   ```
4. Save the file

## How Authentication Works

### First Time Using Protected Features
- When you click "Add Player", "+ Add", "Deal It In", or try to remove a player, a modal will pop up
- Enter your secret code
- If correct, the action will execute and you'll stay authenticated for 30 minutes
- If wrong, you'll see an error message and can try again

### Session Duration
- Once authenticated, your session lasts **30 minutes**
- After 30 minutes of inactivity, you'll need to enter the code again for the next protected action
- You can manually close the app to immediately logout

### What Others See
- If someone else tries to use a protected feature, they'll see the auth modal
- Without the correct code, they cannot add/remove players or save games
- The app still works for viewing leaderboards, statistics, and game history

## Security Tips

⚠️ **IMPORTANT:**
- Keep your secret code **private**
- Don't share it with other users
- Use a strong, unique code that's hard to guess
- Consider changing it occasionally

## Features You Can Still Use Without Auth
✅ View Overall Leaderboard
✅ View Per-Game Results
✅ View Game History
✅ View Player Statistics
✅ Delete Games (still protected, but different workflow)

## Customization Options

### Change the modal styling
Look for `.auth-overlay` and `.auth-modal` CSS classes to customize colors, fonts, and appearance.

### Change the timeout duration
In the `confirmAuth()` function, find:
```javascript
setTimeout(() => { isAuthenticated = false; showToast('Session expired.'); }, 30 * 60 * 1000);
```
Replace `30 * 60 * 1000` with milliseconds (e.g., `60 * 60 * 1000` for 60 minutes).

### Customize auth messages
Look for `showAuthModal()` and `confirmAuth()` functions to change error messages and prompts.

