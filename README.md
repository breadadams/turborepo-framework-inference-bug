# Turborepo framework inference bug

This repro exhibits a problem in Turborepo (currently `v2.5.6`) regarding framework inference, for the following issue: https://github.com/vercel/turborepo/issues/10826

## Steps to reproduce

1. Perform regular setup, i.e. `npm i` + install Turbo globally.
2. Run `turbo build` to create base cache entries.
3. ❌ Run `VITE_FOO=1 turbo build`, and see that `pkg-a` and `app-a` are **cache misses**.
4. ❌ Run `VITE_FOO=2 turbo build`, and as above, `pkg-a` and `app-a` are **cache misses**.
5. ✅ Run `VITE_FOO=3 turbo build --framework-inference=false`, `pkg-a` and `app-a` are **cache misses**.
6. ✅ Run `VITE_FOO=4 turbo build --framework-inference=false`, `pkg-a` and `app-a` are **cache hits** (full turbo).
7. ✅ Run `VITE_FOO=5 turbo build --framework-inference=false`, `pkg-a` and `app-a` are **cache hits** (full turbo).

## What is expected

1. Perform regular setup, i.e. `npm i` + install Turbo globally.
2. Run `turbo build` to create base cache entries.
3. Run `VITE_FOO=1 turbo build`, and see that `pkg-a` and `app-a` are **cache hits** (full turbo).
