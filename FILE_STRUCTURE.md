# Poker Leaderboard - New File Structure

## Overview
The application has been refactored to use a modular file structure with separate JSON files for each game instead of storing everything in a single `data.json` file.

## New File Structure

```
PokerLeaderboard/
├── index.html                 # Main application (updated)
├── players.json              # Central player list (NEW)
├── games-manifest.json       # Game metadata index (NEW)
├── games/                    # Games directory (NEW)
│   ├── game-1.json
│   ├── game-2.json
│   ├── game-3.json
│   ├── game-4.json
│   ├── game-5.json
│   ├── game-6.json
│   ├── game-7.json
│   └── game-8.json
├── data.json                 # Legacy (can be archived/deleted)
├── DEPLOYMENT.md
├── JSON_GUIDE.md
└── SECURITY_SETUP.md
```

## Files Created

### 1. players.json
Contains the master list of all players with their IDs and names. This is the single source of truth for player data.

**Structure:**
```json
{
  "players": [
    { "id": "1", "name": "Gaurav" },
    { "id": "2", "name": "Vatsal" },
    ...
  ]
}
```

### 2. games-manifest.json
Index file that lists all games with their metadata and corresponding file paths. This allows the app to know which game files exist without loading them all.

**Structure:**
```json
{
  "games": [
    {
      "id": "1",
      "name": "Poker Night April 11th",
      "date": "2026-04-11",
      "file": "game-1.json"
    },
    ...
  ]
}
```

### 3. games/game-N.json
Individual game files containing complete game results. Each game has its own file for better organization and modularity.

**Structure:**
```json
{
  "id": "1",
  "name": "Poker Night April 11th",
  "date": "2026-04-11",
  "results": [
    {
      "playerId": "4",
      "playerName": "Monty",
      "type": "win",
      "amount": 2653.3
    },
    ...
  ]
}
```

## Code Changes

### loadState() Function
- Now loads players from `players.json`
- Loads game manifest from `games-manifest.json`
- Asynchronously loads individual game files from the `games/` directory
- Stores selected game date in localStorage instead of state
- Gracefully handles missing files with try-catch blocks

### saveState() Function
- Stores selected game date in localStorage
- Maintains localStorage backup for client-side state
- No longer auto-downloads files on every save

### saveGameFile() Function (NEW)
- Saves individual game files
- Downloads game file to client
- Logs game data to console for verification

### downloadDataAsJSON() Function
- Updated to export all data as a complete backup
- Useful for full database exports

## Benefits of This Structure

1. **Modularity**: Each game is independent, making it easier to manage individual game data
2. **Scalability**: Adding new games doesn't require modifying large monolithic files
3. **Maintainability**: Easier to find and update specific games
4. **Performance**: Lazy loading of individual games can be implemented if needed
5. **Version Control**: Smaller files are easier to track in git
6. **Separation of Concerns**: Players, game index, and individual games are separate

## Data Migration

All existing data from `data.json` has been automatically extracted and distributed:
- Players → `players.json`
- Game summaries → `games-manifest.json`
- Individual game details → `games/game-N.json`

## Usage Notes

1. **Adding New Players**: Edit `players.json` to add new players with sequential IDs
2. **Adding New Games**: 
   - Create new game file in `games/` directory (e.g., `game-9.json`)
   - Add entry to `games-manifest.json`
   - Or use the UI which will auto-generate files
3. **Backup**: Use the "Download" button in the app to export complete backup as JSON
4. **Restore**: If needed, the localStorage backup can be recovered via browser console

## Next Steps (Optional)

1. **Backend Integration**: Add server-side endpoints to persist game files
2. **Database**: Replace JSON files with database entries
3. **Pagination**: Implement lazy loading for faster initial app load
4. **Archive**: Move old games to archive directory for better organization
5. **Validation**: Add schema validation for JSON files

## Testing Checklist

- [x] Players load correctly
- [x] Game manifest loads correctly
- [x] Individual games load correctly
- [x] Selected game persists via localStorage
- [x] New games can be added
- [x] Overall stats calculate correctly
- [x] Per-game stats display correctly
- [x] Download backup functionality works
