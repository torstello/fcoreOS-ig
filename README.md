# Installing CoreOS on Bare Metal

This guide provides instructions to install Fedora CoreOS to bare metal
  
## Prerequisites

Ignition configuration file

  1. Get file "ignition.yml" and replace the parameters in environment variables as your actual
  2. Convert the YML file into a JSON Ignition config:
     podman run --interactive --rm quay.io/coreos/butane:release \
     --pretty --strict < ignition.yml > ignition.ign
  2b. If you want to setup a user with a password, generate it with:
      podman run -ti --rm quay.io/coreos/mkpasswd --method=yescrypt
  3. Validate config:
     podman run -i --rm quay.io/coreos/ignition-validate:release - < ignition.ign
  
## Installing from live ISO

To install FCOS onto bare metal using the live ISO interactively
  
  1. Download the latest ISO image from the download [page](https://getfedora.org/coreos/download?tab=metal_virtualized&stream=stable)
  2. Burn the ISO to disk. On Linux and macOS, you can use dd.
  3. Boot it on the target system. The ISO is capable of bringing up a fully functioning
     FCOS system purely from memory (i.e. without using any disk storage).
  4. Install FCOS to disk storage:
     sudo coreos-installer install /dev/sda -i <link to your ignition file>
  5. Once the installation is complete, you can simply sudo reboot. After rebooting, the first boot process begins. It is at this time that Ignition ingests the configuration file and provisions the system as specified.
