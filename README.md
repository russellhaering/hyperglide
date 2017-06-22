# Hyperglide

[Glide](https://github.com/Masterminds/glide) is a tool that makes it easy to manage `vendor` directories in Go.

Hyperglide is an opinionated wrapper around Glide which supports only three operations:

1. Updating every non-pinned dependency to the latest master (`hyperglide up`)
2. Updating a single dependency to the latest master (`hyperglide up <package>`)
3. Installing new dependencies, and only new dependencies (`hyperglide newdep`)

## How it Works

### Updating Dependencies

When you run `hyperglide up`, hyperglide:

1. Backs up your `glide.yaml`
2. Generates a new one which forces every unpinned dependency referenced in `glide.lock` to master
3. Runs `glide update -v`
4. Restores your `glide.yaml`

This mostly exists as a workaround to [this issue](https://github.com/Masterminds/glide/issues/592).

### New Dependencies

When you run `hyperglide newdep`, hyperglide:

1. Backs up your `glide.yaml`
2. Generates a new one which forces every dependency to the version referenced in `glide.lock`
3. Runs `glide update -v`
4. Restores your `glide.yaml`

This will cause Glide to vendor any new dependencies referenced in your repository, without updating existing ones.