# Maintainer: leopempera

pkgname=veeam
pkgver=6.1.0.1498
pkgrel=1
pkgdesc="Veeam Agent for Linux"
arch=('x86_64')
url=https://repository.veeam.com/backup/linux/agent
install=${pkgname}.install
license=('custom')
depends=('ncurses' 'lvm2' 'fuse' 'mlocate')
source=("$url/rpm/el/9/x86_64/$pkgname-$pkgver-1.el9.x86_64.rpm" 
	"$url/rpm/el/9/x86_64/$pkgname-libs-$pkgver-1.x86_64.rpm")
sha256sums=('b5068ec379a33b46bd3f9e3f6d076f23fa06e5d3f68134e79f64cc07eb2c2f1d'
            '8ab12273aa2609802659f7f358673f29dc0c4a1421a9cac82494c745fee47689')
noextract=("$pkgname-$pkgver-1.el9.x86_64.rpm"
	   "$pkgname-libs-$pkgver-1.x86_64.rpm")
backup=('etc/veeam/veeam.ini' 'usr/share/veeam/lpb_scheme.sql' 'usr/share/veeam/db_upgrade.sql' 'usr/share/veeam/db_scheme.sql' 'var/lib/veeam/veeam_db.sqlite' 'var/lib/veeam/veeam_db.sqlite-shm' 'var/lib/veeam/veeam_db.sqlite-wal')

package() {
  bsdtar -xf $pkgname-$pkgver-1.el9.x86_64.rpm -C "$pkgdir" -s /sbin/bin/ -s '|lib/systemd|usr/lib/systemd|'
  bsdtar -xf $pkgname-libs-$pkgver-1.x86_64.rpm -C "$pkgdir" -s /sbin/bin/ -s '|lib/systemd|usr/lib/systemd|'
  sed -i -e 's|/var/run|/run|' -e 's|/sbin|/bin|' "$pkgdir"/usr/lib/systemd/system/veeamservice.service
  rm -rf "$pkgdir"/usr/lib/.build-id/
  install -d  "$pkgdir"/usr/share/licenses/$pkgname/
  ln -s ../../doc/$pkgname/EULA "$pkgdir"/usr/share/licenses/$pkgname/
  ln -s ../../doc/$pkgname/3rdPartyNotices.txt "$pkgdir"/usr/share/licenses/$pkgname/
}
