Releasing Catatumbo
===================

Releases are automated via GitHub Actions. Pushing a tag triggers the release workflow, which
builds, signs, and publishes the artifacts directly to Maven Central.

Prerequisites
-------------

The following secrets must be configured in the GitHub repository settings:

| Secret | Description |
|---|---|
| `OSSRH_USERNAME` | Sonatype OSSRH username |
| `OSSRH_TOKEN` | Sonatype OSSRH token/password |
| `GPG_PRIVATE_KEY` | Armored GPG private key (`gpg --export-secret-keys --armor <key-id>`) |
| `GPG_PASSPHRASE` | Passphrase for the GPG key |

Procedure
---------

1. Make sure all changes are checked in and the build is passing.
2. Update the version in `pom.xml` from `X.Y.Z-SNAPSHOT` to `X.Y.Z`.
3. Commit: `git commit -am "Prepare release X.Y.Z"`
4. Tag: `git tag catatumbo-X.Y.Z`
5. Push the commit and tag: `git push && git push --tags`
6. The `Release` GitHub Actions workflow will trigger automatically, build the artifacts, sign
   them with GPG, and publish them to Maven Central.
7. Verify the new version is available on
   [Maven Central](https://mvnrepository.com/artifact/com.jmethods/catatumbo). The artifacts are
   available on Sonatype almost immediately, but propagation to the Maven Central CDN and mirrors
   (including `search.maven.org` and `mvnrepository.com`) typically takes 30 minutes to a few
   hours.
8. Update the version in `pom.xml` to `X.Y+1.0-SNAPSHOT` and commit:
   `git commit -am "Prepare for next development iteration"`
