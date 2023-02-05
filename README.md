# ts-expect-error issue for duplicated files

There are 3 packages here: `package-a`, `package-b`, and `package-c`.

`package-b` depends on `package-a`.

`package-c` depends on both `package-a` and `package-b`.

## Reproduction steps

```
// in package-b
npm install
npm link

// in package-c
npm install
npm link @lamnhh/package-b

// in package-c
npm run typecheck
```

The expected result is that `typecheck` passes. The actual result is:

```
> typecheck
> tsc --noEmit

../package-b/node_modules/@lamnhh/package-a/index.ts:1:1 - error TS2578: Unused '@ts-expect-error' directive.

1 // @ts-expect-error global
  ~~~~~~~~~~~~~~~~~~~~~~~~~~


Found 1 error in ../package-b/node_modules/@lamnhh/package-a/index.ts:1
```
