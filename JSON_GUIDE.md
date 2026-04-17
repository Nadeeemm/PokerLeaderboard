# JSON Data Persistence Guide

## How It Works

Your Poker Leaderboard app now uses a `data.json` file for persistent data storage.

### On Startup
- The app automatically loads player and game data from `data.json`
- If the file doesn't exist, the app starts with empty data

### When You Add Games or Players
- Changes are made in the app's memory
- Click the **💾 Save Data** button in the header to download your updated data
- Replace your `data.json` file with the downloaded version

## File Structure

The `data.json` file contains:

```json
{
  "players": [
    { "id": "1", "name": "Player Name" },
    { "id": "2", "name": "Another Player" }
  ],
  "games": [
    {
      "id": "1",
      "name": "Game Name",
      "date": "2026-04-17",
      "results": [
        { "playerId": "1", "playerName": "Player Name", "type": "win", "amount": 100.50 },
        { "playerId": "2", "playerName": "Another Player", "type": "loss", "amount": 100.50 }
      ]
    }
  ],
  "selectedGame": "1"
}
```

## Workflow

1. **Start**: App loads `data.json` automatically
2. **Add Players**: Click "+" in Players tab (requires secret code)
3. **Add Game**: Fill form and click "Deal It In" (requires secret code)
4. **Save**: Click 💾 **Save Data** button to download updated `data.json`
5. **Update**: Replace old `data.json` with the downloaded file
6. **Refresh**: Reload the page to verify data was loaded

## Alternative: Server-Based Saving

If you want automatic saving without manual downloads, you can:

### Option 1: Use a Simple Backend
Create a simple Node.js/Python server that:
- Receives POST requests with updated state
- Saves to `data.json` on disk
- Serves `data.json` on GET requests

Example Node.js endpoint:
```javascript
app.post('/api/save', (req, res) => {
  fs.writeFileSync('data.json', JSON.stringify(req.body, null, 2));
  res.json({ success: true });
});
```

Then modify the `saveState()` function to POST the data instead.

### Option 2: Use Firebase/Similar Service
Replace fetch() calls with Firebase Realtime Database operations.

## Tips

- **Backup**: Keep copies of `data.json` in case of errors
- **Manual Edits**: You can manually edit `data.json` to fix data
- **Browser Console**: Check console (F12) for debug logs during load/save
- **Backup Storage**: Data is also saved to browser's localStorage as a safety net

## Current Data

Your `data.json` currently contains:
- **10 Players**: Og Gaurav, Vatsal, Nadeem, Monty, Hanu, Anush, Sam, Keshav, HeHe, Ginni
- **1 Game**: "Poker Night #1" with all results loaded

