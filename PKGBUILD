
# Maintainer: Andrea Feletto <andrea@andreafeletto.com>

pkgname=gmid
pkgver=1.8.3
pkgrel=1
pkgdesc='Fast Gemini server written with security in mind.'
arch=('x86_64')
url='https://gmid.omarpolo.com'
license=('ISC')
depends=('libretls')
conflicts=('gmid-git' 'gmid-bin')
source=(
	"https://github.com/omar-polo/$pkgname/releases/download/$pkgver/$pkgname-$pkgver.tar.gz"
	"gmid.service"
	"gmid.conf"
)
sha256sums=(
	'f7b6cc1deaea6c5242301fa7440c0f5caaf282fea780ba1edcef480f7fa67fe1'
	'61450ba6fb7283b03f099e5172cf4e64bf40093ad2bd126b7915940d40922c9a'
	'4d943727a57dbf5f246963c0f90ccc54919cc2296538457e6b16f29f7580d9d6'
)

build() {
	cd "$srcdir/$pkgname-$pkgver"
	MANDIR='usr/share/man/' ./configure --prefix='usr/'
	make
}

package() {
	cd "$srcdir"
	install -Dm644 gmid.service -t "$pkgdir/usr/lib/systemd/system"
	install -Dm644 gmid.conf -t "$pkgdir/usr/lib/sysusers.d"

	cd "$srcdir/$pkgname-$pkgver"
	make DESTDIR="$pkgdir/" install
	install -Dm755 contrib/gencert -t "$pkgdir/usr/share/$pkgname"
	install -Dm755 contrib/renew-certs -t "$pkgdir/usr/share/$pkgname"
	install -Dm644 LICENSE -t "$pkgdir/usr/share/licenses/$pkgname"
	install -Dm644 README.md -t "$pkgdir/usr/share/doc/$pkgname"

	mkdir -p "$pkgdir/usr/share/vimfiles"
	cp -R contrib/vim/* "$pkgdir/usr/share/vimfiles/"
}
