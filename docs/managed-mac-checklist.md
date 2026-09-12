# Nexus Shell: a pilot checklist for managed Macs

For Mac administrators evaluating the official AutoPkg/Munki recipes. This is deployment documentation maintained by the product developer; it does not claim organization-wide licensing or an end-to-end test of your environment.

## 1. Review and download

Review [the download recipe](../NexusShell/NexusShell.download.recipe), then create a local override so parent changes can be detected:

```sh
autopkg repo-add viewer12/nexusshell-recipes
autopkg make-override NexusShell.download
autopkg verify-trust-info NexusShell.download
autopkg run NexusShell.download -k FAIL_RECIPES_WITHOUT_TRUST_INFO=yes
```

The recipe checks the Developer ID signature, bundle identifier `sameral.Nexus-Shell`, Team ID `5MBFAB57U2` and strict signing validity. Successful download is not fleet installation, malware certification or permission to ignore your software review.

## 2. Stage in Munki

Use an already configured, writable test Munki repository. Review [the Munki recipe](../NexusShell/NexusShell.munki.recipe), create its override, then import:

```sh
autopkg make-override NexusShell.munki
autopkg verify-trust-info NexusShell.munki
autopkg run NexusShell.munki -k FAIL_RECIPES_WITHOUT_TRUST_INFO=yes
```

Expected defaults: `apps/NexusShell`, `testing` catalog, `minimum_os_version=14.2`, `supported_architectures=[arm64]`, `unattended_install=false`. Check the resulting pkginfo and version, regenerate catalogs through your normal workflow, and assign only a test manifest initially. Importing is not client assignment.

## 3. Verify a useful task

- Launch on one eligible Apple Silicon Mac.
- Configure a test Linux connection using the user's approved credential process.
- Check the feature actually needed by the team: terminal, SFTP, container inspection or monitoring. Packaging success is not feature validation.
- Confirm the commercial license and required Pro entitlement. Free is for personal, non-commercial use; the recipe grants no license.
- Keep server credentials out of recipes and manifests. No central connection provisioning or managed preferences are promised by this recipe.
- Agent Bridge is optional and off by default. Installing the app does not authorize an agent or enable the bridge. Do not enable it across a fleet as a side effect of software delivery.

## 4. Handle updates deliberately

When trust verification fails, inspect upstream changes before updating trust. When the signature check fails, stop and investigate; do not remove the verifier. Keep locally approved artifacts and use your existing Munki version/rollback policy. This recipe follows the selected upstream release and does not implement version pinning or automatic rollback.

The repository's recorded AutoPkg download test used AutoPkg 2.9.1 and Nexus Shell 1.6.9. This checklist does not claim a new latest-release or fleet deployment test.

[Full deployment guide and current product terms](https://nexusshell.app/en/guides/deploy-macos-ssh-client-autopkg-munki/?utm_source=github-recipes&utm_medium=repository&utm_campaign=managed_macs_202609)

[AutoPkg parent trust documentation](https://github.com/autopkg/autopkg/wiki/AutoPkg-and-recipe-parent-trust-info)
