# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

reveal.js is an open source HTML presentation framework that enables creating beautiful web-based presentations. This repository contains the core framework source code and build system.

## Build System

The project uses **Gulp** as its build system with tasks defined in `gulpfile.js`.

### Key Commands

```bash
# Development server with live reload (default port 8000)
npm start
# or: gulp serve
# Custom port/host: gulp serve --port=9000 --host=0.0.0.0

# Build all distribution files (UMD + ESM bundles)
npm run build
# or: gulp build

# Run tests (ESLint + QUnit via Puppeteer)
npm test
# or: gulp test

# Run only linting
gulp eslint

# Run only QUnit tests
gulp qunit

# Package presentation as zip file
gulp package
```

### Build Output

- **dist/reveal.js** - UMD bundle with broad browser support (ES5 transpiled)
- **dist/reveal.esm.js** - ES module bundle for modern browsers
- **dist/theme/** - Compiled CSS themes from Sass sources
- **plugin/*/[name].js** - UMD plugin bundles
- **plugin/*/[name].esm.js** - ES module plugin bundles

## Architecture

### Core Structure

The codebase follows a modular architecture centered around a main Reveal class:

- **js/reveal.js** - Main Reveal class factory function; manages initialization, configuration, state, and coordinates all controllers
- **js/index.js** - Public API wrapper providing backwards compatibility with pre-4.0 API; exports singleton pattern
- **js/config.js** - Default configuration values
- **js/controllers/** - Feature-specific controllers (19 modules):
  - `autoanimate.js` - Auto-animate transitions between slides
  - `backgrounds.js` - Slide backgrounds management
  - `controls.js` - Navigation controls UI
  - `fragments.js` - Fragment (step-by-step) content
  - `keyboard.js` - Keyboard navigation
  - `location.js` - URL hash management
  - `overview.js` - Overview mode (grid view)
  - `plugins.js` - Plugin system management
  - `printview.js` - Print/PDF layout
  - `scrollview.js` - Scroll-based presentation mode
  - `slidecontent.js` - Slide content processing
  - `slidenumber.js` - Slide number display
  - Others: focus, jumptoslide, notes, overlay, pointer, progress, touch
- **js/components/playback.js** - Single component for auto-slide playback controls
- **js/utils/** - Shared utility functions and constants

### Plugin System

Built-in plugins (bundled separately):
- **Highlight** - Syntax highlighting for code blocks
- **Markdown** - Markdown content support
- **Search** - Text search functionality
- **Notes** - Speaker notes view
- **Zoom** - Zoom in/out on slide content
- **Math** - LaTeX math typesetting

Each plugin is built as both UMD and ESM modules, located in `plugin/[name]/plugin.js`.

### Build Process

1. **JavaScript**: Rollup bundles source with Babel transpilation:
   - ES5/UMD target: Uses `babelConfig` with core-js polyfills for broad browser support
   - ESM target: Uses `babelConfigESM` targeting modern browsers only
   - Terser minification applied to both
2. **CSS**: Sass compilation with autoprefixer and minification (IE9 compatibility for core)
3. **Themes**: Sass themes compiled from `css/theme/source/` to `dist/theme/`

### Testing

- **QUnit** tests in `test/*.html` run via Puppeteer in headless Chrome
- Tests run on local server (port 8009) during `gulp qunit`
- ESLint configuration in package.json enforces code style

## Code Style

From `.github/CONTRIBUTING.md` and ESLint config:
- **Indentation**: Tabs (not spaces)
- **Strings**: Single quotes
- **Strict equality**: Always use `===` and `!==` (enforced by ESLint)
- Follow existing file conventions when modifying code

## HTML Structure

Presentations require this basic structure (see `index.html`):

```html
<div class="reveal">
  <div class="slides">
    <section>Slide content</section>
  </div>
</div>
```

Initialize with:
```javascript
Reveal.initialize({
  hash: true,
  plugins: [ RevealMarkdown, RevealHighlight, RevealNotes ]
});
```

## Development Notes

- **Node.js**: Requires version 18.0.0 or higher
- **Watch mode**: `gulp serve` provides live reload for HTML, MD, JS, CSS, and plugin changes
- **Source maps**: Generated for all JavaScript bundles
- **Caching**: Rollup build cache maintained in memory for faster rebuilds
