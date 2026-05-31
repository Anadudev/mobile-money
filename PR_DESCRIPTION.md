# PR Description

## Summary
The Swagger UI integration now serves its static assets (CSS & JavaScript) from the **jsDelivr CDN** by default, improving documentation load performance. Set `SWAGGER_CDN='false'` to revert to local assets if needed.

## Changes Made
- **File Modified:** `src/routes/docs.ts`
  ```ts
  // Previously:
  const useCdn = process.env.SWAGGER_CDN === 'true';
  // Updated to:
  // Use CDN for Swagger UI assets unless explicitly disabled via SWAGGER_CDN='false'
  const useCdn = process.env.SWAGGER_CDN !== 'false';
  ```
- The new logic defaults to using the CDN unless `SWAGGER_CDN` is explicitly set to `'false'`.

## Impact
- **Performance:** Faster loading of the Swagger UI documentation in development and production.
- **Compatibility:** Existing environments that rely on local assets can retain that behavior by setting `SWAGGER_CDN='false'`.
- **Scope:** No other files or functionality were modified.

## Testing
1. Run the application in development mode with the default configuration; Swagger UI should load assets from `https://cdn.jsdelivr.net/npm/swagger-ui-dist/...`.
2. Set `SWAGGER_CDN='false'` and verify that the UI falls back to local assets.
3. All existing test suites pass (`npm test`).

## Upstream
The branch `standardize-mock-assertions` now tracks `origin/standardize-mock-assertions` and has been pushed.
