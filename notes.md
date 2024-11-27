# CRA vs Vite: A Comparison

## Webpack (CRA) vs Vite in Development

- **CRA (Create React App)** or **Vue CLI** uses **Webpack**, which:
  - Transpiles source code (e.g., JSX to plain JavaScript).
  - Locates dependencies like `react` in `node_modules`, resolves their internal imports, and bundles everything, including application code, into a single `bundle.js` file sent to the browser.
  - During development, Webpack rebundles the entire app with each change, which can slow down as the app grows.

- **Vite**, in contrast:
  - Also transpiles the source code but skips bundling during development.
  - Serves dependencies (like `react`) as separate ES modules, which the browser fetches and resolves using native `import/export`.
  - This lightweight, module-based approach makes Vite significantly faster during development.

## Deployment

For deployment:
- Both tools bundle the code.
- **Vite** uses **Rollup** to create a single `bundle.js` file, similar to **Webpack**.

## Summary

- **Vite**:
  - Source code → transpiled to plain JS → browser fetches dependencies as separate ES modules → resolves modules → executes the code.

- **Webpack**:
  - Source code → transpiled to plain JS → dependencies located in `node_modules` → combined with app code into `bundle.js` → browser downloads and executes the code.
