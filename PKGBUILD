# Maintainer: 0x9fff00 <0x9fff00+git@protonmail.ch>

_name=PyMCTranslate
pkgname=python-${_name,,}
pkgver=1.2.12
pkgrel=1
pkgdesc='A library of block mappings that can be used to convert from any Minecraft format into any other Minecraft format'
arch=('any')
url="https://github.com/gentlegiantJGC/$_name"
license=('custom')
depends=('python' 'python-amulet-nbt' 'python-numpy')
makedepends=('python-build' 'python-installer' 'python-setuptools' 'python-versioneer' 'python-wheel')
# tests directory isn't in pypi sdist
source=("$pkgname-$pkgver.tar.gz::$url/archive/$pkgver.tar.gz")
sha256sums=('32d3ff80b9693f38e49fc719db72f87c51d5d5075bc3ee046d458d9614505b52')

prepare() {
  cd "$_name-$pkgver"

  # use current versioneer
  sed -Ei 's/(versioneer)-518/\1/' pyproject.toml
}

build() {
  cd "$_name-$pkgver"

  python -m build --wheel --no-isolation
}

check() {
  cd "$_name-$pkgver"

  python -m unittest discover -s tests
}

package() {
  cd "$_name-$pkgver"

  python -m installer --destdir="$pkgdir" dist/*.whl

  # https://wiki.archlinux.org/title/Python_package_guidelines#Using_site-packages
  local _site_packages="$(python -c 'import site; print(site.getsitepackages()[0])')"

  install -d "$pkgdir/usr/share/licenses/$pkgname"
  local _license_path="$_site_packages/$_name-$pkgver.dist-info/LICENSE"
  [ -f "$pkgdir/$_license_path" ] || { echo "License file not found"; exit 1; }
  ln -s "$_license_path" "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}
