# Fork maintenance

This fork adds Apple authentication fixes to upstream commit `3bc9515`.

The source changes come from these pull requests:

- [PR 89](https://github.com/Lakr233/AssppWeb/pull/89), head `835a54d`: browser SAP request signing.
- [PR 91](https://github.com/Lakr233/AssppWeb/pull/91), head `500e1c4`: authentication URL and redirect normalization.

The fork also permits the exact SAP certificate and setup hosts through Wisp.
These hosts are `s.mzstatic.com` and `fpinit.itunes.apple.com`.
Account credentials stay in the browser.
Opening the account list does not start SAP preparation.
Preparation starts only when the user initiates authentication.

The Docker workflow tests both packages before it builds and publishes images.
Images support `linux/amd64` and `linux/arm64`.
The build downloads public Apple program files and verifies their pinned SHA-256 values.
The workflow does not authenticate an Apple account.

The image name is `ghcr.io/ciiiii/assppweb`.
Each build publishes `latest` and a commit tag.
Use an image digest when deploying a verified build.

Local checks do not establish that a real account can authenticate.
Verify account refresh and downloads in the browser before replacing an existing instance.
