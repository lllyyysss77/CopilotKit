```markdown
# CopilotKit Development Patterns

> Auto-generated skill from repository analysis

## Overview

This skill teaches you the core development patterns, conventions, and workflows used in the CopilotKit monorepo. CopilotKit is a TypeScript-based project built on Next.js, organized as a multi-package workspace. The repository emphasizes clear commit conventions, modular code organization, robust testing, and a set of repeatable workflows for feature development, testing, documentation, and release management.

## Coding Conventions

### File Naming

- **CamelCase** is used for file names.
  - Example: `agentCapabilities.ts`, `sharedStateManager.ts`

### Import Style

- **Alias imports** are preferred for referencing internal modules.
  ```typescript
  import { AgentManager } from '@copilotkit/core';
  import { useSharedState } from '@copilotkit/react-core';
  ```

### Export Style

- **Mixed exports**: Both named and default exports are used, depending on context.
  ```typescript
  // Named export
  export function useAgent() { ... }

  // Default export
  export default AgentProvider;
  ```

### Commit Messages

- **Conventional commits** are enforced.
  - Prefixes: `fix:`, `feat:`, `style:`, `chore:`, `test:`, `docs:`
  - Example: `feat: add agent capability propagation to runtime layer`

## Workflows

### Package Version Bump and Changelog

**Trigger:** When preparing for a new release or after merging significant changes.  
**Command:** `/bump-version`

1. Update `package.json` version for each package:
    ```json
    {
      "version": "1.2.0"
    }
    ```
2. Update `CHANGELOG.md` for each package with new changes.
3. Update `pnpm-lock.yaml` to lock new versions.

---

### Add or Update Feature Across Multiple Packages

**Trigger:** When adding a cross-cutting feature (e.g., agent capabilities) that must propagate through multiple layers.  
**Command:** `/add-feature-multi`

1. Add or update types in `packages/shared/src/utils/types.ts`.
2. Implement the feature in:
    - `packages/core/src/**/*.ts`
    - `packages/runtime/src/**/*.ts`
    - `packages/react-core/src/**/*.tsx`
3. Add or update tests in `__tests__` folders:
    ```typescript
    // Example test file
    import { newFeature } from '../newFeature';

    test('should work as expected', () => {
      expect(newFeature()).toBe(true);
    });
    ```
4. Update hooks or utility files as needed.

---

### Add or Update API Endpoint and Tests

**Trigger:** When adding a new endpoint or changing endpoint behavior.  
**Command:** `/add-endpoint`

1. Create or update handler file in `packages/runtime/src/v2/runtime/handlers/`.
    ```typescript
    // handler.ts
    export default function handler(req, res) { ... }
    ```
2. Create or update test file in `packages/runtime/src/v2/runtime/__tests__/`.
    ```typescript
    // handler.test.ts
    import handler from '../handlers/handler';

    test('handler returns expected result', () => { ... });
    ```
3. Update index or related files if needed.

---

### Add or Update React Hook and Tests

**Trigger:** When introducing new stateful logic or utility for React components.  
**Command:** `/add-hook`

1. Create or update hook file in `packages/react-core/src/v2/hooks/`.
    ```typescript
    // useNewFeature.ts
    export function useNewFeature() { ... }
    ```
2. Add or update test file in `hooks/__tests__/`.
    ```typescript
    // useNewFeature.test.tsx
    import { renderHook } from '@testing-library/react';
    import { useNewFeature } from '../useNewFeature';

    test('useNewFeature behaves correctly', () => { ... });
    ```
3. Export hook in `hooks/index.ts`:
    ```typescript
    export * from './useNewFeature';
    ```

---

### Integration Example Addition or Expansion

**Trigger:** When adding support for a new integration or updating example coverage.  
**Command:** `/add-integration-example`

1. Add or update `Dockerfile(s)` and `docker-compose.test.yml` in `examples/integrations/*/`.
2. Add or update `fixtures/default.json`.
3. Add or update minimal backend/frontend code, e.g.:
    - `agent/main.py`
    - `src/app/api/copilotkit/route.ts`
4. Update `package.json` or config files as needed.

---

### Docs Integration Section Addition

**Trigger:** When a new integration is supported and needs documentation.  
**Command:** `/add-docs-integration`

1. Create documentation landing page and metadata:
    - `docs/content/docs/integrations/[integration]/index.mdx`
    - `docs/content/docs/integrations/[integration]/meta.json`
2. Add quickstart and feature pages:
    - `docs/content/docs/integrations/[integration]/*.mdx`
3. Update integration selector, grid, and navigation components:
    - `docs/components/ui/integrations-sidebar/integration-selector.tsx`
    - `docs/components/content/integration-grid.tsx`
    - `docs/components/react/quickstart-dropdown.tsx`
4. Update `docs/next.config.mjs` or middleware for routing.

---

### Test Suite Expansion or Review Feedback

**Trigger:** When increasing test coverage or after code review.  
**Command:** `/expand-tests`

1. Add or update test files for features or edge cases:
    - `packages/*/src/**/__tests__/*.test.ts*`
    - `sdk-python/tests/*.py`
2. Extract helpers or constants for reuse.
3. Refactor test code for clarity or DRYness.

---

### Docs Sync or Auto-Formatting

**Trigger:** When keeping docs in sync or enforcing code style.  
**Command:** `/sync-docs`

1. Update documentation files or scripts:
    - `docs/content/docs/**/*.mdx`
    - `docs/scripts/*.ts`
2. Apply formatting fixes to code or docs.
3. Update workflow files as needed:
    - `.github/workflows/*.yml`

---

## Testing Patterns

- **Framework:** [Vitest](https://vitest.dev/)
- **Test file pattern:** `*.test.ts` (or `*.test.tsx` for React)
- **Typical structure:**
    ```typescript
    import { myFunction } from '../myFunction';

    test('myFunction returns correct value', () => {
      expect(myFunction(2)).toBe(4);
    });
    ```
- **Location:** Tests are placed in `__tests__` folders adjacent to source code.

## Commands

| Command                  | Purpose                                                                 |
|--------------------------|-------------------------------------------------------------------------|
| /bump-version            | Bump package versions and update changelogs for release                 |
| /add-feature-multi       | Add or update a feature across multiple packages                        |
| /add-endpoint            | Add or update an API endpoint and its tests                             |
| /add-hook                | Add or update a React hook and its tests                                |
| /add-integration-example | Add or expand an integration example                                    |
| /add-docs-integration    | Add a new integration section to the documentation                      |
| /expand-tests            | Expand test coverage or address review feedback                         |
| /sync-docs               | Sync documentation or auto-fix formatting                               |
```
