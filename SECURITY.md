# Security Policy

## Reporting a vulnerability

Open a **private security advisory** on GitHub. Don't open a public
issue for security reports.

What helps: the build (Release/Debug), Windows version, and steps to
reproduce.

## What counts

This is an injected DLL that hooks game functions. The honest attack
surface:

- **Hook handling.** The DX11 vtable swap and the CreateMove hook
  (MinHook + signature scan) touch foreign code. A bug that corrupts
  memory outside the intended hook targets is in scope.
- **Offset parsing.** `offsets.h` and the generated SDK headers are
  synced from cs2-dumper output. If a malformed offset value can be
  turned into an arbitrary write, that's in scope.
- **Unload path.** `END` reverts all hooks before the DLL is freed —
  an unsafe unload is in scope.

Not security issues:

- Getting detected by VAC or banned from CS2. That's the documented
  risk of running this, not a vulnerability — see the Disclaimer in
  the README.
- Stale offsets after a CS2 update. That's maintenance (see
  "Updating Offsets" in the README).
- Anything in vendored third-party code (`imgui-master`,
  `minhook-master`, `stb_image.h`) — report upstream.

## Scope

In scope: this repo's own code — the DLL, hooks, features, menu.

Out of scope: third-party libraries, CS2 itself, Steam / VAC.

## What to expect

Indie project, no bug bounty, no SLA. I'll acknowledge your report,
fix confirmed issues, and credit you unless you'd rather stay
anonymous.
