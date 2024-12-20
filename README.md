# SSR PurgeCSS Issue: Unused Styles Not Removed with Dynamic Client-Side Components

This repository demonstrates a bug where Tailwind CSS's PurgeCSS fails to remove unused styles in a server-side rendering (SSR) environment (like Next.js or Nuxt.js) when styles are dynamically added during client-side hydration.  This results in larger-than-necessary CSS bundles, impacting page load performance.

## Problem

When a component's styles are conditionally applied and only rendered on the client-side after the initial server-render, PurgeCSS might not detect and remove those unused styles.

## Reproduction

1. Clone this repository.
2. Install dependencies: `npm install`
3. Run the development server (the instructions depend on the SSR framework used, e.g., `npm run dev` for Next.js).
4. Observe the browser's developer tools (Network tab) to see that unused CSS is still present in the bundle.

## Solution

The solution involves strategies to make PurgeCSS aware of the dynamically added classes, even if they're conditionally rendered. Possible solutions include:

* **Custom PurgeCSS configuration:**  Configure PurgeCSS to include more aggressive selectors, which might cause some false positives.
* **Extracting dynamically-added classes:**  Extract the dynamic classes that are conditionally added to another CSS file that is correctly included.
* **Using a different purging strategy:**  Consider alternative approaches such as using a critical CSS extraction strategy. 

See the `bugSolution.js` for a possible solution demonstrating one of these methods.
