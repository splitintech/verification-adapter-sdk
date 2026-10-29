# Publishing

See [repository release setup](repository-release.md) before enabling publishing. Configure npm trusted publishing for repository `splitintech/verification-adapter-sdk` and workflow `verification-adapter-sdk-publish.yml` for each public workspace package. Preserve package names and publish a new version only when intended. No npm token is required.

From the standalone repository root, after tests, build and packed-consumer checks pass, create a signed tag matching the package version:

```bash
version=$(node -p "require('./package.json').version")
node scripts/assert-release-tag.mjs --tag "verification-adapter-sdk-v$version" --prefix verification-adapter-sdk-v --workspace-root .
git tag -s "verification-adapter-sdk-v$version" -m "verification-adapter-sdk $version"
git push origin "verification-adapter-sdk-v$version"
```

Do this only with a clean working tree and configured Git signing. The workflow requires `NPM_TRUSTED_PUBLISHING_ENABLED=true`, publishes with provenance, and skips versions already in the registry. Existing hub release tags remain historical references.
