# Maintainer: 0x9fff00 <0x9fff00+git@protonmail.ch>

_name=PyMCTranslate
pkgname=python-pymctranslate
pkgver=1.2.22
pkgrel=1
pkgdesc='A library of block mappings that can be used to convert from any Minecraft format into any other Minecraft format'
arch=('any')
url="https://github.com/gentlegiantJGC/PyMCTranslate"
license=('custom')
depends=('python' 'python-amulet-nbt' 'python-numpy')
makedepends=('python-build' 'python-installer' 'python-setuptools' 'python-versioneer' 'python-wheel')

source=("${pkgname}-${pkgver}.tar.gz::https://github.com/gentlegiantJGC/PyMCTranslate/archive/refs/tags/${pkgver}.tar.gz")
sha256sums=('bac61b0b01f38cba5c69210c86ce1843e66da6de622997fab850f00694d6f380')

prepare() {
  cd "${_name}-${pkgver}"

  # use current versioneer
  sed -Ei 's/(versioneer)-518/\1/' pyproject.toml
}

build() {
  cd "${_name}-${pkgver}"

  python -m build --wheel --no-isolation
}

check() {
  cd "${_name}-${pkgver}"

  python -m unittest discover -s tests
}

package() {
  cd "${_name}-${pkgver}"

  python -m installer --destdir="$pkgdir" dist/*.whl

  # https://wiki.archlinux.org/title/Python_package_guidelines#Using_site-packages
  local _site_packages="$(python -c 'import site; print(site.getsitepackages()[0])')"

  install -d "$pkgdir/usr/share/licenses/$pkgname"
  local _license_path="$_site_packages/$_name-$pkgver.dist-info/LICENSE"
  [ -f "$pkgdir/$_license_path" ] || { echo "License file not found"; exit 1; }
  ln -s "$_license_path" "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}
