# Maintainer: Andreas Wagner <Andreas dot Wagner at em dot uni-frankfurt dot de>
# Contributor: Marco Lima <cipparello gmail com>
pkgname=collectl
pkgver=3.7.4
pkgrel=1
pkgdesc="Collect Process and System Information"
url="http://collectl.sourceforge.net/"
license=('PerlArtistic' 'GPL')
arch=('i686' 'x86_64')
depends=('perl')
optdepends=('pciutils: list PCI devices'
        'ethtool: display net cards settings (recommended)'
	    'dmidecode: Desktop Management Interface data'
	    'inetutils: hostname command')
backup=(etc/collectl.conf etc/conf.d/collectl.conf)
source=("http://downloads.sourceforge.net/project/$pkgname/$pkgname/$pkgname-$pkgver/$pkgname-$pkgver.src.tar.gz"
	collectl
	collectl.conf.d
	collectl.systemd)
options=('docs')

package() {
  cd "$srcdir/$pkgname-$pkgver"

  sed -i 's|#Grep =    /bin/grep|Grep =    /usr/bin/grep|' collectl.conf
  sed -i 's|#Egrep =   /bin/egrep|Egrep =   /usr/bin/egrep|' collectl.conf
  sed -i 's|#Lspci =   /sbin/lspci|Lspci =   /usr/bin/lspci|' collectl.conf
  sed -i 's|#Ps =      /bin/ps|Ps =      /usr/bin/ps|' collectl.conf
  sed -i 's|#Rpm =     /bin/rpm|Rpm =     /usr/bin/rpm|' collectl.conf
  sed -i 's|#Lctl =    /usr/sbin/lctl|Lctl =    /usr/bin/lctl|' collectl.conf

  sed -i 's|for (my $i=0; defined(@$ipmiRemap) && $i<@{$ipmiRemap}; $i++)|for (my $i=0; $i<@{$ipmiRemap}; $i++)|' formatit.ph

  DESTDIR=${pkgdir} ./INSTALL
  rm -rf "$pkgdir/etc/init.d"

  # instead, install the init scipt, configuration file and systemd service file
  install -D -m755 ../collectl $pkgdir/etc/rc.d/collectl
  install -D -m644 ../collectl.conf.d $pkgdir/etc/conf.d/collectl.conf
  install -D -m644 ../collectl.systemd $pkgdir/etc/systemd/system/collectl.service
}

md5sums=('08f62a6778586028e6f788356626cd68'
         '7a564c6ce8e53c58568192efcbbc13d9'
         '46a71b5630ea9eab4a0058a62519c1fd'
         '6b1bc42a099a635caa341baf2259b45d')
