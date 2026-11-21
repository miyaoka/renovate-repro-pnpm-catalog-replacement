# pnpm catalog + replacement: `catalog:` references are not renamed

## Current behavior

`config:recommended` includes `replacements:all`, which replaces `@tsconfig/node24` with `@tsconfig/node26`.

The dependency is defined in the pnpm catalog and referenced from `package.json` and `packages/a/package.json` with `"catalog:"`.

Renovate opens "Replace dependency @tsconfig/node24 with @tsconfig/node26". The branch renames the key in `pnpm-workspace.yaml` only. Both `package.json` files keep `"@tsconfig/node24": "catalog:"`, so the lockfile update fails:

```
ERR_PNPM_CATALOG_ENTRY_NOT_FOUND_FOR_SPEC  No catalog entry '@tsconfig/node24' was found for catalog 'default'.
```

## Expected behavior

The `package.json` files that reference the catalog entry are renamed in the same branch (`"@tsconfig/node26": "catalog:"`), and the lockfile update succeeds.

## Link to the Renovate discussion

https://github.com/renovatebot/renovate/discussions/48267
