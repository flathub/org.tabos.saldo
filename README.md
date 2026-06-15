## Updating Dependencies

1. Install <https://github.com/flatpak/flatpak-builder-tools/tree/master/pip>
2. `flatpak install flathub org.gnome.Platform//50 org.gnome.Sdk//50`
3. `python3 flatpak-pip-generator.py --runtime=org.gnome.Sdk//50 --requirements-file=requirements.txt --prefer-wheels=cryptography`

## Building Locally

To build the flatpak the same way it is built on the Flathub build servers run:

```bash
flatpak run org.flatpak.Builder build-dir --user --ccache --force-clean --install org.tabos.saldo.json
```
