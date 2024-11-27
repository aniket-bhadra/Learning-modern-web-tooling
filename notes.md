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

In **Webpack**, all files (app code and dependencies) are bundled into a single `bundle.js`, which the browser downloads and executes.

In **Vite**, files and dependencies (e.g., `react`, `react-dom`) are sent to the browser on demand. When an import statement is encountered, the browser requests the imported file or library from the Vite dev server:
- If it’s a file (e.g., `App.jsx`), the Vite dev server transpiles it on the fly and sends the transpiled code.
- If it’s a library (e.g., `react`), the Vite dev server sends it directly as an optimized ES module.

> **Optimized ES module** means the library is pre-processed (e.g., minified, split into smaller parts) for faster loading and efficient use in the browser as an ES module.

## Why Does CRA’s index.html Have No `<script>` Tag?

In **Vite**, the `<script type="module" src="/src/main.jsx">` is needed because Vite serves files as separate ES Modules to the browser. The script tag tells the browser where to start execution (in this case, from `main.jsx`). When the browser requests this file, Vite transpiles it before sending it to the browser. If the browser encounters any import statements in the file, it requests those dependencies from the Vite server, which transpiles and serves them as needed.

In contrast, **CRA** uses **Webpack**, which bundles all files into a single `bundle.js` during the build or development process. Webpack automatically injects this `bundle.js` into the HTML, so there’s no need to manually add a script tag.
