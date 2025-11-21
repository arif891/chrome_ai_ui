# Build Guide

This guide explains how to use the bundler and build system for the Chrome AI Chat UI project.

## Overview

The project uses **esbuild** to bundle and optimize:

- **JavaScript:** `assets/js/chat_app/main.js` and `layx/layx.js`
- **CSS:** `layx/layx.css` and `assets/css/chat_app/main.css`
- **Assets:** Fonts (woff2), images, and other resources

All files are bundled separately with code splitting for optimal performance.

## Prerequisites

- Node.js 14+
- npm or yarn

## Installation

1. Install dependencies:

```bash
npm install
```

This will install `esbuild` (ESM bundler) and other dev dependencies.

## Build Commands

### Production Build (minified by default)

```bash
npm run build
```

This command:
- Bundles both JS and CSS files
- Minifies output for smaller file size (~45% reduction)
- Optimizes for production deployment
- Creates separate bundles for chat-app and layx
- Copies font assets to dist folder

**Output Files:**

```bash
dist/assets/js/chat-app.bundle.js      (55.2 KB minified)
dist/layx/layx.bundle.js                (4.0 KB minified)
dist/assets/css/chat-app.bundle.css     (14.8 KB minified)
dist/layx/layx.bundle.css               (26.7 KB minified)
dist/assets/font/Red_Hat_Display_*.woff2 (28.4 KB)
dist/assets/font/Fira_Code.woff2        (22.8 KB)
```

### Development Build (with source maps)

```bash
npm run build:dev
```

This command:
- Bundles all files without minification
- Generates source maps (.map files) for debugging
- Preserves original code structure
- Better for local development and debugging

**Output:**

- `dist/assets/js/chat-app.bundle.js` (103.2 KB + .map file)
- `dist/layx/layx.bundle.js` (7.6 KB + .map file)
- `dist/assets/css/chat-app.bundle.css` (28.2 KB + .map file)
- `dist/layx/layx.bundle.css` (33.2 KB + .map file)
- Font files and assets copied

### Development Watch Mode

```bash
npm run dev
```

This command:
- Watches for file changes
- Automatically rebuilds without minification
- Generates source maps for debugging
- Rebuilds in ~300-500ms
- Perfect for active development

### Production Watch Mode

```bash
npm run watch
```

This command:
- Watches for file changes
- Automatically rebuilds with minification
- Production-optimized bundles
- Useful for testing production builds during development

### Watch Mode with Source Maps

```bash
npm run watch:dev
```

This command:
- Watches for file changes
- Rebuilds without minification
- Generates source maps
- Useful for debugging with auto-rebuild

## Build Configuration

The build system is configured in `build.mjs`:

```javascript
{
  entryPoints: [
    'assets/js/chat_app/main.js',
    'layx/layx.js',
    'layx/layx.css',
    'assets/css/chat_app/main.css',
  ],
  bundle: true,
  outdir: 'dist',
  outExtension: {
    '.js': '.bundle.js',
    '.css': '.bundle.css'
  },
  format: 'esm',
  target: ['chrome139'],
  minify: !process.argv.includes('--dev'),
  sourcemap: process.argv.includes('--dev'),
  splitting: true,
  platform: 'browser',
}
```

## Using Bundled Files

### Switch to Bundled CSS and JS

Update `index.html`:

```html
<!-- Production: Use bundled versions -->
<link rel="stylesheet" href="/dist/layx.bundle.css">
<link rel="stylesheet" href="/dist/chat-app.bundle.css">
<script src="/dist/layx.bundle.js" type="module"></script>
<script src="/dist/chat-app.bundle.js" type="module"></script>

<!-- Development: Use original files (currently active) -->
<!-- <link rel="stylesheet" href="/layx/layx.css">
<link rel="stylesheet" href="/assets/css/chat_app/main.css">
<script src="/layx/layx.js" type="module"></script>
<script defer src="/assets/js/chat_app/main.js" type="module"></script> -->
```

## File Structure

```
├── assets/
│   ├── js/
│   │   └── chat_app/
│   │       ├── main.js              ← Entry point for JS
│   │       ├── core/
│   │       ├── lib/
│   │       ├── ui/
│   │       └── utils/
│   └── css/
│       └── chat_app/
│           └── main.css             ← Entry point for CSS
├── layx/
│   ├── layx.js                      ← Entry point
│   ├── layx.css                     ← Entry point
│   ├── components/
│   ├── helpers/
│   ├── main/
│   ├── others/
│   └── utilities/
├── dist/                            ← Build output
│   ├── assets/
│   ├── layx/
│   └── ...
└── build.mjs                        ← Build configuration
```

## Workflow

### Development Workflow

1. Run watch mode:

   ```bash
   npm run dev
   ```

2. Edit files in `assets/js/chat_app/` or `layx/`

3. Bundle automatically updates on save

4. Test in browser (using original files via index.html)

5. Check browser console for errors

### Production Workflow

1. Build minified version:

   ```bash
   npm run build
   ```

2. Update `index.html` to use bundled files (uncomment production lines)

3. Deploy `dist/` folder with `index.html`

4. Verify all assets load correctly

## Bundle Size Comparison

| Mode | JS Size | CSS Size | Total |
|------|---------|----------|-------|
| Production (minified) | 59.2 KB | 41.5 KB | 100.7 KB |
| Development | 110.8 KB | 61.4 KB | 172.2 KB |
| Reduction | ~46% | ~32% | ~41% |

## Troubleshooting

### Build fails with font resolution errors

- Ensure font paths in CSS use relative paths
- Currently fixed: `../../../assets/font/filename.woff2`
- Fonts are automatically copied to `dist/assets/font/`

### CSS not loading in bundled version

- Check that CSS links in `index.html` point to `dist/` folder
- Verify bundled CSS exists: `dist/assets/css/chat-app.bundle.css`
- Check browser Network tab for 404 errors

### Build is slow

- First build may take 1-2 seconds
- Subsequent watch builds are much faster (~300-500ms)
- This is normal for esbuild

### Changes not reflecting in browser

- Make sure `index.html` uses bundled files
- Clear browser cache (Ctrl+Shift+Delete)
- Hard refresh browser (Ctrl+Shift+R)
- Check browser console for errors

### Bundle size too large

- Already minified in production build
- Consider removing unused dependencies
- Check for duplicate code between bundles

## Performance Tips

1. **Use minification for production:**

   ```bash
   npm run build
   ```

2. **Monitor bundle size:**
   - Production: ~100 KB total
   - Development: ~172 KB total

3. **Enable gzip compression on server:**
   - Can reduce bundle size by 60-70%
   - Configure in web server (nginx, Apache, etc.)

4. **Use source maps only in development:**
   - Already configured: `npm run build:dev`
   - Improves debugging without hurting production

## CI/CD Integration

### GitHub Actions Example

```yaml
name: Build

on: [push, pull_request]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-node@v3
        with:
          node-version: '18'
      - run: npm install
      - run: npm run build
      - uses: actions/upload-artifact@v3
        with:
          name: dist
          path: dist/
```

## Advanced Usage

### View Build Details

```bash
# See what esbuild generates
ls -lh dist/
```

### Watch Multiple Files

The watch mode automatically tracks:
- `assets/js/chat_app/**/*.js`
- `layx/**/*.js`
- `layx/**/*.css`
- `assets/css/chat_app/**/*.css`

### Disable Minification

Use `--dev` flag:

```bash
npm run build:dev
npm run watch:dev
```

## Next Steps

1. Run `npm run build` to generate production bundles
2. Switch `index.html` to use bundled files
3. Test all features in the bundled version
4. Deploy `dist/` to production
5. Use `npm run dev` during development

## Resources

- [esbuild Documentation](https://esbuild.github.io/)
- [Chrome AI API](https://developer.chrome.com/docs/ai/)
- [ES Modules Guide](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Modules)
