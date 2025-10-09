# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a **Shopify theme** based on the **Empire theme (v12.0.0)** by Pixel Union. The theme is customized for a Shopify store located at `bongs-ca.myshopify.com` with theme ID `148623130813`.

## Development Commands

### Shopify CLI Commands
```bash
# Start local development server
npm run dev

# Push theme to Shopify store
npm run push

# Pull theme from Shopify store
npm run pull
```

All Shopify theme commands target:
- Store: `bongs-ca.myshopify.com`
- Theme ID: `148623130813`

## Architecture & Structure

### Shopify Theme Structure

This follows standard Shopify 2.0 theme architecture:

- **`layout/`** - Theme layouts (theme.liquid, password.liquid, quickshop.liquid, none.liquid)
- **`sections/`** - Reusable sections for theme customization
  - `static-*.liquid` - Core static sections (header, footer, product, collection, cart, etc.)
  - `dynamic-*.liquid` - Dynamic/customizable sections (slideshow, featured collection, blog posts, etc.)
  - `pxs-*.liquid` - Pixel Union specific sections (newsletter, map, image-with-text-overlay)
- **`snippets/`** - Reusable Liquid components (navigation, product grid, form elements, icons, etc.)
- **`templates/`** - Page templates with both `.liquid` and `.json` formats
  - JSON templates define section configurations for Shopify 2.0
  - Liquid templates for customers/* pages
- **`blocks/`** - Custom blocks for app/theme sections
- **`assets/`** - Static files (CSS, JS, images)
  - `empire.js` / `empire.min.js` - Main theme JavaScript (webpack bundled)
  - `theme.css.liquid` - Main theme styles (Liquid template for dynamic CSS)
  - `polyfills.min.js` - Browser polyfills
  - `instantPage.min.js` - Page preloading
- **`locales/`** - Translation files for internationalization
- **`config/`** - Theme settings and configuration
  - `settings_schema.json` - Theme customization options (colors, typography, products, etc.)
  - `settings_data.json` - Current theme settings values

### Key Features

- **Age Gate**: Site-wide age verification system
- **Live Search**: Predictive search with quick links and images
- **Product Features**:
  - Quickshop functionality
  - Product compare (up to 3 products)
  - Product swatches (color/variant display)
  - Recently viewed products
  - Inventory status display with low stock indicators
  - Dynamic checkout button support
- **Navigation**: Mega menu with images, sidebar navigation, multi-column menus
- **Cart**: Add-to-cart banner, free shipping progress bar
- **Collections**: Multiple layouts (grid, subcollections, with FAQ)
- **Performance**: Script minification, animation reduction options, instant page loading

### JavaScript Architecture

The main JavaScript is webpack-bundled in `assets/empire.js`:
- Uses TypeScript-compiled modules
- CSS breakpoint detection system
- Module-based architecture with callbacks
- Async script loading with polyfill support

### Liquid Templates

- Main layout: `layout/theme.liquid` - includes head, body structure, modals, PhotoSwipe gallery
- Header: `sections/static-header.liquid` - sticky header, logo, search, cart, navigation
- Complex Liquid logic for:
  - Product variant selection
  - Collection filtering/sorting
  - Age gate verification
  - Add-to-cart functionality
  - Product comparison

## Common Development Patterns

### Liquid Debugging
- Use console logs (not logger) per user instructions
- Theme version and routes available in `window.Theme` object

### TypeScript/JavaScript
- After making changes to TypeScript/JavaScript, check for TypeScript errors
- Minified scripts controlled by `settings.minify_scripts` setting

### Styling
- CSS is generated from Liquid templates (`.css.liquid` files)
- Theme uses CSS custom properties for colors, fonts, and layout
- Responsive breakpoints managed via CSS pseudo-elements

### Product Variants
- Product option styles: select dropdowns or radio buttons
- Swatch system for color/image variants
- Sold out options: selectable, disabled, or hidden

## Important Settings

Theme settings are configured in `config/settings_schema.json`:
- **Colors**: Background, text, buttons, header, footer, overlays
- **Typography**: Fonts for headings, body, menu, buttons, sections
- **Products**: Sale badges, inventory display, variant options, swatches
- **Product Grid**: Image styles, quickshop, product compare
- **Cart**: Free shipping bar, checkout lock icon
- **Performance**: Animation reduction, script minification

## Notes

- This is a production Shopify theme - be careful with changes to core functionality
- Theme documentation: http://support.pixelunion.net/category/385-empire
- Theme support: https://support.pixelunion.net/hc/en-us/requests/new
