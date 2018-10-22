#Zecora

Sync libraries with library wrappers.

## Project goals

There is some external library that you want to include in a package manager. You have no write access, only read. You own the wrapper that makes the library compatible with your package manager of choice.


## How it works

Not all of the description below has been implemented, so consider this a specification for how Zecora will work.

Zecora is a GitHub App. You install it into the repo that contains the library wrapper (right now only Conan is supported). Your repo must contain a `.zecora.json` configuration file, which will tell Zecora where to find the target library to wrap.

- On installation Zecora looks for the `.zecora.json` file, and parses it. Suppose it points to libawesome at https://github.com/DEGoodmanWilson/awesomesauce. Suppose new releases occur on tags with regex pattern `/v\d\.\d\.\d` (_e.g._ `v1.2.3`)

- Zecora then subscribes to `branch` events from the target repo, in this case DEGoodmanWilson/awesomesauce

- When a new tag matching the specified regex is pushed, Zecora creates a new branch `testing/x.y.z` in the wrapper repo.

- In this new branch, Zecora increments the version number in the conanfile

- Zecora pushes the new branch to the repo, then somehow—perhaps via opening an issue—notifies the repo owner

### Edge cases

- Wrapper repos with no `.zecora.json` get tracked, but there's nothing we can do to help. We listen for push events to the repo to see if / when a `.zecora.json` file gets pushed to the main branch, and then record the contents.

- Wrapper repos with a `.zecora.json` file that changes. Because we are listening to push notification on the wrapper repo, we can detect changes to the configuraiton, and act accordingly

- Wrapper repos with badly specified target repos.

- Wrapper repos that track a library not on GitHub