# Maintainer of original: Martin Dünkelmann <nc-duenkekl3 at netcologne.de>
# Custom patch applied for Arch

pkgname=moneymanagerex-patched
pkgver=1.6.4.r4380.g2e244b6c8
pkgrel=1
pkgdesc="MoneyManagerEx is an easy-to-use personal finance suite. This package will always point to the newest tagged version."
arch=('x86_64')
url="http://www.moneymanagerex.org/"
license=('GPL')
depends=('wxwidgets-gtk3' 'webkit2gtk-4.1')
makedepends=('appstream' 'cmake' 'fakeroot' 'file' 'gawk' 'gcc' 'gettext' 'git' 'jq' 'lsb-release' 'make' 'pkg-config' 'rapidjson')
optdepends=('cups: for printing support')
replaces=('mmex')
provides=('moneymanagerex')
conflicts=('moneymanagerex')
source=('file://CMP0037_policy.patch'
        git+https://github.com/moneymanagerex/moneymanagerex.git#tag=v${pkgver})
sha512sums=('SKIP' 'SKIP')

pkgver() {
  cd "${srcdir}"/moneymanagerex

  git describe --long | sed 's/^v//;s/\([^-]*-g\)/r\1/;s/-/./g'
}

prepare() {
  cd "${srcdir}"/moneymanagerex

  git submodule update --init --recursive

  patch CMakeLists.txt < ../CMP0037_policy.patch
}

build() {
  cd "${srcdir}"/moneymanagerex

  # Disable all warnings when building, then configure CMake
  export CXXFLAGS=-w
  
  cmake -DCMAKE_BUILD_TYPE=None -DCMAKE_INSTALL_PREFIX='/usr' -Wno-dev -DwxWidgets_CONFIG_EXECUTABLE=/usr/bin/wx-config .
  
  cmake --build .
}

package() {
  cd "${srcdir}"/moneymanagerex

  make DESTDIR="${pkgdir}" install
}
