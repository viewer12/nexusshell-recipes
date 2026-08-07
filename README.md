# Nexus Shell AutoPkg Recipes

AutoPkg recipes maintained by the Nexus Shell developer for deploying the official macOS release.

Nexus Shell is a native macOS SSH workspace for Apple silicon Macs. The download recipe reads the latest release from the public `viewer12/Nexus-Shell-Releases` repository and verifies the signed app before completing.

## Add the recipe repository

```sh
autopkg repo-add viewer12/nexusshell-recipes
```

## Download and verify Nexus Shell

```sh
autopkg run NexusShell.download
```

The recipe verifies:

- Bundle identifier: `sameral.Nexus-Shell`
- Developer Team ID: `5MBFAB57U2`
- Apple Developer ID certificate chain
- Strict code-signing validity

Nexus Shell currently requires macOS 14.2 or later on Apple silicon.

Product information and direct downloads are available at [nexusshell.app](https://nexusshell.app/).

## Validation

The recipe was tested with AutoPkg 2.9.1 against Nexus Shell 1.6.9. It selected the expected GitHub release asset, downloaded the DMG, mounted it, and passed strict `CodeSignatureVerifier` validation.

## License

The recipe and repository documentation are available under the MIT License.
