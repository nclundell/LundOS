# Installation
Currently available images are:
  - lundos-gnome
  - lundos-hyprland

To rebase an existing atomic Fedora installation to the latest build:

- First rebase to the unsigned image, to get the proper signing keys and policies installed:
  ```
  rpm-ostree rebase ostree-unverified-registry:ghcr.io/nclundell/$(imagename):latest
  ```
- Reboot to complete the rebase:
  ```
  systemctl reboot
  ```
- Then rebase to the signed image, like so:
  ```
  rpm-ostree rebase ostree-image-signed:docker://ghcr.io/nclundell/$(imagename):latest
  ```
- Reboot again to complete the installation
  ```
  systemctl reboot
  ```

To build an ISO:
  - Install the BlueBuild CLI tool
  ```
  podman run --pull always --rm ghcr.io/blue-build/cli:latest-installer | bash
  ```
  - Run the BlueBuild ISO generator:
  ```
  sudo bluebuild generate-iso --iso-name $(image_name).iso image ghcr.io/nclundell/$(imagename)
  ```
