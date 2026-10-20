## Updating Dependencies

All modules live in the single manifest `org.tabos.saldo.json`.

The Python packages are pinned as PyPI artifacts (wheels where available) and
were originally generated with
[flatpak-pip-generator](https://github.com/flatpak/flatpak-builder-tools/tree/master/pip).

### Regular Python dependencies

```sh
flatpak-pip-generator --runtime org.gnome.Sdk//51 \
    --requirements-file requirements.txt --output pypi-dependencies
```

Copy the resulting modules into the `modules` array of `org.tabos.saldo.json`.

### cryptography

`cryptography` is installed from its official manylinux wheels (x86_64 and
aarch64) instead of being compiled from source, so no Rust toolchain or SDK
extension is needed:

```sh
flatpak-pip-generator --runtime org.gnome.Sdk//51 \
    --prefer-wheels=cryptography --wheel-arches x86_64,aarch64 cryptography
```

Replace the `python3-cryptography` module with the generated one (both wheel
sources, including their `sha256`). Its runtime dependencies `cffi` and
`pycparser` are installed by the `cryptography-deps` module.

## Building Locally

To build the flatpak the same way it is built on the Flathub build servers run:

```sh
flatpak run org.flatpak.Builder -v --bundle-sources --install-deps-from=flathub --user \
    --force-clean build-dir org.tabos.saldo.json
```
