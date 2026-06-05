# ffmpeg-static

Pinned mirror of [John Van Sickle's ffmpeg static builds](https://johnvansickle.com/ffmpeg/),
republished as GitHub release assets so PLA build pipelines don't
depend on a single-maintainer site at deploy time.

## How consumers use it

Build scripts download a versioned asset and verify it against a
sha256 pin they carry themselves:

```
https://github.com/publicala/ffmpeg-static/releases/download/ffmpeg-<version>/ffmpeg-<version>-<arch>-static.tar.xz
```

Arch is `amd64` or `arm64`. The consumer's checksum pin is the source
of truth. This mirror is an availability contingency, not a trust
anchor: a tampered or corrupted asset fails the consumer's checksum
verification exactly like a tampered upstream download would.

## Adding a version

1. Download both arch tarballs from upstream (`releases/` carries the
   current version, `old-releases/` the superseded ones).
2. Verify them against upstream's published `.md5` files.
3. Create the release:

   ```bash
   gh release create ffmpeg-<version> \
     --title "ffmpeg <version> (static)" \
     --notes "sha256 lines and the upstream source link" \
     ffmpeg-<version>-amd64-static.tar.xz \
     ffmpeg-<version>-arm64-static.tar.xz
   ```

Assets keep upstream's exact bytes. Never re-compress or rename
beyond the versioned filename pattern.

## Licensing

ffmpeg is licensed under the GPL. These builds are redistributed
unmodified from upstream, which publishes its build configuration and
source links at <https://johnvansickle.com/ffmpeg/>. The
corresponding source for each release is the matching ffmpeg release
at <https://ffmpeg.org/download.html>.
