# Descr

Just test project to train Nuxt Skills

# Nuxt Minimal Starter

Look at the [Nuxt documentation](https://nuxt.com/docs/getting-started/introduction) to learn more.

## Setup

Make sure to install dependencies:

```bash
# npm
npm install

# pnpm
pnpm install

# yarn
yarn install

# bun
bun install
```

## Development Server

Start the development server on `http://localhost:3000`:

```bash
# npm
npm run dev

# pnpm
pnpm dev

# yarn
yarn dev

# bun
bun run dev
```

## Production

Build the application for production:

```bash
# npm
npm run build

# pnpm
pnpm build

# yarn
yarn build

# bun
bun run build
```

Locally preview production build:

```bash
# npm
npm run preview

# pnpm
pnpm preview

# yarn
yarn preview

# bun
bun run preview
```

Check out the [deployment documentation](https://nuxt.com/docs/getting-started/deployment) for more information.

# Directory Structure

```
project-root/
├── assets/               # Uncompiled assets like images, fonts, or SCSS files
├── components/           # Reusable Vue components
│   ├── ItemCard.vue      # Example: Card to display an item
│   ├── FilterMenu.vue    # Example: Filter menu component
│   └── Header.vue        # Example: Header component
├── data/                 # JSON files with item data
│   ├── items.json        # Example: Main items list
│   └── categories.json   # Example: Categories for filtering
├── layouts/              # Layouts to structure the app
│   ├── default.vue       # Main layout with header/footer
│   └── auth.vue          # Layout for authentication pages
├── middleware/           # Middleware for authentication or route guards
│   └── auth.js           # Example: Auth middleware
├── pages/                # Nuxt pages based on the routing system
│   ├── index.vue         # Homepage
│   ├── store.vue         # Store page (item grid)
│   └── items/            # Dynamic item routes
│       └── [id].vue      # Individual item details page
├── plugins/              # Plugins to extend Vue/Nuxt functionality
│   └── axios.js          # Example: Axios plugin for API calls
├── public/               # Static files directly served (favicon, robots.txt)
├── static/               # Static assets (will be copied as-is during build)
│   └── images/           # Example: Static images
├── store/                # Vuex or Pinia store (if using)
│   ├── cart.js           # Cart state management
│   ├── wishlist.js       # Wishlist state management

```

### Description of Folders and Files:

- **`assets/`**: Store uncompiled files like images, fonts, or raw SCSS files.
- **`components/`**: Houses reusable Vue components.
- **`data/`**: Contains JSON files or other static data sources.
- **`layouts/`**: Defines reusable layouts with a consistent structure.
- **`middleware/`**: Stores custom middleware logic, such as authentication guards.
- **`pages/`**: Maps directly to the routes of your app.
- **`plugins/`**: Contains custom plugins for extending Vue or Nuxt.
- **`static/`**: Serves static files directly, unchanged.
- **`store/`**: Manages the application state using Vuex or Pinia.
