# Contributor: graysky <graysky AT archlinux DOT us>
# Contributor: Jan Alexander Steffens (heftig) <jan.steffens@gmail.com>

### BUILD OPTIONS
# Set these variables to ANYTHING that is not null to enable them

# Tweak kernel options prior to a build via nconfig
_makenconfig=

# Optionally select a sub architecture by number if building in a clean chroot
# Leaving this entry blank will require user interaction during the build
# which will cause a failure to build if using makechrootpkg. Note that the
# generic (default) option is 30.
#
# Note - the march=native option is unavailable by this method, use the nconfig
# and manually select it.
#
#  1. AMD Opteron/Athlon64/Hammer/K8 (MK8)
#  2. AMD Opteron/Athlon64/Hammer/K8 with SSE3 (MK8SSE3)
#  3. AMD 61xx/7x50/PhenomX3/X4/II/K10 (MK10)
#  4. AMD Barcelona (MBARCELONA)
#  5. AMD Bobcat (MBOBCAT)
#  6. AMD Jaguar (MJAGUAR)
#  7. AMD Bulldozer (MBULLDOZER)
#  8. AMD Piledriver (MPILEDRIVER)
#  9. AMD Steamroller (MSTEAMROLLER)
#  10. AMD Excavator (MEXCAVATOR)
#  11. AMD Zen (MZEN)
#  12. AMD Zen 2 (MZEN2)
#  13. Intel P4 / older Netburst based Xeon (MPSC)
#  14. Intel Atom (MATOM)
#  15. Intel Core 2 (MCORE2)
#  16. Intel Nehalem (MNEHALEM)
#  17. Intel Westmere (MWESTMERE)
#  18. Intel Silvermont (MSILVERMONT)
#  19. Intel Goldmont (MGOLDMONT)
#  20. Intel Goldmont Plus (MGOLDMONTPLUS)
#  21. Intel Sandy Bridge (MSANDYBRIDGE)
#  22. Intel Ivy Bridge (MIVYBRIDGE)
#  23. Intel Haswell (MHASWELL)
#  24. Intel Broadwell (MBROADWELL)
#  25. Intel Skylake (MSKYLAKE)
#  26. Intel Skylake X (MSKYLAKEX)
#  27. Intel Cannon Lake (MCANNONLAKE)
#  28. Intel Ice Lake (MICELAKE)
#  29. Intel Cascade Lake (MCASCADELAKE)
#  30. Generic-x86-64 (GENERIC_CPU)
#  31. Native optimizations autodetected by GCC (MNATIVE)
_subarch=

# Compile ONLY used modules to VASTLYreduce the number of modules built
# and the build time.
#
# To keep track of which modules are needed for your specific system/hardware,
# give module_db script a try: https://aur.archlinux.org/packages/modprobed-db
# This PKGBUILD read the database kept if it exists
#
# More at this wiki page ---> https://wiki.archlinux.org/index.php/Modprobed-db
_localmodcfg=y

### IMPORTANT: Do no edit below this line unless you know what you're doing

pkgbase=linux-muqss
pkgver=5.4.14
pkgrel=1
_ckpatchversion=1
arch=(x86_64)
url="https://wiki.archlinux.org/index.php/Linux-ck"
license=(GPL2)
makedepends=(bc kmod libelf)
options=('!strip')
_ckpatch="patch-5.4-ck${_ckpatchversion}"
_muqss_patch=0001-MultiQueue-Skiplist-Scheduler-v0.196.patch
_gcc_more_v='20190822'
_uksm_patch=uksm-5.4.patch
_bfq_patch=5.4-bfq-dev-lucjan-v11-r2K191206.patch
source=(
  "https://www.kernel.org/pub/linux/kernel/v5.x/linux-$pkgver.tar".{xz,sign}
  config         # the main kernel config file
  "enable_additional_cpu_optimizations-$_gcc_more_v.tar.gz::https://github.com/graysky2/kernel_gcc_patch/archive/$_gcc_more_v.tar.gz"
  "http://ck.kolivas.org/patches/5.0/5.4/5.4-ck${_ckpatchversion}/$_ckpatch.xz"
  #http://ck.kolivas.org/patches/muqss/5.0/5.4/${_muqss_patch}
  https://github.com/dolohow/uksm/raw/master/v5.x/${_uksm_patch}
  #https://raw.githubusercontent.com/zaza42/uksm/master/${_uksm_patch}
  #https://raw.githubusercontent.com/Szpadel/uksm/master/v5.x/${_uksm_patch}
  https://github.com/sirlucjan/kernel-patches/raw/master/5.4/bfq-dev-lucjan/${_bfq_patch}
  0001-ZEN-Add-sysctl-and-CONFIG-to-disallow-unprivileged-CLONE_NEWUSER.patch
  0001-cpu-5.4-make-O3-always-available.patch
  0002-lib-devres-add-a-helper-function-for-ioremap_uc.patch
  0003-mfd-intel-lpss-Use-devm_ioremap_uc-for-MMIO.patch
  0004-PCI-pciehp-Prevent-deadlock-on-disconnect.patch
  0005-ACPI-PM-s2idle-Rework-ACPI-events-synchronization.patch
  0006-iwlwifi-pcie-restore-support-for-Killer-Qu-C0-NICs.patch
  0007-drm-i915-save-AUD_FREQ_CNTRL-state-at-audio-domain.patch
  0008-drm-i915-Fix-audio-power-up-sequence-for-gen10-displ.patch
  0009-drm-i915-extend-audio-CDCLK-2-BCLK-constraint-to-more.patch
  0010-drm-i915-Limit-audio-CDCLK-2-BCLK-constraint-back-to-GLK-only.patch
  0011-pinctrl-sunrisepoint-Add-missing-Interrupt-Status-register-offset.patch
  0012-Revert-iwlwifi-mvm-fix-scan-config-command-size.patch
  0013-e1000e-Revert-e1000e-Make-watchdog-use-delayed-work.patch
  0014-drm-amdgpu-Add-DC-feature-mask-to-disable-fractional-pwm.patch
  )
validpgpkeys=(
  'ABAF11C65A2970B130ABE3C479BE3E4300411886'  # Linus Torvalds
  '647F28654894E3BD457199BE38DBBDC86092693E'  # Greg Kroah-Hartman
)
sha256sums=('531e18b0eef516fa4b3843f89729fafbf3c6bc00325b082cc1f2cfcb28c8d7f0'
            'SKIP'
            '5846061889e70eae83340d9889f9edefbef194c056619a867d5ddb4a22fb223e'
            '8c11086809864b5cef7d079f930bd40da8d0869c091965fa62e95de9a0fe13b5'
            'f445eea4d0ec2015a25f1ad625c848f4f2252099795966fa4105e0aa29674c5c'
            '81d34bf02e771a126af5cb382d44a86dcc759c88b7c89fc7e5b7737731b9130e'
            'e5fb58afd02977fbd3d77d6c57c36d996acac98b39a044dc406fc2ff1a3b5bbe'
            'b7f445d79b4a790138e6306f84c33ccd38f69918b3c34ad9452b69e59e7f489a'
            '8203736c5809e5cdfb9968840b2b90c16572b63e1c4b6eb7a009cb96df54cc8b'
            '6fd45ccc07747f177b83550d397c16f8c32fa49985eab790be9792bcb0adf8fd'
            'd7257a252b7912cd9a5e96fb9eedadd6fa0744f5ea2ac52c135de7c28dac9c98'
            '657fd313fb16cb6a6ce6cff4bc6ad96069b500514e6998442aed95573ab4083a'
            '18054e5cd9fa921256bc67713126258d331c6079402c669069240edb7aad7a30'
            '2516be40fe063f7a448c69f170d628dbf549c3e084c2c7eb6910fd4782a6e73f'
            'e2084feabc3abeed37579ff515c367014356a652b85794b1612fea4daabe85d3'
            '988ffbb96d85564a9d96145e5973339a8f78ae95d919efb2ee7bb50f7a8e8fc9'
            '5257159e20a5fcb102a3b3ee6de33882a9e132e7f1d4345b8730effdd0240bb6'
            '763cd8e7d5b4a5c24f7a82f24c64ec5503ea5c81dfb42fa74150136c0ca066fd'
            '33ec2170ace6b4f7dbc1cc751110d325d8619202d0f312587adbc4bef7a045ce'
            '54104b9118d9151379589f0b95bce38aaea5d7068e80e7ab5dbdad0b73d7b1b7'
            'f9464bc1980e54f6d090f20658907318456c2d86654c8681fd518083c2596be7'
            'cba63c224af57d6b9432bb5f507121148d02b313c5f87c55504f49632a3a6062')

export KBUILD_BUILD_HOST=archlinux
export KBUILD_BUILD_USER=$pkgbase
export KBUILD_BUILD_TIMESTAMP="$(date -Ru${SOURCE_DATE_EPOCH:+d @$SOURCE_DATE_EPOCH})"

prepare() {
  cd linux-${pkgver}

  echo "Setting version..."
  scripts/setlocalversion --save-scmversion
  echo "-$pkgrel" > localversion.10-pkgrel
  echo "${pkgbase#linux}" > localversion.20-pkgname

  local src
  for src in "${source[@]}"; do
    src="${src%%::*}"
    src="${src##*/}"
    [[ $src = 0*.patch ]] || continue
    echo "Applying patch $src..."
    patch -Np1 < "../$src"
  done

  echo "Setting config..."
  cp ../config .config

  # https://bbs.archlinux.org/viewtopic.php?pid=1824594#p1824594
  sed -i -e 's/# CONFIG_PSI_DEFAULT_DISABLED is not set/CONFIG_PSI_DEFAULT_DISABLED=y/' ./.config

  # https://bbs.archlinux.org/viewtopic.php?pid=1863567#p1863567
  sed -i -e '/CONFIG_LATENCYTOP=/ s,y,n,' \
      -i -e '/CONFIG_SCHED_DEBUG=/ s,y,n,' ./.config

  # fix naming schema in EXTRAVERSION of ck patch set
  sed -i -re "s/^(.EXTRAVERSION).*$/\1 = /" "../${_ckpatch}"

  echo "Patching with ck patchset..."

  # ck patchset itself
  patch -Np1 -i ../"${_ckpatch}"

  # UKSM
  echo "applying uksm patch..."
  patch -Np1 -i ../"${_uksm_patch}"

  # BFQ patches
  echo "applying bfq patches..."
  patch -Np1 -i ../"${_bfq_patch}"

  # non-interactively apply ck1 default options
  # this isn't redundant if we want a clean selection of subarch below
  make olddefconfig

  # https://github.com/graysky2/kernel_gcc_patch
  echo "Applying enable_additional_cpu_optimizations_for_gcc_v9.1+_kernel_v4.13+.patch ..."
  patch -Np1 -i "$srcdir/kernel_gcc_patch-$_gcc_more_v/enable_additional_cpu_optimizations_for_gcc_v9.1+_kernel_v4.13+.patch"

  if [ -n "$_subarch" ]; then
    # user wants a subarch so apply choice defined above interactively via 'yes'
    yes "$_subarch" | make oldconfig
  else
    # no subarch defined so allow user to pick one
    make oldconfig
  fi

  ### Optionally load needed modules for the make localmodconfig
  # See https://aur.archlinux.org/packages/modprobed-db
    if [ -n "$_localmodcfg" ]; then
      if [ -f $HOME/.config/modprobed.db ]; then
        echo "Running Steven Rostedt's make localmodconfig now"
        make LSMOD=$HOME/.config/modprobed.db localmodconfig
      else
        echo "No modprobed.db data found"
        exit
      fi
    fi

  make -s kernelrelease > version
  echo "Prepared %s version %s" "$pkgbase" "$(<version)"

  [[ -z "$_makenconfig" ]] || make nconfig

  # save configuration for later reuse
  cat .config > "${startdir}/config.last"
}

build() {
  cd linux-${pkgver}
  make bzImage modules
}

_package() {
  pkgdesc="The ${pkgbase/linux/Linux} kernel and modules with the ck1 patchset featuring MuQSS CPU scheduler"
  depends=(coreutils kmod initramfs)
  optdepends=('crda: to set the correct wireless channels of your country'
              'linux-firmware: firmware images needed for some devices')
  provides=("linux-muqss=${pkgver}")

  cd linux-${pkgver}

  local kernver="$(<version)"
  local modulesdir="$pkgdir/usr/lib/modules/$kernver"

  echo "Installing boot image..."
  # systemd expects to find the kernel here to allow hibernation
  # https://github.com/systemd/systemd/commit/edda44605f06a41fb86b7ab8128dcf99161d2344
  #install -Dm644 "$(make -s image_name)" "$modulesdir/vmlinuz"
  #
  # hard-coded path in case user defined CC=xxx for build which causes errors
  # see this FS https://bugs.archlinux.org/task/64315
  install -Dm644 arch/x86/boot/bzImage "$modulesdir/vmlinuz"

  # Used by mkinitcpio to name the kernel
  echo "$pkgbase" | install -Dm644 /dev/stdin "$modulesdir/pkgbase"

  echo "Installing modules..."
  make INSTALL_MOD_PATH="$pkgdir/usr" modules_install

  # remove build and source links
  rm "$modulesdir"/{source,build}

  echo "Fixing permissions..."
  chmod -Rc u=rwX,go=rX "$pkgdir"
}

_package-headers() {
  pkgdesc="Headers and scripts for building modules for ${pkgbase/linux/Linux} kernel"
  depends=('linux-muqss') # added to keep kernel and headers packages matched
  provides=("linux-muqss-headers=${pkgver}" "linux-headers=${pkgver}")

  cd linux-${pkgver}
  local builddir="$pkgdir/usr/lib/modules/$(<version)/build"

  echo "Installing build files..."
  install -Dt "$builddir" -m644 .config Makefile Module.symvers System.map \
    localversion.* version vmlinux
  install -Dt "$builddir/kernel" -m644 kernel/Makefile
  install -Dt "$builddir/arch/x86" -m644 arch/x86/Makefile
  cp -t "$builddir" -a scripts

  # add objtool for external module building and enabled VALIDATION_STACK option
  install -Dt "$builddir/tools/objtool" tools/objtool/objtool

  # add xfs and shmem for aufs building
  mkdir -p "$builddir"/{fs/xfs,mm}

  echo "Installing headers..."
  cp -t "$builddir" -a include
  cp -t "$builddir/arch/x86" -a arch/x86/include
  install -Dt "$builddir/arch/x86/kernel" -m644 arch/x86/kernel/asm-offsets.s

  install -Dt "$builddir/drivers/md" -m644 drivers/md/*.h
  install -Dt "$builddir/net/mac80211" -m644 net/mac80211/*.h

  # http://bugs.archlinux.org/task/13146
  install -Dt "$builddir/drivers/media/i2c" -m644 drivers/media/i2c/msp3400-driver.h

  # http://bugs.archlinux.org/task/20402
  install -Dt "$builddir/drivers/media/usb/dvb-usb" -m644 drivers/media/usb/dvb-usb/*.h
  install -Dt "$builddir/drivers/media/dvb-frontends" -m644 drivers/media/dvb-frontends/*.h
  install -Dt "$builddir/drivers/media/tuners" -m644 drivers/media/tuners/*.h

  echo "Installing KConfig files..."
  find . -name 'Kconfig*' -exec install -Dm644 {} "$builddir/{}" \;

  echo "Removing unneeded architectures..."
  local arch
  for arch in "$builddir"/arch/*/; do
    [[ $arch = */x86/ ]] && continue
    echo "Removing $(basename "$arch")"
    rm -r "$arch"
  done

  echo "Removing documentation..."
  rm -r "$builddir/Documentation"

  echo "Removing broken symlinks..."
  find -L "$builddir" -type l -printf 'Removing %P\n' -delete

  echo "Removing loose objects..."
  find "$builddir" -type f -name '*.o' -printf 'Removing %P\n' -delete

  echo "Stripping build tools..."
  local file
  while read -rd '' file; do
    case "$(file -bi "$file")" in
      application/x-sharedlib\;*)      # Libraries (.so)
        strip -v $STRIP_SHARED "$file" ;;
      application/x-archive\;*)        # Libraries (.a)
        strip -v $STRIP_STATIC "$file" ;;
      application/x-executable\;*)     # Binaries
        strip -v $STRIP_BINARIES "$file" ;;
      application/x-pie-executable\;*) # Relocatable binaries
        strip -v $STRIP_SHARED "$file" ;;
    esac
  done < <(find "$builddir" -type f -perm -u+x ! -name vmlinux -print0)

  echo "Adding symlink..."
  mkdir -p "$pkgdir/usr/src"
  ln -sr "$builddir" "$pkgdir/usr/src/$pkgbase"

  echo "Fixing permissions..."
  chmod -Rc u=rwX,go=rX "$pkgdir"
}

pkgname=("$pkgbase" "$pkgbase-headers")
for _p in "${pkgname[@]}"; do
  eval "package_$_p() {
    $(declare -f "_package${_p#$pkgbase}")
    _package${_p#$pkgbase}
  }"
done

# vim:set ts=8 sts=2 sw=2 et:
