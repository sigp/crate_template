This repo contains boilerplate files for spinning up a new Rust crate following Sigma Prime conventions.

## Crate Metadata

Ensure to include the following fields in your `Cargo.toml`:

```
edition = "2021"
license = "Apache 2.0"
readme = "README.md"
description = ""
repository = "https://github.com/sigp/$crate_name"
documentation = "https://docs.rs/$crate_name"
keywords = ["ethereum"]
categories = ["cryptography::cryptocurrencies"]
```

Edit the above template as appropriate.

You can find suitable categories here:

- https://crates.io/category_slugs

## Publishing (Setup)

To set up crate publishing, obtain a `crates.io` API token from https://crates.io/settings/tokens
or re-use an existing one.

Set it as a secret called `CARGO_REGISTRY_TOKEN` on the repository.

Add the `.github/workflows/release.yml` workflow to the repository.

Afer publishing for the first time (see below), assign ownership to the `sigp/crates-io` team:

```
cargo owner --add github:sigp:crates-io $crate_name
```

## Publishing (Process)

Set the version in `Cargo.toml` to the version you wish to publish. Ensure this is pushed to the
`main` branch (preferably by a pull request).

With the `main` branch checked out and up-to-date, run:

```
cargo publish --dry-run
```

You should not see any errors.

Then tag the new release:

```
git tag -s v1.0.0 -m v1.0.0
```

- Use a tag name starting with `v`
- Use `-s` to sign the tag
- Use `-m` to set the message equal to the tag name

Sanity check with:

```
git show --show-signature v1.0.0
```

Then push:

```
git push origin v1.0.0
```

GitHub actions will take it from there.

If it fails spuriously you can try re-running the publish job. If that doesn't work, you should
cut a new release with a new tag.
