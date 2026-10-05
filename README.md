# prettier-plugin-tailwindcss: Svelte whitespace and duplicates

Minimal reproduction for `prettier-plugin-tailwindcss` leaving extra whitespace and duplicate classes in Svelte `class` attributes.

```bash
pnpm install
pnpm format
```

`src/App.svelte` before formatting:

```svelte
<div class="  sm:flex   underline  block  "></div>
<Button class="  sm:flex   underline  " />
<div class={cn('  sm:flex   underline  ')}></div>
<div class={'flex underline flex'}></div>
```

After `pnpm format`:

```svelte
<div class="  block underline sm:flex"></div>
<Button class="  underline   sm:flex  " />
<div class={cn("  underline   sm:flex  ")}></div>
<div class={"flex flex underline"}></div>
```

Expected, matching what the plugin does for JSX, Vue, and HTML:

```svelte
<div class="block underline sm:flex"></div>
<Button class="underline sm:flex" />
<div class={cn("underline sm:flex")}></div>
<div class={"flex underline"}></div>
```
