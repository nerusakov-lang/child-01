# CLAUDE.md

## Project Overview

**Child Health Roadmap** (Дорожная карта здоровья ребёнка) - A Russian-language single-page web application that tracks infant development milestones, medical checkups, vaccinations, and recommendations for the first 6 months of life.

## Tech Stack

- **Frontend**: Vanilla HTML/CSS/JavaScript (single-file architecture)
- **Styling**: Tailwind CSS (CDN-loaded from `cdn.tailwindcss.com`)
- **Data Persistence**: Browser localStorage
- **Language**: Russian (ru)

## Codebase Structure

```
/
├── index.html       # Main application (all code in one file)
├── icon-512.png     # App icon (512x512 PNG)
└── CLAUDE.md        # This file
```

## Application Architecture

The entire application is contained in `index.html`:

### HTML Structure (lines 1-75)
- Header with birth date input and progress bar
- Month tabs navigation
- Main content area
- Settings modal
- Bottom navigation bar

### CSS (lines 8-28)
- Custom styles embedded in `<style>` tag
- Category color-coding with left borders
- Animations and transitions
- Mobile-optimized scrollbar hiding

### JavaScript (lines 76-109)
- `healthData` object: Contains all milestone data for months 1-6
- State management via `currentMonth`, `currentView`, `completedItems`, `birthDate`
- localStorage helpers: `safeGet()`, `safeSet()`
- Rendering functions: `renderContent()`, `renderCat()`, `renderItem()`, etc.
- Export feature: Generates `.ics` calendar file

## Data Structure

The `healthData` object contains data for each month (1-6) with categories:
- `physical` - Physical development metrics
- `motor` - Motor skill milestones
- `emotional` - Emotional/cognitive development
- `nutrition` - Feeding guidelines
- `sleep` - Sleep recommendations
- `doctors` - Medical checkups
- `tests` - Medical tests/screenings
- `vaccines` - Vaccination schedule
- `recommendations` - General care tips

Each item has:
- `id`: Unique identifier (format: `{month}-{category_initial}{number}`)
- `text`: Main description
- `note` (optional): Additional details

## Key Features

1. **Age Tracking**: Auto-calculates infant's age from birth date
2. **Progress Tracking**: Checkboxes persist via localStorage
3. **Multiple Views**: Calendar (by month), Vaccines, Doctors
4. **ICS Export**: Export appointments to calendar apps
5. **Settings**: Reset progress or birth date

## Development Guidelines

### Code Style
- All code is in a single `index.html` file
- Use vanilla JavaScript (no frameworks/bundlers)
- Maintain Russian language for all user-facing text
- Keep CSS minimal, leverage Tailwind utilities

### Adding New Features
1. For new data items: Add to the `healthData` object
2. For new categories: Add to each month's `categories` object and create CSS class `.category-{name}`
3. For new views: Add button to nav, create `render{ViewName}()` function

### Data ID Convention
- Format: `{month}-{category_initial}{sequential_number}`
- Examples: `1-p1` (month 1, physical, item 1), `3-v2` (month 3, vaccines, item 2)
- Category initials: p=physical, m=motor, e=emotional, n=nutrition, s=sleep, d=doctors, t=tests, v=vaccines, r=recommendations

### Testing
- No automated tests - manual browser testing
- Test in mobile viewport (max-width: 512px is optimal)
- Verify localStorage persistence across page reloads

### Common Modifications

**Adding a new milestone:**
```javascript
// In healthData[month].categories.{category}.items, add:
{id: "X-YN", text: "Description", note: "Optional note"}
```

**Changing category colors:**
```css
/* In <style> block, modify: */
.category-{name} { border-left: 4px solid #hexcolor; }
```

## Important Notes

- The app is fully client-side with no backend
- All data stays in user's browser (localStorage)
- Medical information follows Russian healthcare standards (vaccination schedule, checkup timings)
- Mobile-first design optimized for smartphone usage

## External Dependencies

- Tailwind CSS (CDN): `https://cdn.tailwindcss.com`
  - No version pinned - uses latest
  - If stability issues occur, consider pinning version

## Build/Deployment

No build process required. Simply serve the `index.html` file via any static file server or open directly in a browser.

```bash
# Local development options:
python3 -m http.server 8000
# or
npx serve .
```
