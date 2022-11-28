# Installing CoreOS on Bare Metal

This guide provides instructions to install Fedora CoreOS to bare metal
  
## Prerequisite

Ignition configuration file

  1. Get file "ignition.yml" and replace the parameters in environment variables as your actual
  2. Convert the YML file into a JSON Ignition config:
     docker run -i --rm quay.io/coreos/fcct --pretty --strict < ignition.yml > ignition.ign
  3. Validate config:
     docker run -i --rm quay.io/coreos/ignition-validate - < ignition.ign
  
## Installing from live ISO

To install FCOS onto bare metal using the live ISO interactively
  
  1. Download the latest ISO image from the download [page](https://getfedora.org/coreos/download?tab=metal_virtualized&stream=stable)
  2. Burn the ISO to disk. On Linux and macOS, you can use dd. On Windows, you can use Rufus in "DD Image" mode.
  3. Boot it on the target system. The ISO is capable of bringing up a fully functioning FCOS system purely from memory (i.e. without using any disk storage). Once booted, you will have access to a bash command prompt.
  4. Install FCOS to disk storage:
     sudo coreos-installer install /dev/sda --ignition-url https://example.com/example.ign
  5. Once the installation is complete, you can simply sudo reboot. After rebooting, the first boot process begins. It is at this time that Ignition ingests the configuration file and provisions the system as specified.
