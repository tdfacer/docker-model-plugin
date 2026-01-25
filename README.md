# docker-model-plugin AUR Package

AUR package for [Docker Model Runner](https://github.com/docker/model-runner) - a Docker CLI plugin for managing and running AI models in containers.

## Installation

### From AUR

```bash
# Using an AUR helper (e.g., yay, paru)
yay -S docker-model-plugin

# Or manually
git clone https://aur.archlinux.org/docker-model-plugin.git
cd docker-model-plugin
makepkg -si
```

### Usage

Once installed, the plugin is available as a Docker CLI subcommand:

```bash
# List available models
docker model list

# Pull a model
docker model pull ai/smollm2

# Run a model
docker model run ai/smollm2 "Hello, how are you?"

# Interactive chat
docker model run ai/smollm2

# Get help
docker model --help
```

## Package Details

| Field | Value |
|-------|-------|
| Package Name | `docker-model-plugin` |
| Binary | `/usr/lib/docker/cli-plugins/docker-model` |
| License | Apache-2.0 |
| Upstream | https://github.com/docker/model-runner |

## Updating for New Releases

```bash
# Update version in PKGBUILD
vim PKGBUILD
# Change: pkgver=X.Y.Z
# Reset: pkgrel=1

# Update checksums
updpkgsums

# Test build
makepkg -sf

# Regenerate .SRCINFO
makepkg --printsrcinfo > .SRCINFO

# Commit and push
git add PKGBUILD .SRCINFO
git commit -m "Update to version X.Y.Z"
git push origin master      # GitHub mirror
git push aur master         # AUR
```

## Testing in Clean Chroot

```bash
# Create chroot (one-time setup)
mkdir ~/chroot
mkarchroot ~/chroot/root base-devel

# Build in clean environment
makechrootpkg -c -r ~/chroot
```

## Troubleshooting

### "docker model" command not found
- Verify Docker is installed: `docker --version`
- Check plugin exists: `ls /usr/lib/docker/cli-plugins/docker-model`
- Restart Docker daemon: `sudo systemctl restart docker`

### Build fails with module errors
- Ensure Go 1.25+ is installed: `go version`
- Check internet connectivity for module downloads

### Tests fail during check()
- Some tests require Docker runtime
- Build continues with a warning if tests fail

## Links

- **Upstream**: https://github.com/docker/model-runner
- **Documentation**: https://docs.docker.com/ai/model-runner/
- **AUR Package**: https://aur.archlinux.org/packages/docker-model-plugin

## Maintainer

Trevor Facer <trevordf@protonmail.com>
