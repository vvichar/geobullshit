# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a single-file web application for studying Lithuanian geography curriculum. It's a quiz app that highlights geographic features on an interactive map and asks users to identify them by typing the name.

## Architecture

**Single HTML File Application**
- `index.html` contains everything: HTML structure, CSS styles, JavaScript logic, and geographic data
- No build process, no dependencies to install - just open in a browser
- Uses CDN-loaded libraries: Leaflet.js for mapping

**Key Components (all in index.html):**

1. **Geographic Data** (`geographyData` object)
   - Three categories: `mountains`, `rivers`, `lakes`
   - Each location has: `name`, `lat`, `lng`, `zoom`, and `polygon` (array of coordinate pairs)
   - Polygons define the actual shape of geographic features on the map

2. **Map Configuration**
   - Uses Leaflet.js with CartoDB Voyager tiles (no labels variant)
   - Centered at `[20, 0]` with zoom level 2 for global view
   - Polygons are highlighted in red with 20% opacity fill

3. **Quiz Logic**
   - Text-input based (not multiple choice)
   - Case-insensitive answer matching
   - Tracks score, correct/incorrect counts, question number
   - Category filtering available

4. **User Interaction**
   - Tracks if user manually zoomed/panned (`userInteracted` flag)
   - Auto-centers map on new questions only if user hasn't interacted
   - Supports Enter key to submit answers

## Running the Application

```bash
# Simply open the file in any browser
start index.html
# or
open index.html
```

No server required - it's a static HTML file.

## Development Workflow

**To add new locations:**
1. Add entry to the appropriate category in `geographyData` object
2. Include `name`, `lat`, `lng`, `zoom`, and `polygon` coordinates
3. Polygon coordinates are `[lat, lng]` pairs forming a closed shape

**To modify map appearance:**
- Map tiles: Change the tile layer URL in `L.tileLayer()`
- Polygon styling: Modify the options in `L.polygon()` call (color, fillColor, fillOpacity, opacity, weight)
- Initial view: Adjust `map.setView([lat, lng], zoom)`

**To adjust quiz behavior:**
- Answer checking: `checkAnswer()` function handles case-insensitive matching
- Score calculation: Points awarded in `checkAnswer()`
- Question loading: `loadQuestion()` selects random location and displays polygon

## Git Workflow

- Default branch: `claude/geography-study-app-abGy1` (currently active default)
- Push all changes to the default branch, not feature branches
- Repository uses simple direct-push workflow

## Important Notes

- The app is in Lithuanian language (`lang="lt"`)
- Mobile responsive with breakpoint at 768px (column-reverse layout)
- User interaction tracking prevents jarring auto-centering during manual exploration
- Polygon shapes are approximate representations of geographic features
