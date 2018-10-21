#Zecora

Sync libraries with library wrappers.

## Project goals

There is some external library that you want to include in a package manager. You have no write access, only read. You own the wrapper that makes the library compatible with your package manager of choice.

Zecora is the glue that holds all this together.
- Zecora listens for new tags (or branches TODO) on a target library that matches a pattern indicating a new release, e.g. `v5.0.4`
- Zecora makes a new branch on your code, e.g. `testing/v5.0.4`
- Zecora updates the original source download location and bumps the version number in your code, and pushes the new branch, ideally triggering a CI build
