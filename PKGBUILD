# Maintainer: 0x9fff00 <0x9fff00+git@protonmail.ch>

_name=PyMCTranslate
pkgname=python-${_name,,}
pkgver=1.0.12
pkgrel=1
pkgdesc='A library of block mappings that can be used to convert from any Minecraft format into any other Minecraft format'
arch=('any')
url="https://github.com/gentlegiantJGC/$_name"
license=('custom')
depends=('python' 'python-amulet-nbt' 'python-numpy')
makedepends=('python-pip' 'python-setuptools' 'python-wheel')
source=("https://files.pythonhosted.org/packages/source/${_name::1}/$_name/$_name-$pkgver.tar.gz")
sha256sums=('c059c0a95fac3b0e8cf52d5fa4b7a25e2ec02f3b203460ba9168ff187268cba9')

build() {
  cd "$_name-$pkgver"

  # only bdist_wheel minifies and installs json
  python setup.py bdist_wheel
}

package() {
  cd "$_name-$pkgver"

  PIP_CONFIG_FILE=/dev/null pip install --isolated --root="$pkgdir" --ignore-installed --no-deps "dist/$_name-$(python -c 'import versioneer; print(versioneer.get_version())')-py3-none-any.whl"
  python -O -m compileall "$pkgdir"/usr/lib/python*/site-packages/$_name
  install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}
