# Maintainer: robertfoster
# Contributor: LIN Rs <LinRs[d]users.noreply.github.com>

pkgbase=devilutionx-git
pkgname=("${pkgbase}")
pkgver=1.5.1.r447.8fa95a174
pkgrel=1
pkgdesc="Diablo devolved for linux (git version)"
arch=('armv6h' 'armv7h' 'arm' 'aarch64' 'i686' 'x86_64')
url="https://github.com/diasurgical/devilutionX"
license=('custom:unlicense')
depends=('bzip2' 'fmt' 'libpng' 'libsodium' 'sdl2' 'sdl2_image' 'simpleini' 'zlib')
makedepends=('cmake' 'devilutionx-graphics-tools-git' 'flac' 'gettext' 'git' 'lame' 'smpq')
conflicts=("${pkgbase%-git}")
provides=("${pkgbase%-git}")
source=("${pkgbase%-git}::git+${url}")
sha256sums=('SKIP')

pkgver() {
  cd "${pkgbase%-git}"
  printf "%s" "$(git describe --tags | sed 's/\([^-]*-\)g/r\1/;s/-/./g')"
}

prepare() {
  if [ ! -d build ]; then
    mkdir build
  fi
}

build() {
  patch -d "${pkgbase%-git}/" -p1 < ../no-item-drop.patch
  patch -d "${pkgbase%-git}/" -p1 < ../exp-share.patch
  cd build
  cmake ../"${pkgbase%-git}" \
    -DBUILD_TESTING=off \
    -DCMAKE_INSTALL_PREFIX="/usr"

  cmake --build . -j $(getconf _NPROCESSORS_ONLN)
}

package_devilutionx-git() {
  cd build
  DESTDIR="${pkgdir}" \
    cmake --install .
}
