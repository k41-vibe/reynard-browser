# Reynard (LiveContainer ext-host build)

Personal test build of [Reynard Browser](https://github.com/minh-ton/reynard-browser) (GPL-3.0) with one change:

**Child-process launches route through LiveContainer's LiveProcess extension when available** — see `patches/ipc/glue/NSExtensionUtils.mm.patch`. Inside [LiveContainer](https://github.com/LiveContainer/LiveContainer) (the ext-host variant), the `Reynard Helper.appex` child processes are spawned by LiveProcess; regular installations keep using the system extension registry as before.

Branch: `livecontainer-ext-host` (based on upstream `main` at 0.17.0).

Use the upstream repo for documentation, features and support. This build is for personal testing; issues go to upstream.
