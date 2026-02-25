---
name: lint-code
description: Run code linting with Prettier, ESLint, and TypeScript checks.
---
# lint-code
Run comprehensive code linting and auto-fix with Prettier, ESLint, and TypeScript.

## Config
- **Prettier**: `.prettierrc`, `.prettierignore`
- **ESLint**: `.eslintrc.*`, `eslint.config.*`
- **TypeScript**: `tsconfig.json`

## Process
1. **Detect configs** - Check which linters are configured:
   - `.prettierrc*` → Prettier
   - `.eslintrc.*` / `eslint.config.*` → ESLint
   - `tsconfig.json` → TypeScript
2. **Run only configured linters** - Skip linters without config:
   - Prettier format check & fix (if configured)
   - ESLint code quality check & fix (if configured)
   - TypeScript type check (if configured)
3. **Final verification** - Run all configured linters again
4. **Handle conflicts** - If issues remain, check for config conflicts and notify user

## Quick Usage
### Prettier
```bash
# Check formatting
npx prettier --check "src/**/*.{js,ts,tsx,json,css,md}"

# Auto-fix formatting
npx prettier --write "src/**/*.{js,ts,tsx,json,css,md}"
```

### ESLint
```bash
# Check code quality
npx eslint "src/**/*.{js,ts,tsx}"

# Auto-fix issues
npx eslint --fix "src/**/*.{js,ts,tsx}"
```

### TypeScript
```bash
# Type check
npx tsc --noEmit
```

## Notes
- **Only run linters with config** - Skip if no corresponding config file found
- Run linters sequentially to avoid conflicts
- Some issues require manual fix (e.g., unused variables, type errors)
- Config conflicts may occur between Prettier and ESLint rules
- Use `--cache` flag for faster subsequent runs
