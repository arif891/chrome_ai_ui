# Quick Start - Build Setup

Your bundler is now ready! Here's how to use it:

## ✅ Setup Complete

- ✓ esbuild installed and configured
- ✓ Build scripts added to package.json
- ✓ build.mjs configured with minification by default
- ✓ layx.js bundled with chat-app
- ✓ Code splitting optimized
- ✓ index.html updated to use bundled files

## 🚀 Common Commands

### Development (Watch Mode with Source Maps)

```bash
npm run dev
```

- Watches for file changes
- Automatically rebuilds
- Generates source maps for debugging
- Disables minification for readable code
- Best for active development

### Production Build (Minified by Default)

```bash
npm run build
```

- Minifies both bundles
- Optimizes for production
- Recommended for deployment
- Fast build time

### Development Build (One-time with Source Maps)

```bash
npm run build:dev
```

- Builds without minification
- Generates source maps
- Good for debugging
- Larger file size but readable

### Watch Mode (Production Mode)

```bash
npm run watch
```

- Watches for changes
- Rebuilds with minification
- Suitable for production-like development

### Watch Mode (Development Mode)

```bash
npm run watch:dev
```

- Watches for changes
- Builds without minification
- Generates source maps
- Best for debugging active changes

## 📦 Build Output

After running any build command, your bundled files are in `dist/`:

**Production Build:**

```bash
dist/assets/js/chat-app.bundle.js    (55.2 KB - minified)
dist/layx/layx.bundle.js              (4.0 KB - minified)
dist/chunk-*.bundle.js                (shared chunks)
```

**Development Build:**

```bash
dist/assets/js/chat-app.bundle.js    (103.2 KB + source maps)
dist/layx/layx.bundle.js              (7.6 KB + source maps)
dist/**/*.bundle.js.map               (source maps for debugging)
```

## 📝 Next Steps

1. **Start development:**

   ```bash
   npm run dev
   ```

2. **Make changes** to files in:
   - `assets/js/chat_app/`
   - `layx/`

3. **The bundle rebuilds automatically** ✨

4. **For production:**

   ```bash
   npm run build
   ```

5. **Deploy** the `dist/` folder with `index.html`

## 🔧 Build Modes Explained

| Command | Minified | Source Maps | Use Case |
|---------|----------|-------------|----------|
| `npm run build` | ✅ | ❌ | Production deployment |
| `npm run build:dev` | ❌ | ✅ | Local debugging |
| `npm run dev` | ❌ | ✅ | Active development |
| `npm run watch` | ✅ | ❌ | Production-like dev |
| `npm run watch:dev` | ❌ | ✅ | Debug with auto-rebuild |

## 📊 Bundle Comparison

**Production (minified):** ~65 KB total

- chat-app.bundle.js: 55.2 KB
- layx.bundle.js: 4.0 KB
- Chunks: ~5.8 KB

**Development (unminified):** ~117 KB total

- chat-app.bundle.js: 103.2 KB
- layx.bundle.js: 7.6 KB
- Chunks: ~6.2 KB

Production bundles are ~45% smaller due to minification!

## 💡 Tips

- **Minification reduces bundle by ~45%** for production
- **Source maps help debug** original code in dev mode
- **Code splitting creates shared chunks** for better performance
- **Watch mode rebuilds in ~300-500ms**
- **Both layx.js and chat_app are bundled** together

## ✅ Verify Your Setup

Try these commands:

```bash
# Production build (minified)
npm run build

# Check output size
ls -lh dist/

# Development build (with source maps)
npm run build:dev

# Watch mode for development
npm run dev
```

## 🎉 You're All Set

Your bundler now:

- ✨ Bundles both layx.js and chat-app
- ✨ Minifies by default for production
- ✨ Generates source maps for debugging
- ✨ Uses code splitting for optimization
- ✨ Watches for changes in dev mode

Start with `npm run dev` and enjoy development! 🚀
