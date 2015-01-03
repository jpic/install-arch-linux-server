# Install Arch Linux on a headless server through a booted Ubuntu live

Some ISPs like online.net do not provide an installer for Arch Linux.
However, we can boot the "rescue os" which is a live ubuntu system, and
follow [Arch Linux documentation "Install from Existing
Linux"](https://wiki.archlinux.org/index.php/Install_from_Existing_Linux)

## Usage

Format [`/dev/sda` to BtrFS Partionning](https://wiki.archlinux.org/index.php/partitioning#Btrfs_Partitioning) and install arch linux in subvolumes:

    ansible-playbook -i "yourhostname," --ask-sudo-pass rescue_reinstall_arch_linux.yml

If you just want to debug your arch root on `/dev/sda` through Ubuntu Live,
then this command will make it operationnal in /tmp/root.x86_64/mnt:

    ansible-playbook -i "yourhostname," --ask-sudo-pass rescue_mount_arch_linux.yml
    # you may chroot /tmp/root.x86_64/mnt on the server now and have a working arch

If you just want to build an [Arch Linux
chroot](https://wiki.archlinux.org/index.php/Install_from_Existing_Linux#Creating_the_chroot) in `/tmp/root.x86_64` by default:

    ansible-playbook -i "yourhostname," --ask-sudo-pass rescue_arch_linux_chroot.yml

It's ansible, you can override any variable you find in
`roles/rescue/vars/main.yml` with `-e 'var=bar'`.
