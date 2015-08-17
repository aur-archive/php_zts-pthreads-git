# Maintainer: Boris Momčilović <boris.momcilovic@gmail.com>

pkgname=php_zts-pthreads-git
pkgver=2.0.10.r22.gd9c0911
pkgrel=1
pkgdesc="Threading for PHP - Share Nothing, Do Everything :)"
arch=('i686' 'x86_64')
url="https://github.com/krakjoe/pthreads"
license=('PHP')
depends=('php_zts')
makedepends=('git')
source=("$pkgname"::'git://github.com/krakjoe/pthreads.git')
md5sums=('SKIP')
_ininame="pthreads.ini"
_inifile="etc/php-zts/conf.d/$_ininame"
backup=("$_inifile")

pkgver() {
  cd "$srcdir/$pkgname"
  git describe --long --tags | sed -r 's/^v//;s/([^-]*-g)/r\1/;s/-/./g'
}

build() {
  cd "$srcdir/$pkgname"

  /usr/bin/php-zts/phpize
  ./configure --with-php-config=/usr/bin/php-zts/php-config --prefix=/usr
  make
  #TEST_PHP_EXECUTABLE=`which php` php run-tests.php
}

package() {
  cd "$srcdir/$pkgname"
  make PREFIX=/usr INSTALL_ROOT="$pkgdir" install
  echo ";zend_extension=pthreads.so" > "$_ininame"
  install -vDm644 "$_ininame" "$pkgdir/$_inifile"
}
