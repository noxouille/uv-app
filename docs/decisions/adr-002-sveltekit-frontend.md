# ADR-002: Frontend Framework Selection — SvelteKit 5

**Status**: ✅ Accepted  
**Date**: 2025-04-08  
**Deciders**: Product Owner

---

## Context

We need to select a frontend framework for the Meal Planning PWA. The choice should support:

- Progressive Web App (PWA) capabilities
- Mobile-first responsive design
- Good developer experience for AI agent collaboration
- Type safety
- Form handling and validation

## Decision

**Use SvelteKit 5** as the frontend framework.

### Rationale

| Factor               | SvelteKit 5 Advantage                                          |
| -------------------- | -------------------------------------------------------------- |
| **Simplicity**       | Less boilerplate than React, simpler component syntax          |
| **Performance**      | Compiled to vanilla JS, smaller bundle size                    |
| **PWA Support**      | Built-in service worker support, easy manifest configuration   |
| **State Management** | Svelte 5 Runes ($state, $derived) — no external library needed |
| **Form Handling**    | Native progressive enhancement, server-side form actions       |
| **Type Safety**      | First-class TypeScript support                                 |
| **AI Friendly**      | Clear, concise code patterns easy for AI agents to generate    |

### Stack Details

| Component       | Choice                                      |
| --------------- | ------------------------------------------- |
| **Framework**   | SvelteKit 5 (Svelte 5 with runes)           |
| **Language**    | TypeScript                                  |
| **Styling**     | Tailwind CSS                                |
| **Forms**       | Superforms + Zod                            |
| **Icons**       | Lucide-svelte or Heroicons                  |
| **HTTP Client** | Native fetch (via SvelteKit load functions) |

## Alternatives Considered

### React + Next.js

- **Pros**: Huge ecosystem, many examples
- **Cons**: More complex, heavier bundle, need external state management
- **Verdict**: Good but overkill for our MVP

### Vue + Nuxt

- **Pros**: Gentle learning curve, good docs
- **Cons**: Smaller ecosystem than React/Svelte
- **Verdict**: Good alternative, but SvelteKit edges ahead for PWA

### Pure Svelte (no Kit)

- **Pros**: Lightweight
- **Cons**: Missing routing, SSR, and other app features we'd need to add
- **Verdict**: SvelteKit provides everything we need out of the box

## Consequences

### Positive

- Faster development due to less boilerplate
- Smaller bundle size = faster PWA load times
- Built-in form handling reduces complexity
- Server-side rendering improves SEO (if needed later)

### Trade-offs

- Smaller ecosystem than React (but still well-supported)
- Fewer third-party libraries (though most needs are covered)
- Team may need to learn Svelte syntax (minimal for AI agents)

## Implementation Notes

### Project Structure

```
frontend/
├── src/
│   ├── app.html              # HTML template
│   ├── app.d.ts              # TypeScript declarations
│   ├── lib/                  # Shared components & utilities
│   │   ├── components/       # Svelte components
│   │   ├── stores/           # Svelte stores (if needed)
│   │   └── schemas/          # Zod schemas
│   ├── routes/               # SvelteKit file-based routing
│   │   ├── +layout.svelte    # Root layout
│   │   ├── +page.svelte      # Home page
│   │   ├── profile/          # Profile routes
│   │   │   ├── +page.svelte  # Profile form
│   │   │   └── +page.server.ts # Server-side form handling
│   │   └── api/              # API proxy routes (if needed)
│   └── static/               # Static assets
│       ├── manifest.json     # PWA manifest
│       └── icons/            # App icons
├── svelte.config.js          # Svelte configuration
├── vite.config.ts            # Vite + Tailwind config
├── tailwind.config.js        # Tailwind CSS config
└── package.json
```

### Key Patterns

#### Component Example

```svelte
<!-- ProfileForm.svelte -->
<script lang="ts">
  import { superForm } from 'sveltekit-superforms';
  import { zod } from 'sveltekit-superforms/adapters';
  import { profileSchema } from '$lib/schemas/profile';

  let { data } = $props();

  const { form, errors, enhance, submitting } = superForm(data.form, {
    validators: zod(profileSchema)
  });
</script>

<form method="POST" use:enhance>
  <label>
    Adults
    <input
      type="number"
      name="adults_count"
      bind:value={$form.adults_count}
    />
    {#if $errors.adults_count}
      <span class="error">{$errors.adults_count}</span>
    {/if}
  </label>

  <button type="submit" disabled={$submitting}>
    {$submitting ? 'Saving...' : 'Save Profile'}
  </button>
</form>
```

#### Server-Side Form Handling

```typescript
// routes/profile/+page.server.ts
import { superValidate } from "sveltekit-superforms";
import { zod } from "sveltekit-superforms/adapters";
import { profileSchema } from "$lib/schemas/profile";
import { fail } from "@sveltejs/kit";

export const load = async () => {
  const form = await superValidate(zod(profileSchema));
  return { form };
};

export const actions = {
  default: async ({ request }) => {
    const form = await superValidate(request, zod(profileSchema));

    if (!form.valid) {
      return fail(400, { form });
    }

    // Save to API
    await saveProfile(form.data);

    return { form };
  },
};
```

## References

- [SvelteKit Documentation](https://kit.svelte.dev/)
- [Svelte 5 Runes](https://svelte.dev/blog/runes)
- [Superforms](https://superforms.rocks/)
- [SvelteKit PWA Guide](https://vite-pwa-org.netlify.app/frameworks/sveltekit.html)

---

_Related: ADR-001 (Backend Stack)_
