pkgname=mutt-kz
pkgver=1.6.0.1
pkgrel=1
pkgdesc='mutt with notmuch support and another improvements...'
url='https://github.com/karelzak/mutt-kz'
license=('GPL')
backup=('etc/Muttrc')
arch=('i686' 'x86_64')
optdepends=('smtp-forwarder: to send mail')
depends=('gpgme' 'ncurses' 'gnutls' 'libsasl' 'libidn' 'krb5' 'tokyocabinet'
    'notmuch-runtime')
makedepends=('w3m' 'docbook-xsl')
conflicts=('mutt')
provides=('mutt')
source=(
    "$pkgname-$pkgver.tar.gz::https://github.com/karelzak/$pkgname/archive/v$pkgver.tar.gz"
)
sha256sums=('7832ba066fb6d2681450e4c32b910dfb645ae7afd99dfa6b83c33ce1c5e58cea')

prepare() {
    cd "$pkgname-$pkgver"

    autoreconf -vfi
}

build() {
    cd "$pkgname-$pkgver"

    ./configure \
        --prefix=/usr \
        --sysconfdir=/etc \
        --mandir=/usr/share/man \
        --with-docdir=/usr/share/doc \
        --with-mailpath=/var/mail \
        --disable-dependency-tracking \
        --enable-compressed \
        --enable-fcntl \
        --enable-gpgme \
        --enable-hcache \
        --enable-imap \
        --enable-pop \
        --enable-smtp \
        --with-curses \
        --with-gss \
        --with-idn \
        --with-mixmaster \
        --without-bdb \
        --without-gdbm \
        --without-qdbm \
        --with-regex \
        --with-sasl \
        --with-gnutls \
        --enable-sidebar \
        --enable-nntp \
        --enable-notmuch

    make
}

package() {
    cd "$pkgname-$pkgver"
    make DESTDIR="${pkgdir}" install

    rm "${pkgdir}"/etc/mime.types{,.dist}
    rm "${pkgdir}"/usr/bin/{flea,muttbug}
    rm "${pkgdir}"/usr/share/man/man1/{flea,muttbug}.1
    install -D -m 644 contrib/gpg.rc "$pkgdir"/etc/Muttrc.gpg.dist
}
