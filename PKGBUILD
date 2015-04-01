# Maintainer: Yunhui Fu <yhfudev at gmail dot com>

pkgname=kali-pogoplug-image
pkgver=1.1.0
pkgrel=1
pkgdesc="PogoPlug Kali image"
arch=('i686' 'x86_64' 'arm')
url="https://github.com/yhfudev/arch-kali-pogoplug.git"
license=('GPL')

optdepends=(
    'pixz'
    'bmap-tools'
    'bsdtar'
    )

makedepends=(
    'git' 'bc' 'gcc-libs' 'bash' 'sudo'
    'ncurses' 'lzop' 'uboot-tools' # for kernel
    'qemu' 'qemu-user-static-exp' 'binfmt-support' # cross compile and chroot
    'debootstrap' # to create debian rootfs
    'parted' 'dosfstools'
    'yaourt' 'multipath-tools' # for kpartx, in AUR, you need to use yaourt to install it
    'lib32-libstdc++5' 'lib32-zlib' # for 32 bit compiler
    'base-devel' 'abs' 'fakeroot'
    # 'kernel-package' # debian packages, include make-kpkg
    )
#install="$pkgname.install"
#PKGEXT=.pkg.tar.xz

provides=('kali-pogoplug-image-git')
conflicts=('kali-pogoplug-image')


# config for GoFlex Home/Net, Pogoplug E02/Mobile/V4, iConnect, Dockstar, Sheevaplug, NSA320, NSA325, Topkick,
ARCHITECTURE="armel"
PATCH_MAC80211="kali-arm-build-scripts-git/patches/kali-wifi-injection-3.18.patch"
CONFIG_KERNEL="config-3.19-kirkwood-yhfu-3"
CONFIG_KERNEL="config-3.18.5-kirkwood-tld-1"
PATCH_CONFIG_KERNEL="pogoplug-kernel-config.patch"
MAKE_CONFIG=kirkwood_defconfig


# Package installations for various sections.
# This will build a minimal XFCE Kali system with the top 10 tools.
# This is the section to edit if you would like to add more packages.
# See http://www.kali.org/new/kali-linux-metapackages/ for meta packages you can
# use. You can also install packages, using just the package name, but keep in
# mind that not all packages work on ARM! If you specify one of those, the
# script will throw an error, but will still continue on, and create an unusable
# image, keep that in mind.
PACKAGES_ARM="abootimg cgpt fake-hwclock ntpdate vboot-utils vboot-kernel-utils uboot-mkimage"
PACKAGES_BASE="initramfs-tools sudo parted e2fsprogs usbutils nfs-common lsb-release ntfs-3g usbmount hdparm tmux wpasupplicant"
PACKAGES_TOOLS="passing-the-hash winexe aircrack-ng hydra john sqlmap libnfc-bin mfoc nmap ethtool"
PACKAGES_SERVICES="openssh-server"
#PACKAGES_DESKTOP="kali-menu kali-defaults xfce4 network-manager network-manager-gnome xserver-xorg-video-fbdev"
#PACKAGES_TOOLS_GUI="wireshark iceweasel"
#PACKAGES_ADDON="apache2 fruitywifi xfce4-goodies kali-linux-full"
export PACKAGES="${PACKAGES_ARM} ${PACKAGES_BASE} ${PACKAGES_DESKTOP} ${PACKAGES_TOOLS} ${PACKAGES_SERVICES} ${PACKAGES_TOOLS_GUI} ${PACKAGES_ADDON}"

# the image container size
IMGCONTAINER_SIZE=3000 # Size of image in megabytes
#IMGCONTAINER_SIZE=7000 # MB, size of kali-linux-full

# If you have your own preferred mirrors, set them here.
# You may want to leave security.kali.org alone, but if you trust your local
# mirror, feel free to change this as well.
# After generating the rootfs, we set the sources.list to the default settings.
export INSTALL_MIRROR=http.kali.org
export INSTALL_SECURITY=security.kali.org

# the /boot path for u-boot
MNTPOINT_BOOT_FIRMWARE=/boot/firmware/
# the root fs / label
DISKLABEL_ROOTFS=rootfs
# the /boot fs label
DISKLABEL_BOOTFS=BOOTFS


DNSRC_UBOOT_HARDKERNEL=uboot-hardkernel-git
GITCOMMIT_UBOOT_HARDKERNEL=f631c80969b33b796d2d4c077428b4765393ed2b

DNSRC_UBOOT_KIRKWOOD=uboot-kirkwood-git
GITCOMMIT_UBOOT_KIRKWOOD=bb8ac0e067f6f42d8832c11c9266707bcba419f9

#GITCOMMIT_LINUX=c193f5d80656ce6d471cf3a28fe8259b3e3a02c0
GITCOMMIT_LINUX=3.18
DNSRC_LINUX=linux-${GITCOMMIT_LINUX}

GITCOMMIT_UBOOT=${GITCOMMIT_UBOOT_KIRKWOOD}
DNSRC_UBOOT=u-boot-${GITCOMMIT_UBOOT}
DNSRC_UBOOT=u-boot-kirkwood-${GITCOMMIT_UBOOT}
USE_GIT_REPO=0
#DNSRC_UBOOT=${DNSRC_UBOOT_HARDKERNEL}
#DNSRC_LINUX=linux-hardkernel-git


_SRCNAME_LINUX=linux-3.18
_PKGVER_LINUX=3.18.5
_PKGBASE_LINUX=linux
_PKGREL_LINUX=1
_kernelname=${_PKGBASE_LINUX#linux}


source=(
        "https://www.kernel.org/pub/linux/kernel/v3.x/${_SRCNAME_LINUX}.tar.xz" # "${DNSRC_LINUX}::git+https://github.com/hardkernel/linux.git"
        "https://www.kernel.org/pub/linux/kernel/v3.x/patch-${_PKGVER_LINUX}.xz"

        "firmware-linux-git::git+https://git.kernel.org/pub/scm/linux/kernel/git/firmware/linux-firmware.git"

        # http://forum.doozan.com/read.php?2,12096,12096
        "linux-3.18.5-kirkwood-tld-1.patch"
        "linux-3.19-kirkwood-tld-1.patch"
        "kali-wifi-injection-3.19.patch" #"kali-arm-build-scripts-git::git+https://github.com/offensive-security/kali-arm-build-scripts.git"

        "config-3.18.5-kirkwood-tld-1"
        "config-3.19-kirkwood-yhfu-3"

        "kali-arm-build-scripts-git::git+https://github.com/offensive-security/kali-arm-build-scripts.git"

        # u-boot
        # instruction to flash u-boot to device: http://forum.doozan.com/read.php?3,12381
        "https://github.com/mibodhi/u-boot-kirkwood/archive/${GITCOMMIT_UBOOT_KIRKWOOD}.tar.gz" # "${DNSRC_UBOOT_KIRKWOOD}::git+https://github.com/mibodhi/u-boot-kirkwood.git"
        #"http://dn.odroid.com/toolchains/gcc-linaro-arm-none-eabi-4.8-2014.04_linux.tar.xz"

        "debian-systemstart.sh"
        "debian-zram.sh"
        "bash.bashrc.template"
        )

md5sums=(
         '9e854df51ca3fef8bfe566dbd7b89241' # linux
         'e8563b2feaa6c33d20d23ac7add9d385' # patch for linux
         'SKIP' # firmware-linux-git
         'fc4929003fbe7013173c450496843503' # linux-3.18.5-kirkwood-tld-1.patch
         'f26bbdfa630138826f48d393f23a0dfb' # linux-3.19-kirkwood-tld-1.patch
         '48b5da35a73f01d24ecb7735f3ab6c4c' # kali-wifi-injection-3.19.patch
         '7c9988bc1be5006acd89886959cdb38c' # config-3.18.5-kirkwood-tld-1
         '7d17ef55604aa9a1dfd0159727dcb395' # config-3.19-kirkwood-yhfu-3
         'SKIP' # kali-arm-build-scripts-git
         '9ef85adf8bea5ef2e967c9cef827c249' # u-boot
         #'12d6e8a0cbd2d8e130cc8f55389a95c3' # gcc for uboot
         'f488b18bc2ab3bfda4efda2b8f5f773b' # debian-systemstart.sh
         '3793439a6f13115f2251e782646ee8e6' # debian-zram.sh
         'c57652f7e448ecf85d99326fe2e04865' # bash.bashrc.template
         )
sha1sums=(
         '4557ef53c89fe70a9da230ae1e6542856d8b0a94' # linux
         'f13c27974ca7d40b9ba59efd0193d915d595813c' # patch for linux
         'SKIP' # firmware-linux-git
         '2a41d01eb6af4d92eb13cbbb8d129812b924b246' # linux-3.18.5-kirkwood-tld-1.patch
         '6feb050bedbbe9fd67000bc6b1356ccf81c9cbc3' # linux-3.19-kirkwood-tld-1.patch
         'b97d9d19b89b7df9d7992e3cb3715892e7bb37b8' # kali-wifi-injection-3.19.patch
         '2a9bcb6626936b00f50dff2ed98f0ca99b86b95c' # config-3.18.5-kirkwood-tld-1
         '1a14482ec0c250bd3dcda34f60fb6312195119e6' # config-3.19-kirkwood-yhfu-3
         'SKIP' # kali-arm-build-scripts-git
         '59bbb6103b1cb73b3bc0fff8a3f04e96a03fdd80' # u-boot
         #'8069f484cfd5a7ea02d5bb74b56ae6c99e478d13' # gcc for uboot
         '37f7c678e300b433aa2f0319f63065784dd056da' # debian-systemstart.sh
         'ab5a6304d3e3ca5b315cff0bfa25558e38520100' # debian-zram.sh
         'd41cad5f9c329373063e510d5910dc41513ae653' # bash.bashrc.template
         )

pkgver() {
    cd "${srcdir}/kali-arm-build-scripts-git"
    local ver="$(git show | grep commit | awk '{print $2}'  )"
    #printf "r%s" "${ver//[[:alpha:]]}"
    echo ${ver:0:7}
}

PREFIX_TMP="${srcdir}/tmptmp-${pkgname}"

FORMAT_NAME='arm'
FORMAT_MAGIC='\x7fELF\x01\x01\x01\x00\x00\x00\x00\x00\x00\x00\x00\x00\x02\x00\x28\x00'
FORMAT_MASK='\xff\xff\xff\xff\xff\xff\xff\x00\xff\xff\xff\xff\xff\xff\xff\xff\xfe\xff\xff\xff'
FORMAT_INTERP='/usr/bin/qemu-arm-static'
FORMAT_REGISTRATION=":$FORMAT_NAME:M::$FORMAT_MAGIC:$FORMAT_MASK:$FORMAT_INTERP:"
BINFMT_MISC="/proc/sys/fs/binfmt_misc"

register_qemuarm() {
    # Check if format is not registered already
    if [ ! -f "$BINFMT_MISC/$FORMAT_NAME" ]; then
        echo "Registering arm binfmt_misc support"
        echo "echo '$FORMAT_REGISTRATION' > /proc/sys/fs/binfmt_misc/register" | sudo sh
    else
        echo "Format $FORMAT_NAME already registered."
    fi
}

unregister_qemuarm() {
    # We were asked to drop the registration
    if [ -f "$BINFMT_MISC/$FORMAT_NAME" ]; then
        echo "echo -1 > '$BINFMT_MISC/$FORMAT_NAME'" | sudo sh
    else
        echo "Format $FORMAT_NAME not registered."
    fi
}

# since the apt-get place lock in $ROOTFS/var/cache/apt/archives
# we need to seperate the dir from multiple instances if we want to share the apt cache
# so we place *.deb and lock file into two folders in ${SRCDEST}/apt-cache-armhf and ${srcdir}/apt-cache-armhf seperately

# link the *.deb from ${SRCDEST}/apt-cache-armhf to ${srcdir}/apt-cache-armhf
aptcache_link2srcdst() {
    # the dir stores the real files
    PARAM_DN_BASE=$1
    shift
    # the dir contains the symbol links
    PARAM_DN_LINK=$1
    shift

    cd "${PARAM_DN_LINK}"
    find "${PARAM_DN_BASE}" -name "*.deb" -type f | while read i; do
        FN="$(basename ${i})"
        sudo rm -f "${FN}"
        sudo ln -s "${i}" "${FN}"
    done
    cd -
}

# backup the new downloaded *.deb from ${srcdir}/apt-cache-armhf to ${SRCDEST}/apt-cache-armhf
aptcache_backup2srcdst() {
    # the dir stores the real files
    PARAM_DN_BASE=$1
    shift
    # the dir contains the symbol links
    PARAM_DN_LINK=$1
    shift

    # make sure the files are not symbol links
    cd "${PARAM_DN_LINK}"
    find "${PARAM_DN_LINK}" -name "*.deb" -type f | while read i; do
        FN="$(basename ${i})"
        sudo mv "${i}" "${PARAM_DN_BASE}"
        sudo rm -f "${FN}"
        sudo ln -s "${PARAM_DN_BASE}/${FN}" "${FN}"
    done
    cd -
}

prepare_linux_4device_hardkernel () {
    # linux kernel for odroid
    cd "${srcdir}/${DNSRC_LINUX}"

    if [ "${USE_GIT_REPO}" = "1" ]; then
        git submodule init
        git submodule update
        git pull --all
        git checkout odroidc-3.10.y
    fi

    patch -p1 --no-backup-if-mismatch < ${srcdir}/kali-wifi-injection-chan.c.patch
    if [ ! "$?" = "0" ]; then
        echo "error in patch kali-wifi-injection-chan.c.patch"
        exit 1
    fi
}

prepare_linux_4device_raspberry () {
    # linux kernel for raspberry
    cd "${srcdir}/${DNSRC_LINUX}"

    if [ "${USE_GIT_REPO}" = "1" ]; then
        git submodule init
        git submodule update
        git pull --all
        # for rpi 1
        # git checkout rpi-3.12.y
    fi
}

prepare_linux_4device_pogoplug () {
    # linux kernel for odroid
    #cd "${srcdir}/${DNSRC_LINUX}"
    echo ""
}

prepare_linux_4device() {
    #prepare_linux_4device_hardkernel
    #prepare_linux_4device_raspberry
    prepare_linux_4device_pogoplug
}

prepare_linux_source() {
    cd "${srcdir}/${DNSRC_LINUX}"

    if [ ! "${USE_GIT_REPO}" = "1" ]; then
        if [ -f "${srcdir}/patch-${_PKGVER_LINUX}" ]; then
            # add upstream patch
            patch -p1 -i "${srcdir}/patch-${_PKGVER_LINUX}"
            if [ ! "$?" = "0" ]; then
                echo "error in patch patch-${_PKGVER_LINUX}"
                exit 1
            fi
        fi
    fi
    prepare_linux_4device
    cd "${srcdir}/${DNSRC_LINUX}"

    patch -p1 --no-backup-if-mismatch < ${srcdir}/${PATCH_MAC80211}
    if [ ! "$?" = "0" ]; then
        echo "error in patch ${PATCH_MAC80211}"
        exit 1
    fi

    if [ -f "${srcdir}/${CONFIG_KERNEL}" ]; then
        # set the .config file
        echo "[DBG] cp ${srcdir}/${CONFIG_KERNEL} .config"
        cp ${srcdir}/${CONFIG_KERNEL} .config # or use ours
    else
        echo "make ${MAKE_CONFIG}"
        make ${MAKE_CONFIG} # generate .config
    fi

    if [ -f "${srcdir}/${PATCH_CONFIG_KERNEL}" ]; then
        patch -p0 --no-backup-if-mismatch < ${srcdir}/${PATCH_CONFIG_KERNEL}
        if [ ! "$?" = "0" ]; then
            echo "error in patch ${PATCH_CONFIG_KERNEL}"
            exit 1
        fi
    fi

    if [ "${_kernelname}" != "" ]; then
        sed -i "s|CONFIG_LOCALVERSION=.*|CONFIG_LOCALVERSION=\"${_kernelname}\"|g" ./.config
        sed -i "s|CONFIG_LOCALVERSION_AUTO=.*|CONFIG_LOCALVERSION_AUTO=n|" ./.config
    fi

    # config ZRAM
    sed -i 's|^[#\w ]*CONFIG_ZRAM=.*$|CONFIG_ZRAM=m|' .config


    # set extraversion to _PKGREL_LINUX
    sed -ri "s|^(EXTRAVERSION =).*|\1 -${_PKGREL_LINUX}|" Makefile

    # don't run depmod on 'make install'. We'll do this ourselves in packaging
    #sed -i '2iexit 0' scripts/depmod.sh
}


kali_rootfs_debootstrap() {
    PARAM_DN_DEBIAN=$1
    shift

    # the apt cache folder
    DN_APT_CACHE="${SRCDEST}/apt-cache-kali-${MACHINEARCH}"
    mkdir -p "${DN_APT_CACHE}"

    # build kali rootfs
    cd "$srcdir"

    if [ ! -f /usr/share/debootstrap/scripts/kali ]; then
        sudo ln -s /usr/share/debootstrap/scripts/sid /usr/share/debootstrap/scripts/kali
    fi
    if [ ! -f /usr/share/debootstrap/scripts/kali ]; then
        echo "Error: no deebootstrap for kali"
        exit 1
    fi

    if [ "${ISCROSS}" = "1" ]; then
        register_qemuarm
    fi

    sudo mkdir -p "${DN_ROOTFS_DEBIAN}/var/cache/apt/archives"
    sudo mkdir -p "${DN_ROOTFS_DEBIAN}/var/cache/apt/archives-real"
    sudo mount -o bind "${DN_APT_CACHE}" "${DN_ROOTFS_DEBIAN}/var/cache/apt/archives-real/"
    aptcache_link2srcdst "../archives-real/" "${DN_ROOTFS_DEBIAN}/var/cache/apt/archives"

    if [ "${ISCROSS}" = "1" ]; then
        echo "cp `which qemu-arm-static` ${DN_ROOTFS_DEBIAN}/usr/bin/"
        sudo mkdir -p "${DN_ROOTFS_DEBIAN}/usr/bin/"
        sudo cp `which qemu-arm-static` "${DN_ROOTFS_DEBIAN}/usr/bin/"
    fi

    echo "[DBG] debootstrap stage 1"
    if [ -f "${PREFIX_TMP}-FLG_KALI_ROOTFS_STAGE1" ]; then
        echo "[DBG] SKIP debootstrap stage 1"

    else
        # create the rootfs - not much to modify here, except maybe the hostname.
        echo "[DBG] debootstrap --foreign --arch ${MACHINEARCH} kali '${DN_ROOTFS_DEBIAN}'  http://${INSTALL_MIRROR}/kali"
        sudo debootstrap --foreign --no-check-gpg --include=ca-certificates,ssh,vim,locales,ntpdate,initramfs-tools --arch ${MACHINEARCH} kali "${DN_ROOTFS_DEBIAN}" "http://${INSTALL_MIRROR}/kali"
        if [ "$?" = "0" ]; then
            touch "${PREFIX_TMP}-FLG_KALI_ROOTFS_STAGE1"
        else
            echo "Error in debootstarap stage 1"
            exit 1
        fi
    fi

    echo "[DBG] debootstrap stage 2"
    if [ -f "${PREFIX_TMP}-FLG_KALI_ROOTFS_STAGE2" ]; then
        echo "[DBG] SKIP debootstrap stage 2"

    else
        sudo chroot "${DN_ROOTFS_DEBIAN}" /usr/bin/env -i LANG=C /debootstrap/debootstrap --second-stage
        if [ "$?" = "0" ]; then
            touch "${PREFIX_TMP}-FLG_KALI_ROOTFS_STAGE2"
        else
            echo "Error in debootstrap stage 2"
            exit 1
        fi
    fi

    echo "[DBG] debootstrap stage 2.5"
    sudo rm -f "${DN_ROOTFS_DEBIAN}/etc/hostname"
    sudo rm -f ${DN_ROOTFS_DEBIAN}/etc/ssh/ssh_host_*

    # Create sources.list
    cat << EOF > "${PREFIX_TMP}-aptlst1"
deb http://${INSTALL_MIRROR}/kali kali main contrib non-free
deb http://${INSTALL_SECURITY}/kali-security kali/updates main contrib non-free
EOF
    chmod 644 "${PREFIX_TMP}-aptlst1"
    sudo chown root:root "${PREFIX_TMP}-aptlst1"
    sudo mv "${PREFIX_TMP}-aptlst1" "${DN_ROOTFS_DEBIAN}/etc/apt/sources.list"
    if [ ! "$?" = "0" ]; then
        echo "Error in move apt/sources.list 2.5"
        exit 1
    fi

    # Set hostname
    #echo "echo kali > '${DN_ROOTFS_DEBIAN}/etc/hostname'" | sudo sh

    # So X doesn't complain, we add kali to hosts
    cat << EOF > "${PREFIX_TMP}-host"
127.0.0.1       kali    localhost
::1             localhost ip6-localhost ip6-loopback
fe00::0         ip6-localnet
ff00::0         ip6-mcastprefix
ff02::1         ip6-allnodes
ff02::2         ip6-allrouters
EOF
    chmod 644 "${PREFIX_TMP}-host"
    sudo chown root:root "${PREFIX_TMP}-host"
    sudo mv "${PREFIX_TMP}-host" "${DN_ROOTFS_DEBIAN}/etc/hosts"
    if [ ! "$?" = "0" ]; then
        echo "Error in move hosts"
        exit 1
    fi

    cat << EOF > "${PREFIX_TMP}-net"
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet dhcp
EOF
    sudo mv "${PREFIX_TMP}-net" "${DN_ROOTFS_DEBIAN}/etc/network/interfaces"

    cat << EOF > "${PREFIX_TMP}-reso"
nameserver 8.8.8.8
EOF
    chmod 644 "${PREFIX_TMP}-reso"
    sudo chown root:root "${PREFIX_TMP}-reso"
    sudo mv "${PREFIX_TMP}-reso" "${DN_ROOTFS_DEBIAN}/etc/resolv.conf"
    if [ ! "$?" = "0" ]; then
        echo "Error in move resolv.conf"
        exit 1
    fi

    export MALLOC_CHECK_=0 # workaround for LP: #520465
    export LC_ALL=C
    export DEBIAN_FRONTEND=noninteractive

    cat << EOF > "${PREFIX_TMP}-deb"
console-common console-data/keymap/policy select Select keymap from full list
console-common console-data/keymap/full select en-latin1-nodeadkeys
EOF
    chmod 644 "${PREFIX_TMP}-deb"
    sudo chown root:root "${PREFIX_TMP}-deb"
    sudo mv "${PREFIX_TMP}-deb" "${DN_ROOTFS_DEBIAN}/debconf.set"
    if [ ! "$?" = "0" ]; then
        echo "Error in move script debconf.set"
        exit 1
    fi

cat << EOF > "${PREFIX_TMP}-fstab"
LABEL=${DISKLABEL_ROOTFS}   /           auto    defaults,noatime,data=writeback,errors=remount-ro  0       1
LABEL=${DISKLABEL_BOOTFS}   ${MNTPOINT_BOOT_FIRMWARE}  auto    defaults,ro,owner,flush,umask=000        0       2

tmpfs       /tmp        tmpfs   nodev,nosuid,mode=1777,size=10%         0   0
#tmpfs       /tmp        tmpfs   nodev,nosuid,mode=1777,size=100m,noatime 0   0
tmpfs       /var/tmp    tmpfs   defaults,noatime,nosuid,size=30m        0   0

#tmpfs       /var/log    tmpfs   nodev,nosuid,size=20%,mode=1755     0       0
tmpfs       /var/log    tmpfs   defaults,noatime,nosuid,mode=0755,size=100m 0   0

# /var/run is a link to /run
#tmpfs       /var/run    tmpfs   defaults,noatime,nosuid,mode=0755,size=2m   0   0

proc            /proc       proc    defaults                            0       0
EOF
    chmod 644 "${PREFIX_TMP}-fstab"
    sudo chown root:root "${PREFIX_TMP}-fstab"
    sudo mv "${PREFIX_TMP}-fstab" "${DN_ROOTFS_DEBIAN}/etc/fstab"
    if [ ! "$?" = "0" ]; then
        echo "Error in move etc/fstab"
        exit 1
    fi
    # Stop the boot-sequence whinging about /tmp being read-only before /tmp is mounted:
    touch "${DN_ROOTFS_DEBIAN}/tmp/.tmpfs"

    echo "[DBG] debootstrap stage 3"
    if [ -f "${PREFIX_TMP}-FLG_KALI_ROOTFS_STAGE3" ]; then
        echo "[DBG] SKIP debootstrap stage 3"

    else
        #sudo mkdir -p "${DN_ROOTFS_DEBIAN}/sys"
        #sudo mkdir -p "${DN_ROOTFS_DEBIAN}/proc"
        #sudo mkdir -p "${DN_ROOTFS_DEBIAN}/dev/"
        #sudo mkdir -p "${DN_ROOTFS_DEBIAN}/dev/pts"
        sudo mount -o bind /sys/ "${DN_ROOTFS_DEBIAN}/sys/"
        mount | grep "${PARAM_DN_DEBIAN}/sys"
        if [ ! "$?" = "0" ]; then
            echo "Error in mount proc"
            exit 1
        fi
        sudo mount -t proc proc "${DN_ROOTFS_DEBIAN}/proc"
        mount | grep "${PARAM_DN_DEBIAN}/proc"
        if [ ! "$?" = "0" ]; then
            echo "Error in mount proc"
            exit 1
        fi
        sudo mount -o bind /dev/ "${DN_ROOTFS_DEBIAN}/dev/"
        mount | grep "${PARAM_DN_DEBIAN}/dev"
        if [ ! "$?" = "0" ]; then
            echo "Error in mount dev"
            exit 1
        fi
        sudo mount -o bind /dev/pts "${DN_ROOTFS_DEBIAN}/dev/pts"
        mount | grep "${PARAM_DN_DEBIAN}/dev/pts"
        if [ ! "$?" = "0" ]; then
            echo "Error in mount dev/pts"
            exit 1
        fi

        # systemstart
        sudo cp "${srcdir}/debian-systemstart.sh" "${DN_ROOTFS_DEBIAN}/etc/init.d/systemstart"
        sudo cp "${srcdir}/debian-zram.sh" "${DN_ROOTFS_DEBIAN}/etc/init.d/zram"
        if [ ! "$?" = "0" ]; then
            echo "Error in move script systemstart"
            exit 1
        fi

        cat << EOF > "${PREFIX_TMP}-ths"
#!/bin/bash
export PATH=/bin:/sbin:/usr/bin:/usr/sbin:$PATH
export DEBIAN_FRONTEND=noninteractive

dpkg-divert --add --local --divert /usr/sbin/invoke-rc.d.chroot --rename /usr/sbin/invoke-rc.d
cp /bin/true /usr/sbin/invoke-rc.d
echo -e "#!/bin/sh\nexit 101" > /usr/sbin/policy-rc.d
chmod +x /usr/sbin/policy-rc.d

apt-get update
apt-get --yes --force-yes install udev makedev
apt-get --yes --force-yes install locales-all

debconf-set-selections /debconf.set
rm -f /debconf.set

apt-get update
apt-get --yes --force-yes install git-core binutils ca-certificates initramfs-tools uboot-mkimage
apt-get --yes --force-yes install locales console-common less nano git

sed -i -e "s|^[#\w ]\{1,2\}en_US|en_US|g" /etc/locale.gen
locale-gen en_US en_US.UTF-8 "en_US ISO-8859-1"
update-locale LANG="en_US.UTF-8" LANGUAGE="en_US" LC_ALL="en_US.UTF-8"
#dpkg-reconfigure locales
dpkg-reconfigure -f noninteractive tzdata

echo "root:toor" | chpasswd
#USER1=pi ; useradd -m -s /bin/bash -G adm,sudo,plugdev,audio,video,cdrom,floppy,dip \${USER1} && echo "\${USER1}:\${USER1}" | chpasswd

sed -i -e 's/KERNEL\!=\"eth\*|/KERNEL\!=\"/' /lib/udev/rules.d/75-persistent-net-generator.rules
rm -f /etc/udev/rules.d/70-persistent-net.rules
apt-get --yes --force-yes install $PACKAGES

update-rc.d ssh enable

rm -f /usr/sbin/policy-rc.d
rm -f /usr/sbin/invoke-rc.d
dpkg-divert --remove --rename /usr/sbin/invoke-rc.d

sed -i -e 's|^[#\w ]*NEED_STATD[ ]*=.*$|NEED_STATD=yes|' /etc/default/nfs-common
update-rc.d rpcbind enable

# update usbmount
# MOUNTOPTIONS="sync,noexec,nodev,noatime,nodiratime"
sed -i -e 's|MOUNTOPTIONS="|MOUNTOPTIONS="utf8=1,|' /etc/usbmount/usbmount.conf

# tmpfs
sed -i -e 's|^[#\w ]*RAMTMP[ ]*=.*$|RAMTMP=yes|' /etc/default/tmpfs

insserv systemstart
insserv zram

rm -f /third-stage
EOF
        chmod +x "${PREFIX_TMP}-ths"
        sudo mv "${PREFIX_TMP}-ths" "${DN_ROOTFS_DEBIAN}/third-stage"
        if [ ! "$?" = "0" ]; then
            echo "Error in move script third-stage"
            exit 1
        fi

        sudo chroot "${DN_ROOTFS_DEBIAN}" /third-stage
        if [ ! "$?" = "0" ]; then
            echo "Error in third-stage"
            exit 1
        fi

        # unmount the cache folder befor clean up, we may reuse the cache for other builds.
        aptcache_backup2srcdst "../archives-real/" "${DN_ROOTFS_DEBIAN}/var/cache/apt/archives"
        sudo umount "${DN_ROOTFS_DEBIAN}/var/cache/apt/archives-real"
        sudo rmdir "${DN_ROOTFS_DEBIAN}/var/cache/apt/archives-real"
        find "${DN_ROOTFS_DEBIAN}/var/cache/apt/archives/" | while read i ; do sudo rm -rf $i; done

        cat << EOF > "${PREFIX_TMP}-aptlst"
deb http://http.kali.org/kali kali main non-free contrib
deb http://security.kali.org/kali-security kali/updates main contrib non-free

deb-src http://http.kali.org/kali kali main non-free contrib
deb-src http://security.kali.org/kali-security kali/updates main contrib non-free
EOF
        chmod 644 "${PREFIX_TMP}-aptlst"
        sudo chown root:root "${PREFIX_TMP}-aptlst"
        sudo mv "${PREFIX_TMP}-aptlst" "${DN_ROOTFS_DEBIAN}/etc/apt/sources.list"
        if [ ! "$?" = "0" ]; then
            echo "Error in move apt/sources.list final: ${DN_ROOTFS_DEBIAN}/etc/apt/sources.list"
            exit 1
        fi

        cat << EOF > "${PREFIX_TMP}-cln"
#!/bin/bash
export PATH=/bin:/sbin:/usr/bin:/usr/sbin:$PATH
export DEBIAN_FRONTEND=noninteractive
rm -rf /root/.bash_history
apt-get update
apt-get clean
find /var/cache/apt/archives/ | while read i ; do rm -f $i; done
/etc/init.d/dbus stop
/etc/init.d/ssh  stop
rm -f /debconf.set
rm -f /0
rm -f /hs_err*
rm -f /cleanup
rm -f /usr/bin/qemu*
EOF
        chmod +x "${PREFIX_TMP}-cln"
        sudo mv "${PREFIX_TMP}-cln" "${DN_ROOTFS_DEBIAN}/cleanup"
        if [ ! "$?" = "0" ]; then
            echo "Error in move script cleanup"
            exit 1
        fi

        sudo chroot "${DN_ROOTFS_DEBIAN}" /cleanup
        if [ ! "$?" = "0" ]; then
            echo "Error in chroot cleanup"
            exit 1
        fi
        sudo rm -f "${DN_ROOTFS_DEBIAN}/usr/bin/qemu*"
        sudo rm -f "${DN_ROOTFS_DEBIAN}/debconf.set"

        sudo umount "${DN_ROOTFS_DEBIAN}/proc/sys/fs/binfmt_misc"
        sudo umount "${DN_ROOTFS_DEBIAN}/dev/pts"
        sudo umount "${DN_ROOTFS_DEBIAN}/dev/"
        sudo umount "${DN_ROOTFS_DEBIAN}/proc"
        sudo umount "${DN_ROOTFS_DEBIAN}/sys/"

        #sudo chown -R root:root "${DN_ROOTFS_DEBIAN}"
        touch "${PREFIX_TMP}-FLG_KALI_ROOTFS_STAGE3"
    fi

    # make sure it umounted
    aptcache_backup2srcdst "../archives-real/" "${DN_ROOTFS_DEBIAN}/var/cache/apt/archives"
    sudo umount "${DN_ROOTFS_DEBIAN}/var/cache/apt/archives-real"
    sudo rmdir "${DN_ROOTFS_DEBIAN}/var/cache/apt/archives-real"
    find "${DN_ROOTFS_DEBIAN}/var/cache/apt/archives/" | while read i ; do sudo rm -rf $i; done

    if [ "${ISCROSS}" = "1" ]; then
        unregister_qemuarm
    fi
}


# compile the source via chroot, example
#compile_in_rootfs_bychroot "KERNEL" "${PREFIX_TMP}-ths" "${srcdir}/${DNSRC_LINUX}" "${DN_ROOTFS_KERNEL}" "${srcdir}/rootfs-compilekernel-${MACHINEARCH}-${pkgname}"
#compile_in_rootfs_bychroot "U-BOOT" "${PREFIX_TMP}-ths" "${srcdir}/${DNSRC_UBOOT}" "${DN_ROOTFS_KERNEL}" "${srcdir}/rootfs-compilekernel-${MACHINEARCH}-${pkgname}"
compile_in_rootfs_bychroot() {
    PARAM_TAGNAME=$1
    shift
    PARAM_FN_EXEC=$1
    shift
    PARAM_DN_SOURCE=$1
    shift
    PARAM_DN_TARGET=$1
    shift
    PARAM_DN_DEBIAN=$1
    shift

    if [ "${PARAM_TAGNAME}" = "" ]; then
        echo "[DBG] Error, not set tag name"
        exit 1
    fi
    if [ "${PARAM_FN_EXEC}" = "" ]; then
        echo "[DBG] Error, not set execute script"
        exit 1
    fi
    if [ ! -f "${PARAM_FN_EXEC}" ]; then
        echo "[DBG] Error,  execute script"
        exit 1
    fi
    if [ ! -f "${PARAM_FN_EXEC}" ]; then
        echo "[DBG] Error, not exist execute script"
        exit 1
    fi
    if [ "${PARAM_DN_SOURCE}" = "" ]; then
        echo "[DBG] Error, not set source dir"
        exit 1
    fi
    if [ "${PARAM_DN_TARGET}" = "" ]; then
        echo "[DBG] Error, not set target dir"
        exit 1
    fi

    if [ "${PARAM_DN_DEBIAN}" = "" ]; then
        PARAM_DN_DEBIAN="${srcdir}/rootfs-compilekernel-${MACHINEARCH}-${pkgname}"
    fi

    # the apt cache folder
    DN_APT_CACHE="${SRCDEST}/apt-cache-kali-${MACHINEARCH}"
    mkdir -p "${DN_APT_CACHE}"

    # build kali rootfs
    cd "$srcdir"

    if [ ! -f /usr/share/debootstrap/scripts/kali ]; then
        sudo ln -s /usr/share/debootstrap/scripts/sid /usr/share/debootstrap/scripts/kali
    fi
    if [ ! -f /usr/share/debootstrap/scripts/kali ]; then
        echo "Error: no deebootstrap for kali"
        exit 1
    fi

    if [ "${ISCROSS}" = "1" ]; then
        register_qemuarm
    fi

    # bind install destination
    echo "[DBG] mount ${PARAM_DN_TARGET} -> ${PARAM_DN_DEBIAN}/home/target/"
    sudo mkdir -p "${PARAM_DN_DEBIAN}/home/target"
    sudo mount -o bind "${PARAM_DN_TARGET}" "${PARAM_DN_DEBIAN}/home/target/"
    # bind source path
    echo "[DBG] mount ${PARAM_DN_SOURCE} -> ${PARAM_DN_DEBIAN}/home/source/"
    sudo mkdir -p "${PARAM_DN_DEBIAN}/home/source/"
    sudo mount -o bind "${PARAM_DN_SOURCE}" "${PARAM_DN_DEBIAN}/home/source/"

    echo "[DBG] mount ${DN_APT_CACHE} -> ${PARAM_DN_DEBIAN}/var/cache/apt/archives-real/"
    sudo mkdir -p "${PARAM_DN_DEBIAN}/var/cache/apt/archives"
    sudo mkdir -p "${PARAM_DN_DEBIAN}/var/cache/apt/archives-real"
    sudo mount -o bind "${DN_APT_CACHE}" "${PARAM_DN_DEBIAN}/var/cache/apt/archives-real/"
    aptcache_link2srcdst "../archives-real/" "${PARAM_DN_DEBIAN}/var/cache/apt/archives"

    if [ "${ISCROSS}" = "1" ]; then
        echo "cp `which qemu-arm-static` ${PARAM_DN_DEBIAN}/usr/bin/"
        sudo mkdir -p "${PARAM_DN_DEBIAN}/usr/bin/"
        sudo cp `which qemu-arm-static` "${PARAM_DN_DEBIAN}/usr/bin/"
    fi

    if [[ ! -f "${PREFIX_TMP}-FLG_KALI_ROOTFS_4COMPILE" || ! -f "${PREFIX_TMP}-FLG_KALI_COMPILE_${PARAM_TAGNAME}_CHROOT" ]]; then
        #sudo mkdir -p "${PARAM_DN_DEBIAN}/sys"
        #sudo mkdir -p "${PARAM_DN_DEBIAN}/proc"
        #sudo mkdir -p "${PARAM_DN_DEBIAN}/dev/"
        #sudo mkdir -p "${PARAM_DN_DEBIAN}/dev/pts"
        echo "[DBG] mount /sys -> ${PARAM_DN_DEBIAN}/sys"
        mkdir -p "${PARAM_DN_DEBIAN}/sys/"
        sudo mount -o bind /sys/ "${PARAM_DN_DEBIAN}/sys/"
        mount | grep "${PARAM_DN_DEBIAN}/sys"
        if [ ! "$?" = "0" ]; then
            echo "Error in mount sys"
            exit 1
        fi
        echo "[DBG] mount /proc"
        mkdir -p "${PARAM_DN_DEBIAN}/proc/"
        sudo mount -t proc proc "${PARAM_DN_DEBIAN}/proc"
        mount | grep "${PARAM_DN_DEBIAN}/proc"
        if [ ! "$?" = "0" ]; then
            echo "Error in mount proc"
            exit 1
        fi
        echo "[DBG] mount /dev -> ${PARAM_DN_DEBIAN}/dev"
        mkdir -p "${PARAM_DN_DEBIAN}/dev/"
        sudo mount -o bind /dev/ "${PARAM_DN_DEBIAN}/dev/"
        mount | grep "${PARAM_DN_DEBIAN}/dev"
        if [ ! "$?" = "0" ]; then
            echo "Error in mount dev"
            exit 1
        fi
        echo "[DBG] mount /dev/pts -> ${PARAM_DN_DEBIAN}/dev/pts"
        sudo mount -o bind /dev/pts "${PARAM_DN_DEBIAN}/dev/pts"
        mount | grep "${PARAM_DN_DEBIAN}/dev/pts"
        if [ ! "$?" = "0" ]; then
            echo "Error in mount dev/pts"
            exit 1
        fi
    fi

    echo "[DBG] create rootfs for compile source"
    if [ -f "${PREFIX_TMP}-FLG_KALI_ROOTFS_4COMPILE" ]; then
        echo "[DBG] SKIP create rootfs for compile source"

    else
        # create the rootfs - not much to modify here, except maybe the hostname.
        echo "[DBG] debootstrap --variant=minbase --no-check-gpg --include=wget,apt-utils,sudo --arch ${MACHINEARCH} kali '${PARAM_DN_DEBIAN}'  http://${INSTALL_MIRROR}/kali"
        #sudo debootstrap --variant=minbase --no-check-gpg --include=wget,apt-utils,sudo --arch=${MACHINEARCH} jessie "${PARAM_DN_DEBIAN}"
        sudo debootstrap --variant=minbase --no-check-gpg --include=wget,apt-utils,sudo --arch ${MACHINEARCH} kali "${PARAM_DN_DEBIAN}" "http://${INSTALL_MIRROR}/kali"
        if [ ! "$?" = "0" ]; then
            echo "Error in debootstarap stage 1"
            exit 1
        fi

        cat << EOF > "${PREFIX_TMP}-stg2"
#!/bin/bash
export PATH=/bin:/sbin:/usr/bin:/usr/sbin:$PATH
export DEBIAN_FRONTEND=noninteractive

apt-get update

apt-get --yes --force-yes install locales console-common less nano git

sed -i -e "s|^[#\w ]\{1,2\}en_US|en_US|g" /etc/locale.gen
locale-gen en_US en_US.UTF-8 "en_US ISO-8859-1"
update-locale LANG="en_US.UTF-8" LANGUAGE="en_US" LC_ALL="en_US.UTF-8"
#dpkg-reconfigure locales
dpkg-reconfigure -f noninteractive tzdata

apt-get --yes --force-yes install wget build-essential libncurses-dev devscripts fakeroot kernel-package bc

rm -f /second-stage
EOF
        echo "cp ${PREFIX_TMP}-stg2 ${PARAM_DN_DEBIAN}/second-stage"
        sudo cp "${PREFIX_TMP}-stg2" "${PARAM_DN_DEBIAN}/second-stage"
        sudo chmod +x "${PARAM_DN_DEBIAN}/second-stage"
        if [ ! "$?" = "0" ]; then
            echo "Error in move script second-stage"
            exit 1
        fi
        sudo chroot "${PARAM_DN_DEBIAN}" /second-stage
        if [ "$?" = "0" ]; then
            sudo rm -f "${PARAM_DN_DEBIAN}/second-stage"
            touch "${PREFIX_TMP}-FLG_KALI_ROOTFS_4COMPILE"
        else
            echo "Error in second-stage"
            exit 1
        fi
    fi

    echo "[DBG] compile ${PARAM_TAGNAME} by chroot"
    if [ -f "${PREFIX_TMP}-FLG_KALI_COMPILE_${PARAM_TAGNAME}_CHROOT" ]; then
        echo "[DBG] SKIP compile ${PARAM_TAGNAME} by chroot"

    else

        if [ ! -f "${PARAM_FN_EXEC}" ]; then
            echo "[DBG] not set exec file!!"
            exit 1
        fi
        sudo cp "${PARAM_FN_EXEC}" "${PARAM_DN_DEBIAN}/third-stage"
        sudo chmod +x "${PARAM_DN_DEBIAN}/third-stage"
        if [ ! "$?" = "0" ]; then
            echo "Error in move script third-stage"
            exit 1
        fi
        sudo chroot "${PARAM_DN_DEBIAN}" /third-stage
        if [ ! "$?" = "0" ]; then
            echo "Error in third-stage"
            exit 1
        fi

        sudo rm -f "${PARAM_DN_DEBIAN}/debconf.set"

        #sudo chown -R root:root "${PARAM_DN_DEBIAN}"
        touch "${PREFIX_TMP}-FLG_KALI_COMPILE_${PARAM_TAGNAME}_CHROOT"
    fi

    # unmount the cache folder befor clean up, we may reuse the cache for other builds.
    aptcache_backup2srcdst "../archives-real/" "${PARAM_DN_DEBIAN}/var/cache/apt/archives"
    sudo umount "${PARAM_DN_DEBIAN}/var/cache/apt/archives-real"
    sudo rmdir "${PARAM_DN_DEBIAN}/var/cache/apt/archives-real"
    find "${PARAM_DN_DEBIAN}/var/cache/apt/archives/" | while read i ; do sudo rm -rf $i; done

    if [[ ! -f "${PREFIX_TMP}-FLG_KALI_ROOTFS_4COMPILE" || ! -f "${PREFIX_TMP}-FLG_KALI_COMPILE_${PARAM_TAGNAME}_CHROOT" ]]; then

        cat << EOF > "${PREFIX_TMP}-cln"
#!/bin/bash
export PATH=/bin:/sbin:/usr/bin:/usr/sbin:$PATH
export DEBIAN_FRONTEND=noninteractive
rm -rf /root/.bash_history
apt-get update
apt-get clean
find /var/cache/apt/archives/ | while read i ; do rm -f $i; done
/etc/init.d/dbus stop
/etc/init.d/ssh  stop
rm -f /debconf.set
rm -f /0
rm -f /hs_err*
rm -f /cleanup
rm -f /usr/bin/qemu*
EOF
        chmod +x "${PREFIX_TMP}-cln"
        sudo mv "${PREFIX_TMP}-cln" "${PARAM_DN_DEBIAN}/cleanup"
        if [ ! "$?" = "0" ]; then
            echo "Error in move script cleanup"
            exit 1
        fi
        sudo chroot "${PARAM_DN_DEBIAN}" /cleanup
        if [ ! "$?" = "0" ]; then
            echo "Error in chroot cleanup"
            exit 1
        fi
    fi

    # make sure it umounted
    sudo rm -f "${PARAM_DN_DEBIAN}/usr/bin/qemu*"
    sudo umount "${PARAM_DN_DEBIAN}/proc/sys/fs/binfmt_misc"
    sudo umount "${PARAM_DN_DEBIAN}/dev/pts"
    sudo umount "${PARAM_DN_DEBIAN}/dev/"
    sudo umount "${PARAM_DN_DEBIAN}/proc"
    sudo umount "${PARAM_DN_DEBIAN}/sys/"

    sudo umount "${PARAM_DN_DEBIAN}/home/target"
    sudo rmdir "${PARAM_DN_DEBIAN}/home/target"
    sudo umount "${PARAM_DN_DEBIAN}/home/source/"
    sudo rmdir "${PARAM_DN_DEBIAN}/home/source/"

    if [ "${ISCROSS}" = "1" ]; then
        unregister_qemuarm
    fi
}

build_linuxkernel_install_rootfs_4device_hardkernel() {
    make uImage
    make dtbs
    sudo mkdir -p "${DN_BOOT_4KERNEL}/dtbs/"
    sudo cp arch/arm/boot/uImage "${DN_BOOT_4KERNEL}/"
    sudo cp arch/arm/boot/dts/meson8b_odroidc.dtb "${DN_BOOT_4KERNEL}/dtbs/"
}

build_linuxkernel_install_rootfs_4device_raspberry() {
    my0_check_valid_path "${DN_ROOTFS_KERNEL}"
    sudo mkdir -p "${DN_BOOT_4KERNEL}"
    sudo chown -R ${USER} "${DN_BOOT_4KERNEL}"
    sudo cp -rf ${srcdir}/firmware-raspberrypi-git/boot/* ${DN_BOOT_4KERNEL}

    sudo cp arch/arm/boot/zImage ${DN_BOOT_4KERNEL}/${FN_RPI_KERNEL}

    T="${PREFIX_TMP}-cmdline.txt"
    cat << EOF > "${T}"
dwc_otg.lpm_enable=0 console=ttyAMA0,115200 kgdboc=ttyAMA0,115200 console=tty1 elevator=deadline root=/dev/mmcblk0p2 rootfstype=ext4 rootwait
EOF
    sudo mv "${T}" "${DN_BOOT_4KERNEL}/cmdline.txt"
    if [ ! "$?" = "0" ]; then
        echo "Error in move file $T"
        exit 1
    fi

    # rpi-wiggle
    sudo mkdir -p ${DN_ROOTFS_KERNEL}/scripts
    #sudo wget https://raw.github.com/dweeber/rpiwiggle/master/rpi-wiggle -O ${DN_ROOTFS_KERNEL}/scripts/rpi-wiggle.sh
    sudo cp ${srcdir}/rpiwiggle-git/rpi-wiggle ${DN_ROOTFS_KERNEL}/scripts/rpi-wiggle.sh
    sudo chmod 755 ${DN_ROOTFS_KERNEL}/scripts/rpi-wiggle.sh
}

build_linuxkernel_install_rootfs_4device_pogoplug() {
    sudo cp "${DN_ROOTFS_KERNEL}/${MNTPOINT_BOOT_FIRMWARE}/zImage" "${DN_ROOTFS_KERNEL}/${MNTPOINT_BOOT_FIRMWARE}/zImage-${_PKGVER_LINUX}-kirkwood-yhfu-3"
    if [ ! "$?" = "0" ]; then
        echo "[DBG] Error in copy zImage"
    fi
}

build_linuxkernel_install_rootfs_4device() {
    #build_linuxkernel_install_rootfs_4device_raspberry
    #build_linuxkernel_install_rootfs_4device_hardkernel
    build_linuxkernel_install_rootfs_4device_pogoplug
}


set_cross_compiler_4device_hardkernel() {
    export ARCH=arm
    if [ "${ISCROSS}" = "1" ]; then
        export PATH=${DN_TOOLCHAIN_KERNEL}/gcc-linaro-arm-linux-gnueabihf-4.9-2014.09_linux/bin/:$PATH
        export CROSS_COMPILE=arm-linux-gnueabihf-
    else
        export CROSS_COMPILE=
        unset CROSS_COMPILE
    fi
}

set_cross_compiler_4device_raspberry() {
    export ARCH=arm
    if [ "${ISCROSS}" = "1" ]; then
        if [ $(uname -m) = x86_64 ]; then
            export DN_TOOLCHAIN_KERNEL="${srcdir}/tools-raspberrypi-git/"
            export PATH=${DN_TOOLCHAIN_KERNEL}/arm-bcm2708/gcc-linaro-arm-linux-gnueabihf-raspbian-x64/bin/:$PATH
            export CROSS_COMPILE=arm-linux-gnueabihf-
        else
            export DN_TOOLCHAIN_KERNEL="${srcdir}/tools-raspberrypi-git/"
            export PATH=${DN_TOOLCHAIN_KERNEL}/arm-bcm2708/gcc-linaro-arm-linux-gnueabihf-raspbian/bin/:$PATH
            export CROSS_COMPILE=arm-linux-gnueabihf-
        fi
    else
        export CROSS_COMPILE=
        unset CROSS_COMPILE
    fi
}

set_cross_compiler_4device_pogoplug() {
    export CROSS_COMPILE=
    unset CROSS_COMPILE
}

set_cross_compiler_4device() {
    #set_cross_compiler_4device_hardkernel
    #set_cross_compiler_4device_raspberry
    set_cross_compiler_4device_pogoplug
}

build_linuxkernel_install_rootfs_bycross() {
    # compile and install linux kernel
    set_cross_compiler_4device

    if [ -f "${PREFIX_TMP}-FLG_KERNEL_COMPILE_CORE" ]; then
        echo "[DBG] SKIP compile kernel core"

    else
        # get kernel version
        #make oldconfig && make prepare
        make prepare

        # load configuration
        # Configure the kernel. Replace the line below with one of your choice.
        #make menuconfig # CLI menu for configuration
        #make nconfig # new CLI menu for configuration
        #make xconfig # X-based configuration
        #make oldconfig # using old config from previous kernel version
        # ... or manually edit .config

        # rewrite configuration
        yes "" | make config >/dev/null

        # compile linux kernel for Raspberry Pi 2
        #make clean
        make -j $MACHINECORES
        RET=$?
        if [ ! "${RET}" = "0" ]; then
            echo "compiling linux kernel return $RET"
            echo "Error in compiling linux kernel"
            exit 1
        fi
        make -j $MACHINECORES modules
        if [ ! "$?" = "0" ]; then
            echo "Error in compiling linux kernel modules"
            exit 1
        fi

        my0_check_valid_path "${DN_ROOTFS_KERNEL}"
        sudo chown -R ${USER} "${DN_ROOTFS_KERNEL}"
        # install kernel
        make -j $MACHINECORES modules_install INSTALL_MOD_PATH="${DN_ROOTFS_KERNEL}"
        if [ "$?" = "0" ]; then
            touch "${PREFIX_TMP}-FLG_KERNEL_COMPILE_CORE"
        else
            echo "Error in installing  linux kernel modules"
            exit 1
        fi
    fi

    my0_check_valid_path "${DN_ROOTFS_KERNEL}"
    sudo mkdir -p "${DN_ROOTFS_KERNEL}/lib/"
    sudo rm -rf ${DN_ROOTFS_KERNEL}/lib/firmware
    #git clone --depth 1 https://git.kernel.org/pub/scm/linux/kernel/git/firmware/linux-firmware.git ${DN_ROOTFS_KERNEL}/lib/firmware
    sudo cp -r ${srcdir}/firmware-linux-git ${DN_ROOTFS_KERNEL}/lib/firmware
    sudo rm -rf ${DN_ROOTFS_KERNEL}/lib/firmware/.git

    build_linuxkernel_install_rootfs_4device
}

build_linuxkernel_install_rootfs_bychroot() {

    cat << EOF > "${PREFIX_TMP}-ths"
#!/bin/bash
export PATH=/bin:/sbin:/usr/bin:/usr/sbin:$PATH
export DEBIAN_FRONTEND=noninteractive

apt-get update
#apt-get --yes --force-yes install wget build-essential libncurses-dev devscripts fakeroot kernel-package bc

MACHINECORES=$(grep -c processor /proc/cpuinfo)
if [ "$MACHINECORES" = "" ]; then
    MACHINECORES=2
fi

export CONCURRENCY_LEVEL=${MACHINECORES}

cd /home/source/

    # get kernel version
    #make oldconfig && make prepare
    make prepare

    # load configuration
    # Configure the kernel. Replace the line below with one of your choice.
    #make menuconfig # CLI menu for configuration
    #make nconfig # new CLI menu for configuration
    #make xconfig # X-based configuration
    #make oldconfig # using old config from previous kernel version
    # ... or manually edit .config

    # rewrite configuration
    yes "" | make config >/dev/null

# make debian package
#make clean

aptitude safe-upgrade
mkdir -p /etc/kernel/postinst.d/
mkdir -p /etc/kernel/postrm.d/
mkdir -p /etc/kernel/preinst.d/
echo "fakeroot make-kpkg --arch arm ${MY_CROSSCOMP_ARG} --initrd ${MY_VEREXT_ARG} kernel_image kernel_headers"
fakeroot make-kpkg --arch arm ${MY_CROSSCOMP_ARG} --initrd ${MY_VEREXT_ARG} kernel_image kernel_headers

# install to target
make -j $MACHINECORES
make -j $MACHINECORES modules
make -j $MACHINECORES modules_install INSTALL_MOD_PATH="/home/target/"
make -j $MACHINECORES install INSTALL_MOD_PATH="/home/target/"

mkdir -p "/home/target/${MNTPOINT_BOOT_FIRMWARE}/"
#make ARCH=arm ${MY_CROSSCOMP_DEF} ${MY_VEREXT_DEF} uImage
#cp arch/arm/boot/uImage /home/target/${MNTPOINT_BOOT_FIRMWARE}/uImage
echo "make zImage"
make zImage
echo "cp arch/arm/boot/zImage /home/target/${MNTPOINT_BOOT_FIRMWARE}/zImage"
cp arch/arm/boot/zImage /home/target/${MNTPOINT_BOOT_FIRMWARE}/zImage
EOF
    compile_in_rootfs_bychroot "KERNEL" "${PREFIX_TMP}-ths" "${srcdir}/${DNSRC_LINUX}" "${DN_ROOTFS_KERNEL}" "${srcdir}/rootfs-compilekernel-${MACHINEARCH}-${pkgname}"

    # install firmware
    my0_check_valid_path "${DN_ROOTFS_KERNEL}"
    sudo mkdir -p "${DN_ROOTFS_KERNEL}/lib/"
    sudo rm -rf ${DN_ROOTFS_KERNEL}/lib/firmware
    #git clone --depth 1 https://git.kernel.org/pub/scm/linux/kernel/git/firmware/linux-firmware.git ${DN_ROOTFS_KERNEL}/lib/firmware
    sudo cp -r ${srcdir}/firmware-linux-git ${DN_ROOTFS_KERNEL}/lib/firmware
    sudo rm -rf ${DN_ROOTFS_KERNEL}/lib/firmware/.git

    build_linuxkernel_install_rootfs_4device
}

rsync_and_verify() {
    PARAM_DN_SRC="$1"
    shift
    PARAM_DN_DST="$1"
    shift

    OPTS_OTHER="--devices --specials --acls --xattrs --sparse"

    sudo rsync -HPavz ${OPTS_OTHER} -q "${PARAM_DN_SRC}" "${PARAM_DN_DST}"

if [ 1 = 0 ]; then
    # verify the files
    cd "${PARAM_DN_SRC}/"
    sudo find . -type f | sudo xargs -n 1 md5sum > "${PREFIX_TMP}-md5sum-root"
    cd -
    cd "${PARAM_DN_DST}"
    sudo md5sum -c "${PREFIX_TMP}-md5sum-root"
    RET=$?
    cd -
    if [ "$RET" = "1" ]; then
        # error
        echo "Error in rootfs" >> "${FN_LOG}"
        exit 1
    fi
fi
}

install_uboot_4device_hardkernel () {
    PARAM_FN_IMAGE=$1
    shift

    echo "[DBG] Install U-Boot ..."
    DEV_LOOP=$(sudo losetup -f --show ${PARAM_FN_IMAGE})
    if [ "${DEV_LOOP}" = "" ]; then
        echo "error in losetup"
        exit 1
    fi

    BL1=${srcdir}/${DNSRC_UBOOT}/sd_fuse/bl1.bin.hardkernel
    UBOOT=${srcdir}/${DNSRC_UBOOT}/sd_fuse/u-boot.bin
if [ 0 = 1 ]; then
    if [ ! -f $BL1 ]; then
        echo "Error: $BL1 does not exist."
        exit 0
    fi

    if [ ! -f $UBOOT ]; then
        echo "Error: $UBOOT does not exist."
        exit 0
    fi

    # install BL1/MBR
    sudo dd if=$BL1   of=${DEV_LOOP} bs=1 count=442
    sudo dd if=$BL1   of=${DEV_LOOP} bs=512 skip=1 seek=1
    # install u-boot:
    sudo dd if=$UBOOT of=${DEV_LOOP} bs=512 seek=64
else
    ( cd ${srcdir}/${DNSRC_UBOOT}/sd_fuse && sh sd_fusing.sh ${DEV_LOOP} )
fi

    sudo losetup -d ${DEV_LOOP}
}

install_uboot_4device_raspberry () {
    echo "[DBG] IGNORE install_uboot_4device_raspberry"
}

install_uboot_4device_pogoplug () {
    echo "[DBG] IGNORE install_uboot_4device_pogoplug"
}

install_uboot_4device() {
    #install_uboot_4device_raspberry
    #install_uboot_4device_hardkernel
    install_uboot_4device_pogoplug
}

# create a image file with two partitions: /boot/ and /
kali_create_image() {
    PARAM_DN_ROOTFS_DEBIAN="$1"
    shift
    PARAM_DN_ROOTFS_KERNEL="$1"
    shift

    # Create the disk and partition it
    if [[ ! -f "${FN_IMAGE}" || ! -f "${PREFIX_TMP}-FLG_KALI_CREATE_IMAGE" ]]; then
        echo "Creating image file for ${pkgdesc}: ${FN_IMAGE}"
        # check Ubuntu Partition Table http://odroid.com/dokuwiki/doku.php?id=en:c1_partition_table
        sudo rm -f "${FN_IMAGE}"
        dd if=/dev/zero of=${FN_IMAGE} bs=1M count=${IMGCONTAINER_SIZE}
        if [ ! "$?" = "0" ]; then
            echo "error in dd"
            exit 1
        fi
        parted ${FN_IMAGE} --script -- mklabel msdos
        if [ ! "$?" = "0" ]; then
            echo "error in parted"
            exit 1
        fi
        parted ${FN_IMAGE} --script -- mkpart primary fat32   3072s 266239s
        parted ${FN_IMAGE} --script -- mkpart primary ext4  266240s    100%

        install_uboot_4device ${FN_IMAGE}

        touch "${PREFIX_TMP}-FLG_KALI_CREATE_IMAGE"
    else
        echo "[DBG] SKIP creating image file ${FN_IMAGE}"
    fi

if [[ ! -f "${PREFIX_TMP}-FLG_FORMAT_IMAGE" || ! -f "${PREFIX_TMP}-FLG_RSYNC_ROOTFS" || ! -f "${PREFIX_TMP}-FLG_RSYNC_KERNEL" || ! -f "${PREFIX_TMP}-FLG_BSDTAR_ROOTFS" ]]; then
    # Set the partition variables
    DEV_LOOP=$(sudo losetup -f --show ${FN_IMAGE})
    if [ "${DEV_LOOP}" = "" ]; then
        echo "error in losetup"
        exit 1
    fi
    LOOPNAME=$(sudo kpartx -va ${DEV_LOOP} | sed -E 's/.*(loop[0-9])p.*/\1/g' | head -1)
    if [ "${LOOPNAME}" = "" ]; then
        echo "Error in loop device"
        exit 1
    fi
    #partprobe "${DEV_LOOP}" # to get /dev/loop0p1 ...
    bootp="/dev/mapper/${LOOPNAME}p1"
    rootp="/dev/mapper/${LOOPNAME}p2"

    if [ -f "${PREFIX_TMP}-FLG_FORMAT_IMAGE" ]; then
        echo "[DBG] SKIP rsync rootfs"

    else
        echo "Create file systems"
        sudo mkfs.vfat -n ${DISKLABEL_BOOTFS} $bootp
        if [ ! "$?" = "0" ]; then
            echo "error in format boot"
            exit 1
        fi

        # Delete has_journal option
        sudo mkfs.ext4 -F -O ^has_journal -E stride=2,stripe-width=1024 -b 4096 -L ${DISKLABEL_ROOTFS} $rootp
        if [ ! "$?" = "0" ]; then
            echo "error in format root"
            exit 1
        fi

        # enable writeback. this step should do before you use data=writeback in the fstab!
        tune2fs -o journal_data_writeback

        #dumpe2fs $rootp
        touch "${PREFIX_TMP}-FLG_FORMAT_IMAGE"
    fi

    # Create the dirs for the partitions and mount them
    DN_ROOT="${srcdir}/mntrootfs-${MACHINEARCH}-${pkgname}"
    mkdir -p ${DN_ROOT}
    sudo mount $rootp ${DN_ROOT}
    if [ ! "$?" = "0" ]; then
        echo "error in mount root"
        exit 1
    fi

    DN_BOOT_4IMAGE="${DN_ROOT}${MNTPOINT_BOOT_FIRMWARE}"
    sudo mkdir -p ${DN_BOOT_4IMAGE}
    if [ ! "$?" = "0" ]; then
        echo "error in mkdir ${DN_BOOT_4IMAGE}"
        exit 1
    fi
    sudo mount $bootp ${DN_BOOT_4IMAGE}
    if [ ! "$?" = "0" ]; then
        echo "error in mount boot"
        exit 1
    fi

    if [ -f "${PREFIX_TMP}-FLG_RSYNC_ROOTFS" ]; then
        echo "[DBG] SKIP rsync rootfs"

    else
        echo "Rsyncing rootfs into image file"
        rsync_and_verify "${PARAM_DN_ROOTFS_DEBIAN}/" ${DN_ROOT}/
        touch "${PREFIX_TMP}-FLG_RSYNC_ROOTFS"
    fi

    if [ -f "${PREFIX_TMP}-FLG_RSYNC_KERNEL" ]; then
        echo "[DBG] SKIP rsync rootfs"

    else
        echo "Rsyncing kernel into image file"
        rsync_and_verify "${PARAM_DN_ROOTFS_KERNEL}/" ${DN_ROOT}/
        touch "${PREFIX_TMP}-FLG_RSYNC_KERNEL"
    fi

    if [ -f "${PREFIX_TMP}-FLG_BSDTAR_ROOTFS" ]; then
        echo "[DBG] SKIP bsdtar rootfs"

    else
        echo "tar rootfs from into image file"
        if which bsdtar; then
            # create a tar package for whole system, include /boot and /
            sudo bsdtar -C "${DN_ROOT}" -cf "${FN_IMAGE_BASE}.tar.gz" .
            touch "${PREFIX_TMP}-FLG_BSDTAR_ROOTFS"
        fi
    fi

    # Unmount partitions
    sudo umount ${DN_BOOT_4IMAGE}
    sudo umount ${DN_ROOT}
    sleep 5  # wait umount
    sudo kpartx -dv ${DEV_LOOP}
    sudo losetup -d ${DEV_LOOP}
    if [ ! "$?" = "0" ]; then
        echo "error in losetup"
        exit 1
    fi
fi

    check_kali_image "${FN_IMAGE}"

    # If you're building an image for yourself, comment all of this out, as you
    # don't need the sha1sum or to compress the image, since you will be testing it
    # soon.
    echo "Generating sha1sum for ${FN_IMAGE}"
    if [ ! -f "${FN_IMAGE}.sha1sum" ]; then
        (cd $(dirname ${FN_IMAGE}) && sha1sum $(basename ${FN_IMAGE}) > ${FN_IMAGE}.sha1sum)
    fi
    if [ ! -f "${FN_IMAGE}.bmap" ]; then
        if which bmaptool; then
            bmaptool create -o ${FN_IMAGE}.bmap ${FN_IMAGE}
        fi
    fi
    FLG_COMPRESSED=0
    if [ ! -f "${FN_IMAGE}.xz" ]; then
        if which pixz; then
            # Don't pixz on 32bit, there isn't enough memory to compress the images.
            HW=$(uname -m)
            if [ ${HW} == 'x86_64' ]; then
                echo "Compressing ${FN_IMAGE}"
                pixz ${FN_IMAGE} ${FN_IMAGE}.xz
                if [ "$?" = "0" ]; then
                    rm -f ${FN_IMAGE}
                    echo "Generating sha1sum for ${FN_IMAGE}.xz"
                    (cd $(dirname ${FN_IMAGE}.xz) && sha1sum $(basename ${FN_IMAGE}.xz) > ${FN_IMAGE}.xz.sha1sum)
                    FLG_COMPRESSED=1
                else
                    rm -f ${FN_IMAGE}.xz
                fi
            fi
        fi
    fi
    if [ "${FLG_COMPRESSED}" = "0" ]; then
        gzip -9 -k ${FN_IMAGE}
        if [ "$?" = "0" ]; then
            (cd $(dirname ${FN_IMAGE}.gz) && sha1sum $(basename ${FN_IMAGE}.gz) > ${FN_IMAGE}.gz.sha1sum)
            FLG_COMPRESSED=1
        else
            rm -f ${FN_IMAGE}.gz
        fi
    fi

}

my0_getpath () {
  PARAM_DN="$1"
  shift
  #readlink -f
  DN="${PARAM_DN}"
  FN=
  if [ ! -d "${DN}" ]; then
    FN=$(basename "${DN}")
    DN=$(dirname "${DN}")
  fi
  cd "${DN}" > /dev/null 2>&1
  DN=$(pwd)
  cd - > /dev/null 2>&1
  echo "${DN}/${FN}"
}

my0_check_valid_path() {
    V=$(my0_getpath "$1")
    if [[ "${V}" = "" || "${V}" = "/" ]]; then
        echo "Error: not set path variable: $1"
        exit 1
    fi
}

my_setevn() {
    # setup environments
    MACHINE=${ARCHITECTURE}
    ISCROSS=1
    HW=$(uname -m)
    case ${HW} in
    armv5el)
        # Pi 1
        ISCROSS=0
        MACHINE=armel
        ;;
    armv7l)
        # Pi 2
        ISCROSS=0
        MACHINE=armhf
        ;;
    x86_64)
        ;;
    esac
    export MACHINEARCH="${MACHINE}"

    MACHINECORES=$(grep -c processor /proc/cpuinfo)
    if [ "$MACHINECORES" = "" ]; then
        MACHINECORES=2
    fi

    export FN_IMAGE_BASE="${srcdir}/${pkgname}-${pkgver}-${MACHINEARCH}"
    export FN_IMAGE="${FN_IMAGE_BASE}.img"

    #export DN_TOOLCHAIN_UBOOT="${srcdir}/toolchains-uboot-${MACHINEARCH}"
    #export DN_TOOLCHAIN_KERNEL="${srcdir}/toolchains-kernel-${MACHINEARCH}"
    export DN_TOOLCHAIN_UBOOT="${srcdir}/"
    export DN_TOOLCHAIN_KERNEL="${srcdir}/"

    DN_ROOTFS_KERNEL="${srcdir}/rootfs-kernel-${MACHINEARCH}-${pkgname}"
    DN_BOOT_4KERNEL="${DN_ROOTFS_KERNEL}${MNTPOINT_BOOT_FIRMWARE}"
    DN_ROOTFS_DEBIAN="${srcdir}/rootfs-kali-${MACHINEARCH}-${pkgname}"

    set_cross_compiler_4device

    mkdir -p "${DN_ROOTFS_KERNEL}"
    mkdir -p "${DN_BOOT_4KERNEL}"
    mkdir -p "${DN_ROOTFS_DEBIAN}"
    my0_check_valid_path "${DN_ROOTFS_KERNEL}"
    my0_check_valid_path "${DN_BOOT_4KERNEL}"
    my0_check_valid_path "${DN_ROOTFS_DEBIAN}"
}

prepare_uboot_4device_hardkernel () {
    echo "[DBG] cd ${srcdir}/${DNSRC_UBOOT} ..."
    cd "${srcdir}/${DNSRC_UBOOT}"
    if [ "${USE_GIT_REPO}" = "1" ]; then
        git checkout odroidc-v2011.03
        if [ ! "$?" = "0" ]; then
            echo "Error in git"
            exit 1
        fi
    fi
}

prepare_uboot_4device_rpi2 () {
    echo "[DBG] prepare_uboot_4device_rpi2"
}

prepare_uboot_4device_pogoplug () {
    echo "[DBG] prepare_uboot_4device_pogoplug"
    echo "[DBG] cd ${srcdir}/${DNSRC_UBOOT} ..."
    cd "${srcdir}/${DNSRC_UBOOT}"
    if [ "${USE_GIT_REPO}" = "1" ]; then
        git checkout 2014.07.c-kirkwood
        if [ ! "$?" = "0" ]; then
            echo "Error in git"
            exit 1
        fi
    fi
}

prepare_uboot_4device () {
    #prepare_uboot_4device_hardkernel
    #prepare_uboot_4device_rpi2
    prepare_uboot_4device_pogoplug
}

prepare_uboot_source () {
    prepare_uboot_4device
}

build_uboot_install_rootfs_4device_hardkernel () {
    cd "${srcdir}/${DNSRC_UBOOT}"

    export ARCH=arm
    if [ "${ISCROSS}" = "1" ]; then
        # 32bit compiler
        export PATH=${DN_TOOLCHAIN_UBOOT}/gcc-linaro-arm-none-eabi-4.8-2014.04_linux/bin/:$PATH
        export CROSS_COMPILE=arm-none-eabi-
    else
        export CROSS_COMPILE=
        unset CROSS_COMPILE
    fi

    echo "[DBG] PATH=${PATH}"
    make -j $MACHINECORES odroidc_config
    make -j $MACHINECORES

    sudo cp "${srcdir}/boot.ini.template"   "${DN_BOOT_4KERNEL}/boot.ini"
    # use the serial in the 40pin slot
    #-e 's|console=ttyS0|console=ttyS2|'

    #sed -i 's|^\(setenv vout_mode .*\)$|#\1|' "${DN_BOOT_4KERNEL}/boot.ini"
    #sed -i 's|^#[\w ]*\(setenv vout_mode "dvi".*\)$|\1|' "${DN_BOOT_4KERNEL}/boot.ini"
    sudo sed -i \
        -e 's|root=/dev/mmcblk0p1|root=/dev/mmcblk0p2|' \
        "${DN_BOOT_4KERNEL}/boot.ini"

    sudo cp "${srcdir}/${DNSRC_UBOOT}/sd_fuse/bl1.bin.hardkernel" "${DN_BOOT_4KERNEL}/"
    sudo cp "${srcdir}/${DNSRC_UBOOT}/sd_fuse/u-boot.bin"         "${DN_BOOT_4KERNEL}/"
    sudo cp "${srcdir}/sd_fusing.sh"                              "${DN_BOOT_4KERNEL}/"
}


build_uboot_install_rootfs_4device_raspberry () {
    echo "TODO: build_uboot_install_rootfs_4device_raspberry"
}

build_uboot_install_rootfs_4device_pogoplug () {
    echo "[DBG] compile and install u-boot"
    cat << EOF > "${PREFIX_TMP}-compileuboot"
#!/bin/bash
export PATH=/bin:/sbin:/usr/bin:/usr/sbin:$PATH
export DEBIAN_FRONTEND=noninteractive

apt-get update
apt-get --yes --force-yes install wget build-essential libncurses-dev devscripts fakeroot kernel-package bc

MACHINECORES=$(grep -c processor /proc/cpuinfo)
if [ "$MACHINECORES" = "" ]; then
    MACHINECORES=2
fi

export CONCURRENCY_LEVEL=${MACHINECORES}

cd /home/source/
#make clean

make -j $MACHINECORES sheevaplug_config
make -j $MACHINECORES

cp "u-boot.bin" "/home/target/${MNTPOINT_BOOT_FIRMWARE}/u-boot.bin"

EOF
    compile_in_rootfs_bychroot "U-BOOT" "${PREFIX_TMP}-compileuboot" "${srcdir}/${DNSRC_UBOOT}" "${DN_ROOTFS_KERNEL}" "${srcdir}/rootfs-compilekernel-${MACHINEARCH}-${pkgname}"
    sudo cp "${DN_ROOTFS_KERNEL}/${MNTPOINT_BOOT_FIRMWARE}/u-boot.bin" "${DN_ROOTFS_KERNEL}/${MNTPOINT_BOOT_FIRMWARE}/uboot.2014.07-yhfu-1.pogo_v4.mtd0.kwb"
    if [ ! "$?" = "0" ]; then
        echo "[DBG] Error in copy u-boot.bin"
    fi
}

build_uboot_install_rootfs_4device () {
    #build_uboot_install_rootfs_4device_hardkernel
    #build_uboot_install_rootfs_4device_raspberry
    build_uboot_install_rootfs_4device_pogoplug
}

build_uboot_install_rootfs() {
    build_uboot_install_rootfs_4device
}

setup_rootfs_4device_hardkernel () {
    # addtional setup for the rootfs

    echo "Enable the Serial console"
if [ 1 = 1 ]; then # for debug
    echo "echo 'T0:123:respawn:/sbin/getty -L ttyS0 115200 vt100' >> ${DN_ROOTFS_DEBIAN}/etc/inittab" | sudo sh
else
    # Ubuntu
    sudo mkdir -p "${DN_ROOTFS_DEBIAN}/etc/init/"
    T="${PREFIX_TMP}-ttyS0.conf"
    cat << EOF > "${T}"
# ttyS0 - getty
#
# This service maintains a getty on ttyS0 from the point the system is
# started until it is shut down again.

start on stopped rc or RUNLEVEL=[12345]
stop on runlevel [!12345]

respawn
exec /sbin/getty -L 115200 ttyS0 vt102
EOF
    sudo mv "${T}" "${DN_ROOTFS_DEBIAN}/etc/init/ttyS0.conf"
    if [ ! "$?" = "0" ]; then
        echo "Error in move file $T"
        exit 1
    fi
fi

    # if use hdr, uncomment following
    #ROOT_UUID=$(blkid $rootp | sed -n 's/.*UUID=\"\([^\"]*\)\".*/\1/p')
    #sudo sed -i -e "s/root=[^\w ]*/root=${ROOT_UUID}/" "${DN_BOOT_4KERNEL}/boot.int"

    sudo mkdir -p "${DN_ROOTFS_DEBIAN}/etc/udev/rules.d/"

    T="${PREFIX_TMP}-10-odroid_am.rules"
    cat << EOF > "${T}"
KERNEL=="amstream*",SUBSYSTEM=="amstream-dev",MODE="0666",GROUP="video"
KERNEL=="amvideo*",SUBSYSTEM=="video",MODE="0666",GROUP="video"
EOF
    sudo mv "${T}" "${DN_ROOTFS_DEBIAN}/etc/udev/rules.d/10-odroid_am.rules"
    if [ ! "$?" = "0" ]; then
        echo "Error in move file $T"
        exit 1
    fi

    T="${PREFIX_TMP}-10-odroid_mali.rules"
    cat << EOF > "${T}"
KERNEL=="mali",SUBSYSTEM=="misc",MODE="0777",GROUP="video"
KERNEL=="ump",SUBSYSTEM=="ump",MODE="0777",GROUP="video"
EOF
    sudo mv "${T}" "${DN_ROOTFS_DEBIAN}/etc/udev/rules.d/10-odroid_mali.rules"
    if [ ! "$?" = "0" ]; then
        echo "Error in move file $T"
        exit 1
    fi

    T="${PREFIX_TMP}-10-odroid-shield.rules"
    cat << EOF > "${T}"
KERNEL=="ttySAC0", SYMLINK+="ttyACM99"
EOF
    sudo mv "${T}" "${DN_ROOTFS_DEBIAN}/etc/udev/rules.d/10-odroid-shield.rules"
    if [ ! "$?" = "0" ]; then
        echo "Error in move file $T"
        exit 1
    fi

    T="${PREFIX_TMP}-50-odroid-hdmi.rules"
    cat << EOF > "${T}"
KERNEL=="fb1", SYMLINK+="fb6"
EOF
    sudo mv "${T}" "${DN_ROOTFS_DEBIAN}/etc/udev/rules.d/50-odroid-hdmi.rules"
    if [ ! "$?" = "0" ]; then
        echo "Error in move file $T"
        exit 1
    fi

    T="${PREFIX_TMP}-60-odroid-cec.rules"
    cat << EOF > "${T}"
KERNEL=="CEC", MODE="0777"
EOF
    sudo mv "${T}" "${DN_ROOTFS_DEBIAN}/etc/udev/rules.d/60-odroid-cec.rules"
    if [ ! "$?" = "0" ]; then
        echo "Error in move file $T"
        exit 1
    fi

    T="${PREFIX_TMP}-99-input.rules"
    cat << EOF > "${T}"
KERNEL=="event*",NAME="input/%k",MODE="0660",GROUP="plugdev"
EOF
    sudo mv "${T}" "${DN_ROOTFS_DEBIAN}/etc/udev/rules.d/99-input.rules"
    if [ ! "$?" = "0" ]; then
        echo "Error in move file $T"
        exit 1
    fi

    # x window
    mkdir -p ${DN_ROOTFS_DEBIAN}/etc/X11/
    sudo mv ${DN_ROOTFS_DEBIAN}/etc/X11/xorg.conf ${DN_ROOTFS_DEBIAN}/etc/X11/xorg.conf.old
    T="${PREFIX_TMP}-xorg.conf"
    cat << EOF > "${T}"
Section "Screen"
  Identifier "Default Screen"
  Monitor "Configured Monitor"
  Device "Configured Video Device"
  DefaultDepth 16
EndSection
EOF
    sudo mv "${T}" "${DN_ROOTFS_DEBIAN}/etc/X11/xorg.conf"
    if [ ! "$?" = "0" ]; then
        echo "Error in move file $T"
        exit 1
    fi

    # SOUND
    T="${PREFIX_TMP}-asound.conf"
    cat << EOF > "${T}"
pcm.!default {
  type plug
  slave {
    pcm "hw:0,1"
  }
}
ctl.!default {
  type hw
  card 0
}
EOF
    sudo mv "${T}" "${DN_ROOTFS_DEBIAN}/etc/asound.conf"
    if [ ! "$?" = "0" ]; then
        echo "Error in move file $T"
        exit 1
    fi

    sudo sed -i \
        -e "s|^#[\w ]*load-module module-alsa-sink|load-module module-alsa-sink|g" \
        -e "s|^#[\w ]*load-module module-alsa-source device=hw:1,0|load-module module-alsa-source device=hw:0,1|g" \
        ${DN_ROOTFS_DEBIAN}/etc/pulse/default.pa

    if [ ! -f ${DN_ROOTFS_DEBIAN}/etc/rc.local ]; then
        echo "echo 'exit 0' >> ${DN_ROOTFS_DEBIAN}/etc/rc.local" | sudo sh
        sudo chmod 755 ${DN_ROOTFS_DEBIAN}/etc/rc.local
    fi

    #sudo sed -i -e "/^[^#]*exit 0/i\echo 0 > /sys/devices/platform/mesonfb/graphics/fb1/blank" ${DN_ROOTFS_DEBIAN}/etc/rc.local
    grep -v 'echo 0 > /sys/devices/platform/mesonfb/graphics/fb1/blank' ${DN_ROOTFS_DEBIAN}/etc/rc.local > tmp
    sed -i -e "/^[^#]*exit 0/i\echo 0 > /sys/devices/platform/mesonfb/graphics/fb1/blank" tmp
    chmod 755 tmp
    sudo mv tmp ${DN_ROOTFS_DEBIAN}/etc/rc.local

    # http://www.armadeus.com/wiki/index.php?title=FrameBuffer
    # change the cursor color
    #PROMPT_COMMAND='echo -e "\033[?16;0;200c"'
    # blinking
    #echo 1 > /sys/class/graphics/fbcon/cursor_blink

    # Set tmux to show the cursor
    T="${PREFIX_TMP}-tmux.conf"
    if [ -f "${DN_ROOTFS_DEBIAN}/etc/tmux.conf" ]; then
        cp "${DN_ROOTFS_DEBIAN}/etc/tmux.conf" "${T}"
    fi
    cat << EOF >> "${T}"
setw -ga terminal-overrides ',*:Cc=\E[?120;%p1%s;240c:Cr=\E[?120;0;240c:civis=\E[?25l:cnorm=\E[?25h:cvvis=\E[?25h,'
set -g status-bg black
set -g status-fg white
EOF
    sudo mv "${T}" "${DN_ROOTFS_DEBIAN}/etc/tmux.conf"
    if [ ! "$?" = "0" ]; then
        echo "Error in move file $T"
        exit 1
    fi

    T="${PREFIX_TMP}-bashrc"
    if [ -f "${DN_ROOTFS_DEBIAN}/etc/bash.bashrc" ]; then
        cp "${DN_ROOTFS_DEBIAN}/etc/bash.bashrc" "${T}"
    fi
    cat "${srcdir}/bash.bashrc.template" >> "${T}"
    sudo mv "${T}" "${DN_ROOTFS_DEBIAN}/etc/bash.bashrc"
    if [ ! "$?" = "0" ]; then
        echo "Error in move file $T"
        exit 1
    fi

if [ 0 = 1 ]; then
    # TO be verified ....
    # http://forum.odroid.com/viewtopic.php?f=114&t=8281
    # http://forum.odroid.com/viewtopic.php?f=115&t=8121#p64249
    # ArchLinux: Improve network speed
    sudo sed -i \
        -e "/exit 0/i\echo 32768 > /proc/sys/net/core/rps_sock_flow_entries" \
        -e "/exit 0/i\echo 2048 > /sys/class/net/eth0/queues/rx-0/rps_flow_cnt" \
        -e "/exit 0/i\echo f > /sys/class/net/eth0/queues/rx-0/rps_cpus" \
        -e "/exit 0/i\# Set XPS" \
        -e "/exit 0/i\echo c > /sys/class/net/eth0/queues/tx-0/xps_cpus" \
        -e "/exit 0/i\#Reconnect" \
        -e "/exit 0/i\ifconfig eth0 down" \
        ${DN_ROOTFS_DEBIAN}/etc/rc.local

    # Slow Network speeds over NFS
    # http://forum.odroid.com/viewtopic.php?f=117&t=8096
    echo "echo 'blacklist rpcsec_gss_krb5' >> ${DN_ROOTFS_DEBIAN}/etc/modprobe.d/blacklist.conf" | sudo sh
fi

    FILES=`cat ${srcdir}/odroid-utility-git/files.txt`
    for fu in odroid-utility.sh $FILES; do
        sudo cp ${srcdir}/odroid-utility-git/$fu ${DN_ROOTFS_DEBIAN}/usr/local/bin/
    done
    # patch for kali:
    sed -i \
        -e  '/"Debian")/ i\Kali) export DISTRO="debian" ;;' \
        -e  's@`curl -s $baseurl/files.txt`@`curl -s $baseurl/files.txt|grep -v odroid-utility.sh`@' \
        ${DN_ROOTFS_DEBIAN}/usr/local/bin/odroid-utility.sh

    sudo chmod +x ${DN_ROOTFS_DEBIAN}/usr/local/bin/odroid-utility.sh
}

# check if the file exist in the created image file
# pass in the mounted root path of the image file
check_rootfs_4device_hardkernel() {
    PARAM_ROOT=$1
    shift

    chkfile_hardkernel=(
        "${MNTPOINT_BOOT_FIRMWARE}/boot.ini"
        "${MNTPOINT_BOOT_FIRMWARE}/bl1.bin.hardkernel"
        "${MNTPOINT_BOOT_FIRMWARE}/u-boot.bin"
        "${MNTPOINT_BOOT_FIRMWARE}/sd_fusing.sh"
        "${MNTPOINT_BOOT_FIRMWARE}/dtbs/meson8b_odroidc.dtb"
        "${MNTPOINT_BOOT_FIRMWARE}/uImage"

        /etc/udev/rules.d/10-odroid_am.rules
        /etc/udev/rules.d/10-odroid_mali.rules
        /etc/udev/rules.d/10-odroid-shield.rules
        /etc/udev/rules.d/50-odroid-hdmi.rules
        /etc/udev/rules.d/60-odroid-cec.rules
        /etc/udev/rules.d/99-input.rules
        /etc/X11/xorg.conf
        /etc/asound.conf
        /usr/local/bin/odroid-utility.sh
    )
    FLG_ERROR=0
    for i in ${chkfile_hardkernel[*]} ; do
        if [ ! -f "${PARAM_ROOT}/${i}" ]; then
            FLG_ERROR=1
            echo "Error: not found required file at ${PARAM_ROOT}/${i}"
        fi
    done
    if [ "${FLG_ERROR}" = "1" ]; then
        echo "[DBG] check file error!"
        exit 1
    fi
}

setup_rootfs_4device_rpi2() {
    # addtional setup for the rootfs

    echo "Enable the Serial console"
if [ 1 = 1 ]; then # for debug
    echo "echo 'T0:23:respawn:/sbin/agetty -L ttyAMA0 115200 vt100' >> ${DN_ROOTFS_DEBIAN}/etc/inittab" | sudo sh
else
    sudo mkdir -p "${DN_ROOTFS_DEBIAN}/etc/init/"
    T="${PREFIX_TMP}-ttyS0.conf"
    cat << EOF > "${T}"
start on stopped rc or RUNLEVEL=[12345]
stop on runlevel [!12345]
respawn
exec /sbin/getty -L 115200 ttyAMA0 vt102
EOF
    echo mv "${T}" "${DN_ROOTFS_DEBIAN}/etc/init/ttyAMA0.conf"
    sudo mv "${T}" "${DN_ROOTFS_DEBIAN}/etc/init/ttyAMA0.conf"
    if [ ! "$?" = "0" ]; then
        echo "Error in move file $T"
        exit 1
    fi
fi

    # if use hdr, uncomment following
    #ROOT_UUID=$(blkid $rootp | sed -n 's/.*UUID=\"\([^\"]*\)\".*/\1/p')
    #sudo sed -i -e "s/root=[^\w ]*/root=${ROOT_UUID}/" "${DN_BOOT_4KERNEL}/boot.int"

    # Set up firmware config
    T="${PREFIX_TMP}-config.txt"
    cat << EOF > "${T}"
# For more options and information see
# http://www.raspberrypi.org/documentation/configuration/config-txt.md
# Some settings may impact device functionality. See link above for details

# uncomment if you get no picture on HDMI for a default "safe" mode
#hdmi_safe=1

# uncomment this if your display has a black border of unused pixels visible
# and your display can output without overscan
#disable_overscan=1

# uncomment the following to adjust overscan. Use positive numbers if console
# goes off screen, and negative if there is too much border
#overscan_left=16
#overscan_right=16
#overscan_top=16
#overscan_bottom=16

# uncomment to force a console size. By default it will be display's size minus
# overscan.
#framebuffer_width=1280
#framebuffer_height=720

# uncomment if hdmi display is not detected and composite is being output
#hdmi_force_hotplug=1

# uncomment to force a specific HDMI mode (this will force VGA)
#hdmi_group=1
#hdmi_mode=1

# uncomment to force a HDMI mode rather than DVI. This can make audio work in
# DMT (computer monitor) modes
#hdmi_drive=2

# uncomment to increase signal to HDMI, if you have interference, blanking, or
# no display
#config_hdmi_boost=4

# uncomment for composite PAL
#sdtv_mode=2

#uncomment to overclock the arm. 700 MHz is the default.
#arm_freq=800

# Turn on i2c (bus #1) for Raspberry Pi 2 and Pi 1 Model A, B (rev 2) and B+.
# If you have a Raspberry Pi Model B rev 1 with the i2c bus 0 instead, change this line to dtparam=i2c0=on
# Raspberry Pi 1
#dtparam=i2c1=on
# Raspberry Pi 2
#dtparam=i2c_arm=on

#to turn on SPI
#dtparam=spi=on
EOF
    echo mv "${T}" "${DN_BOOT_4KERNEL}/config.txt"
    sudo mv "${T}" "${DN_BOOT_4KERNEL}/config.txt"
    if [ ! "$?" = "0" ]; then
        echo "Error in move file $T"
        exit 1
    fi
    sudo ln -sf firmware/config.txt "${DN_ROOTFS_KERNEL}/boot/config.txt"
    echo "echo 'dwc_otg.lpm_enable=0 console=tty1 root=/dev/mmcblk0p2 rootwait' > ${DN_BOOT_4KERNEL}/cmdline.txt" | sudo sh
    sudo ln -sf firmware/cmdline.txt "${DN_ROOTFS_KERNEL}/boot/cmdline.txt"

    # Load sound module on boot
    sudo mkdir -p "${DN_ROOTFS_DEBIAN}/lib/modules-load.d/"
    T="${PREFIX_TMP}-librpi2.conf"
    cat << EOF > "${T}"
snd_bcm2835
bcm2708_rng
EOF
    echo mv "${T}" "${DN_ROOTFS_DEBIAN}/lib/modules-load.d/rpi2.conf"
    sudo mv "${T}" "${DN_ROOTFS_DEBIAN}/lib/modules-load.d/rpi2.conf"
    if [ ! "$?" = "0" ]; then
        echo "Error in move file $T"
        exit 1
    fi

    # Blacklist platform modules not applicable to the RPi2
    sudo mkdir -p "${DN_ROOTFS_DEBIAN}/etc/modprobe.d/"
    T="${PREFIX_TMP}-etcrpi2.conf"
    cat << EOF > "${T}"
blacklist snd_soc_pcm512x_i2c
blacklist snd_soc_pcm512x
blacklist snd_soc_tas5713
blacklist snd_soc_wm8804
EOF
    echo mv "${T}" "${DN_ROOTFS_DEBIAN}/etc/modprobe.d/rpi2.conf"
    sudo mv "${T}" "${DN_ROOTFS_DEBIAN}/etc/modprobe.d/rpi2.conf"
    if [ ! "$?" = "0" ]; then
        echo "Error in move file $T"
        exit 1
    fi

    # Set tmux to show the cursor
    T="${PREFIX_TMP}-tmux.conf"
    if [ -f "${DN_ROOTFS_DEBIAN}/etc/tmux.conf" ]; then
        cp "${DN_ROOTFS_DEBIAN}/etc/tmux.conf" "${T}"
    fi
    cat << EOF >> "${T}"
setw -ga terminal-overrides ',*:Cc=\E[?120;%p1%s;240c:Cr=\E[?120;0;240c:civis=\E[?25l:cnorm=\E[?25h:cvvis=\E[?25h,'
set -g status-bg black
set -g status-fg white
EOF
    sudo mv "${T}" "${DN_ROOTFS_DEBIAN}/etc/tmux.conf"
    if [ ! "$?" = "0" ]; then
        echo "Error in move file $T"
        exit 1
    fi

    T="${PREFIX_TMP}-bashrc"
    if [ -f "${DN_ROOTFS_DEBIAN}/etc/bash.bashrc" ]; then
        cp "${DN_ROOTFS_DEBIAN}/etc/bash.bashrc" "${T}"
    fi
    cat "${srcdir}/bash.bashrc.template" >> "${T}"
    sudo mv "${T}" "${DN_ROOTFS_DEBIAN}/etc/bash.bashrc"
    if [ ! "$?" = "0" ]; then
        echo "Error in move file $T"
        exit 1
    fi

if [ 1 = 0 ]; then
    sudo mkdir -p "${DN_ROOTFS_DEBIAN}/etc/X11/"
    T="${PREFIX_TMP}-xorg.conf"
    cat << EOF > "${T}"
# X.Org X server configuration file for xfree86-video-mali

Section "Device"
        Identifier      "Mali-Fbdev"
        Driver          "mali"
        Option          "fbdev"         "/dev/fb0"
        Option          "DRI2"            "true"
        Option          "DRI2_PAGE_FLIP"  "false"
        Option          "DRI2_WAIT_VSYNC" "false"
        Option          "UMP_CACHED"      "true"
        Option          "UMP_LOCK"        "false"
        Option          "SWCursor"        "true"
        Option          "HWCursor"        "false"
EndSection

Section "ServerFlags"
        Option          "NoTrapSignals" "true"
        Option          "DontZap"       "false"
        Option          "BlankTime"     "0"
        Option          "StandbyTime"   "0"
        Option          "SuspendTime"   "0"
        Option          "OffTime"       "0"
EndSection

Section "DRI"
        Mode            0666
EndSection
EOF
    echo mv "${T}" "${DN_ROOTFS_DEBIAN}/etc/X11/xorg.conf"
    sudo mv "${T}" "${DN_ROOTFS_DEBIAN}/etc/X11/xorg.conf"
    if [ ! "$?" = "0" ]; then
        echo "Error in move file $T"
        exit 1
    fi

    T="${PREFIX_TMP}-xorg.conf.failsafe"
    cat << EOF > "${T}"
Section "Device"
	Identifier	"Configured Video Device"
	Driver		"vesa"
EndSection

Section "Monitor"
	Identifier	"Configured Monitor"
EndSection

Section "Screen"
	Identifier	"Default Screen"
	Monitor		"Configured Monitor"
	Device		"Configured Video Device"
EndSection
EOF
    echo mv "${T}" "${DN_ROOTFS_DEBIAN}/etc/X11/xorg.conf.failsafe"
    sudo mv "${T}" "${DN_ROOTFS_DEBIAN}/etc/X11/xorg.conf.failsafe"
    if [ ! "$?" = "0" ]; then
        echo "Error in move file $T"
        exit 1
    fi
fi # disable this X11 config

}

# check if the file exist in the created image file
# pass in the mounted root path of the image file
check_rootfs_4device_rpi2() {
    PARAM_ROOT=$1
    shift

    chkfile_rpi2=(
        "${MNTPOINT_BOOT_FIRMWARE}/config.txt"
        "${MNTPOINT_BOOT_FIRMWARE}/cmdline.txt"
        "${MNTPOINT_BOOT_FIRMWARE}/${FN_RPI_KERNEL}"

        #/etc/X11/xorg.conf
        #/etc/X11/xorg.conf.failsafe
        /lib/modules-load.d/rpi2.conf
        /scripts/rpi-wiggle.sh
    )
    FLG_ERROR=0
    for i in ${chkfile_rpi2[*]} ; do
        if [ ! -f "${PARAM_ROOT}/${i}" ]; then
            FLG_ERROR=1
            echo "Error: not found required file at ${PARAM_ROOT}/${i}"
        fi
    done
    if [ "${FLG_ERROR}" = "1" ]; then
        echo "[DBG] check file error!"
        exit 1
    fi
}

setup_rootfs_4device_pogoplug() {
    echo "[DBG] skip setup rootfs for pogoplug"
}

check_rootfs_4device_pogoplug() {
    echo "[DBG] SKIP check rootfs for pogoplug"
}

setup_rootfs_4device() {
    #setup_rootfs_4device_hardkernel
    #setup_rootfs_4device_rpi2
    setup_rootfs_4device_pogoplug
}

check_rootfs_4device() {
    #check_rootfs_4device_hardkernel
    #check_rootfs_4device_rpi2
    check_rootfs_4device_pogoplug
}

# create a image file with two partitions: /boot/ and /
check_kali_image() {
    PARAM_FN_IMAGE="$1"
    shift

    echo "[DBG] check_kali_image() ..."
    # Create the disk and partition it
    if [[ ! -f "${PARAM_FN_IMAGE}" ]]; then
        echo "Error: Not found image file ${PARAM_FN_IMAGE}"
        exit 1
    fi

    # Set the partition variables
    DEV_LOOP=$(sudo losetup -f --show ${PARAM_FN_IMAGE})
    if [ "${DEV_LOOP}" = "" ]; then
        echo "error in losetup"
        exit 1
    fi
    LOOPNAME=$(sudo kpartx -va ${DEV_LOOP} | sed -E 's/.*(loop[0-9])p.*/\1/g' | head -1)
    if [ "${LOOPNAME}" = "" ]; then
        echo "Error in loop device 2: ${DEV_LOOP}"
        exit 1
    fi
    #partprobe "${DEV_LOOP}" # to get /dev/loop0p1 ...
    bootp="/dev/mapper/${LOOPNAME}p1"
    rootp="/dev/mapper/${LOOPNAME}p2"

    # Create the dirs for the partitions and mount them
    DN_ROOT="${srcdir}/mntrootfs-${MACHINEARCH}-${pkgname}-checker"
    mkdir -p ${DN_ROOT}
    sudo mount $rootp ${DN_ROOT}
    if [ ! "$?" = "0" ]; then
        echo "error in mount root "
        exit 1
    fi

    DN_BOOT_4IMAGE="${DN_ROOT}${MNTPOINT_BOOT_FIRMWARE}"
    sudo mkdir -p ${DN_BOOT_4IMAGE}
    if [ ! "$?" = "0" ]; then
        echo "error in mkdir ${DN_BOOT_4IMAGE}"
        exit 1
    fi
    sudo mount $bootp ${DN_BOOT_4IMAGE}
    if [ ! "$?" = "0" ]; then
        echo "error in mount boot"
        exit 1
    fi

    check_rootfs_4device "${DN_ROOT}"

    # Unmount partitions
    sudo umount ${DN_BOOT_4IMAGE}
    sudo umount ${DN_ROOT}
    sudo kpartx -dv ${DEV_LOOP}
    sudo losetup -d ${DEV_LOOP}
    if [ ! "$?" = "0" ]; then
        echo "error in losetup"
        exit 1
    fi
}

prepare() {
    my_setevn
    #rm -f "${FN_IMAGE}" ${PREFIX_TMP}*

    rm -rf ${DN_BOOT_4KERNEL}
    rm -rf ${DN_ROOTFS_KERNEL}
    #rm -rf ${DN_ROOTFS_DEBIAN}
    mkdir -p ${DN_BOOT_4KERNEL}
    mkdir -p ${DN_ROOTFS_KERNEL}
    mkdir -p ${DN_ROOTFS_DEBIAN}

    prepare_uboot_source
    prepare_linux_source

    echo "Build rootfs ..."
    cd ${srcdir}
    # create rootfs
    kali_rootfs_debootstrap
    setup_rootfs_4device
    echo "Build rootfs DONE!"
}

build() {
    my_setevn

    echo "Build U-Boot ..."
    build_uboot_install_rootfs
    echo "Build U-Boot DONE!"

    echo "Build Linux kernel ..."
    cd "${srcdir}/${DNSRC_LINUX}"
    build_linuxkernel_install_rootfs_bychroot
    echo "Build Linux kernel DONE!"
}

package() {
    my_setevn

    kali_create_image "${DN_ROOTFS_DEBIAN}" "${DN_ROOTFS_KERNEL}"

    cd ${srcdir}
    #make DESTDIR="$pkgdir/" install
    mkdir -p "${pkgdir}/usr/share/${pkgname}"
    cp ${FN_IMAGE}* "${pkgdir}/usr/share/${pkgname}"
}
