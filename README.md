# go-zenon releases

Signed binary releases of [go-zenon](https://github.com/zenon-network/go-zenon), the Zenon Network node (`znnd`) and its embeddable library (`libznn`).

This repository holds binaries only. It is used when a release has to ship before its source can be published, for example when it contains security fixes. The source for each release is published in [zenon-network/go-zenon](https://github.com/zenon-network/go-zenon), and the binaries are then attached to the matching release there too. The checksums are the same in both places.

## Releases

| Version | Notes |
|---|---|
| [v0.0.10](https://github.com/zenon-network/go-zenon-releases/releases/tag/v0.0.10) | Required upgrade for the community spork renewal. See the [forum post](https://forum.hypercore.one/t/go-zenon-v0-0-10-what-to-expect-at-the-community-spork-renewal/946). |

## Verifying a download

Every release includes `SHA256CHECKSUMS.txt` and a detached signature, `SHA256CHECKSUMS.txt.asc`, made with this key:

```
310A 0EAE A844 9754 CF17  E8BB F6B8 2D11 5587 9DAB
```

The key is published on the signer's GitHub profile at <https://github.com/0x3639.gpg>.

1. Import the key and check the fingerprint matches the one above:

   ```bash
   curl -sL https://github.com/0x3639.gpg | gpg --import
   gpg --fingerprint F6B82D1155879DAB
   ```

2. Download the archive you need, plus `SHA256CHECKSUMS.txt` and `SHA256CHECKSUMS.txt.asc`, into one folder.

3. Check the signature on the checksum file. Look for `Good signature`:

   ```bash
   gpg --verify SHA256CHECKSUMS.txt.asc SHA256CHECKSUMS.txt
   ```

4. Check the archive against the checksum file. Look for `OK`:

   ```bash
   # Linux
   sha256sum --ignore-missing -c SHA256CHECKSUMS.txt
   # macOS
   shasum -a 256 --ignore-missing -c SHA256CHECKSUMS.txt
   ```

   On Windows, compare the output of `Get-FileHash .\znnd-windows-amd64.zip` with the line for that file in `SHA256CHECKSUMS.txt`.

## Archives

| File | Contents |
|---|---|
| `znnd-linux-amd64.tar.gz`, `znnd-linux-arm64.tar.gz` | Node binary for Linux |
| `znnd-darwin-amd64.tar.gz`, `znnd-darwin-arm64.tar.gz`, `znnd-darwin-universal.tar.gz` | Node binary for macOS (Intel, Apple silicon, or both) |
| `znnd-windows-amd64.zip` | Node binary for Windows |
| `libznn-*` | The same node as a shared library, for SDKs and wallets that embed it |
