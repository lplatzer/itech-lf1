# DROID.md - reveal.js Project Reference

## Project Overview
- **Name**: reveal.js
- **Version**: 5.2.1
- **Description**: The HTML Presentation Framework
- **Homepage**: https://revealjs.com
- **License**: MIT
- **Author**: Hakim El Hattab (hakim.elhattab@gmail.com)

reveal.js is an open source HTML presentation framework that enables creating beautiful presentations in a web browser. It comes with powerful features including nested slides, Markdown support, Auto-Animate, PDF export, speaker notes, LaTeX typesetting, syntax highlighted code, and an extensive API.

## Repository Structure

```
reveal.js/
├── css/              # Custom CSS stylesheets
├── demo.html         # Demo presentation example
├── dist/             # Built/compiled files
│   ├── reset.css
│   ├── reveal.css
│   ├── reveal.js     # Main UMD bundle
│   ├── reveal.esm.js # ES module bundle
│   └── theme/        # Built-in themes
├── examples/         # Example presentations
├── js/              # Source JavaScript files
├── plugin/          # Core plugins
│   ├── highlight/   # Syntax highlighting
│   ├── markdown/    # Markdown support
│   ├── math/        # LaTeX/Math support
│   ├── notes/       # Speaker notes
│   ├── search/      # Search functionality
│   └── zoom/        # Zoom functionality
├── test/            # Test files
├── gulpfile.js      # Build configuration
├── index.html       # Main presentation file
└── package.json     # NPM dependencies and scripts
```

## Key Files

### index.html
The main presentation file. Contains:
- HTML structure for slides within `<div class="reveal"><div class="slides">`
- Links to required CSS (reset, reveal, theme, syntax highlighting)
- Script imports for reveal.js and plugins
- Reveal.initialize() configuration

### package.json
- **Main entry**: dist/reveal.js (UMD)
- **Module entry**: dist/reveal.esm.js (ES modules)
- **Node requirement**: >= 18.0.0

### gulpfile.js
Build system using Gulp with:
- Rollup for bundling JavaScript
- Babel for transpilation (ES5 and ESM targets)
- Sass for CSS compilation
- Terser for minification
- ESLint for linting
- gulp-connect for local development server

## NPM Scripts

```bash
npm start      # Start development server (gulp serve)
npm run build  # Build production files (gulp build)
npm test       # Run tests (gulp test)
```

## Development Commands

```bash
# Start local development server
npm start
# Default: http://localhost:8000

# Custom port and host
gulp serve --port=8080 --host=0.0.0.0

# Build all files
npm run build

# Run tests
npm test
```

## Creating Presentations

### Basic Structure
```html
<div class="reveal">
  <div class="slides">
    <section>Slide 1</section>
    <section>Slide 2</section>
    <section>
      <section>Nested slide 1</section>
      <section>Nested slide 2</section>
    </section>
  </div>
</div>
```

### Initialization
```javascript
Reveal.initialize({
  hash: true,
  plugins: [ RevealMarkdown, RevealHighlight, RevealNotes ]
});
```

## Available Plugins

1. **RevealMarkdown** - Write slides in Markdown
2. **RevealHighlight** - Syntax highlighting for code blocks
3. **RevealNotes** - Speaker notes view
4. **RevealMath** - LaTeX/MathJax support
5. **RevealSearch** - Search functionality
6. **RevealZoom** - Zoom in/out capability

## Built-in Themes

Located in `dist/theme/`:
- black.css (default)
- white.css
- league.css
- beige.css
- sky.css
- night.css
- serif.css
- simple.css
- solarized.css
- blood.css
- moon.css
- And more...

## Key Dependencies

### Production
- Core-js for polyfills
- Fitty for text fitting
- Highlight.js for syntax highlighting
- Marked for Markdown parsing

### Development
- Gulp build system
- Rollup for bundling
- Babel for transpilation
- Sass for stylesheets
- QUnit + Puppeteer for testing

## Configuration Options

Common Reveal.initialize() options:
- `hash`: Enable URL hash-based navigation
- `controls`: Show navigation controls
- `progress`: Show progress bar
- `slideNumber`: Display slide numbers
- `transition`: Transition style (none/fade/slide/convex/concave/zoom)
- `theme`: Theme selection
- `plugins`: Array of plugins to load

Full documentation: https://revealjs.com/config/

## Git Status

- **Current branch**: main (default)
- **Modified files**:
  - index.html
  - package-lock.json

## Useful Links

- Documentation: https://revealjs.com/markup/
- Demo: https://revealjs.com/demo
- Installation: https://revealjs.com/installation
- API: https://revealjs.com/api/
- Visual Editor: https://slides.com/

## Common Tasks

### Adding a New Slide
Edit index.html and add a new `<section>` within the slides div.

### Changing Theme
Modify the theme CSS link in index.html:
```html
<link rel="stylesheet" href="dist/theme/[theme-name].css">
```

### Using Markdown
```html
<section data-markdown>
  <textarea data-template>
    ## Slide Title
    - Bullet point
  </textarea>
</section>
```

### Adding Speaker Notes
```html
<section>
  <h2>Slide Content</h2>
  <aside class="notes">
    These are speaker notes visible only in speaker view
  </aside>
</section>
```

## Browser Support
Targets: > 2% market share and not dead browsers (see browserslist in package.json)

## Testing
Uses QUnit with Puppeteer for automated browser testing.
