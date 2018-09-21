pkgname=asterisk-mini
pkgver=15.6.0
pkgrel=1
pkgdesc="A complete PBX solution"
arch=('i686' 'x86_64' 'aarch64' 'armv7h' 'armv6h')
backup=('etc/asterisk/asterisk.conf'
        'etc/asterisk/alsa.conf'
        'etc/asterisk/cdr.conf'
        'etc/asterisk/cdr_adaptive_odbc.conf'
        'etc/asterisk/cdr_syslog.conf'
        'etc/asterisk/cel.conf'
        'etc/asterisk/cel_odbc.conf'
        'etc/asterisk/confbridge.conf'
        'etc/asterisk/extensions.conf'
        'etc/asterisk/indications.conf'
        'etc/asterisk/logger.conf'
        'etc/asterisk/modules.conf'
        'etc/asterisk/musiconhold.conf'
        'etc/asterisk/pjsip.conf'
        'etc/asterisk/res_odbc.conf'
        'etc/asterisk/voicemail.conf'
	'etc/modprobe.d/snd-dummy.conf'
	'etc/modules-load.d/snd-dummy.conf'
	)
url='http://www.asterisk.org'
license=('GPL')
conflicts=('asterisk')
provides=('asterisk')
depends=('popt' 'libxml2' 'jansson' 'libxslt' 'gsm' 'sqlite3' 'libilbc' 'unixodbc' 'zlib')
makedepends=('speexdsp' 'speex' 'unixodbc' 'alsa-lib' 'libvorbis' 'curl' 'lua' 'libsrtp')
optdepends=('lua' 'libsrtp' 'psqlodbc' 'libpri' 'libss7' 'dahdi' 'speexdsp' 'alsa-lib' 'libvorbis' 'curl' 'soxr')
install=asterisk.install

_ast_dl='http://downloads.asterisk.org/pub/telephony'
_pjp_dl='http://www.pjsip.org/release'
_mini_ver='1.0'
source=("${_ast_dl}/asterisk/releases/asterisk-${pkgver}.tar.gz"
        "${_pjp_dl}/2.7.2/pjproject-2.7.2.tar.bz2"
	"pjproject-2.7.md5::${_pjp_dl}/2.7/MD5SUM.TXT"
	"${_ast_dl}/sounds/releases/asterisk-core-sounds-en-gsm-1.6.1.tar.gz"
	"${_ast_dl}/sounds/releases/asterisk-core-sounds-en-gsm-1.6.1.tar.gz.sha1"
	"${_ast_dl}/sounds/releases/asterisk-extra-sounds-en-gsm-1.5.2.tar.gz"
	"${_ast_dl}/sounds/releases/asterisk-extra-sounds-en-gsm-1.5.2.tar.gz.sha1"
	"${_ast_dl}/sounds/releases/asterisk-moh-opsound-gsm-2.03.tar.gz"
	"${_ast_dl}/sounds/releases/asterisk-moh-opsound-gsm-2.03.tar.gz.sha1"
	"asterisk-mini-${_mini_ver}.tar.gz::http://github.com/RoEdAl/asterisk-mini/archive/v${_mini_ver}.tar.gz")
sha256sums=('6620af9749524152a793ecc4ade4604064254cb46e642d50d280d56f6b7eed3e'
            '9c2c828abab7626edf18e04b041ef274bfaa86f99adf2c25ff56f1509e813772'
            'abbf4829cfa938595df431de10e45d291a153b0ee6ec4cafdd64e5b46f540696'
            'd79c3d2044d41da8f363c447dfccc140be86b4fcc41b1ca5a60a80da52f24f2d'
            'c5be5c60f1450419494008c195c08f8aa1e88d6d978001a310c9516f93d18bfb'
            'a872eb41868a75b8b4ea677d46f2659870c7190037e1d97853b4b060e60e9d7c'
            '92c00ca0148f11e85a3af8bfa6ceb4e6091cb1c053a7e29c88484192c1d9ff25'
            'b0fb7b52b05094a3d5298c965e98717f9907d65a9ec47604ac05d8b06a96e940'
            '5db48fc22600cbf3d0ca4da298627c2a35b89b9e9f8ea1d24c466a5b0362cde0'
            '22ad648e4b194231732777f9ade5dfc1375d70719c0ac3010bb8668ffc583ba1')
noextract=(
	'pjproject-2.7.2.tar.bz2'
	'asterisk-core-sounds-en-gsm-1.6.1.tar.gz'
	'asterisk-extra-sounds-en-gsm-1.5.2.tar.gz'
	'asterisk-moh-opsound-gsm-2.03.tar.gz')

build() {
  cd asterisk-${pkgver}
  ./configure \
    --prefix=/usr \
    --sysconfdir=/etc \
    --localstatedir=/var \
    --bindir=/usr/bin \
    --sbindir=/usr/bin \
    --with-externals-cache=${srcdir} \
    --with-sounds-cache=${srcdir} \
    --disable-xmldoc \
    --disable-internal-poll \
    --disable-asteriskssl \
    --without-curses \
    --without-oss \
    --without-portaudio \
    --without-jack \
    --without-x11 \
    --without-vpb \
    --without-gtk2 \
    --without-gmime \
    --without-sdl \
    --without-avcodec \
    --without-bluetooth \
    --without-iodbc \
    --without-imap \
    --without-inotify \
    --without-sqlite \
    --without-sndfile \
    --without-mysqlclient \
    --without-posgres \
    --without-iksemel \
    --without-openr2 \
    --without-radius \
    --without-resample \
    --without-spandsp \
    --without-tds \
    --without-neon29 \
    --without-neon \
    --without-pri \
    --without-ss7 \
    --without-dahdi \
    --without-misdn \
    --without-tonezone \
    --without-fftw3 \
    --without-libedit \
    --without-unbound \
    --without-opus \
    --without-opusfile

  make menuselect.makeopts
  menuselect/menuselect --enable ODBC_STORAGE menuselect.makeopts
  menuselect/menuselect --disable codec_speex --enable func_speex --disable format_ogg_speex menuselect.makeopts
  menuselect/menuselect --disable format_jpeg --disable format_ogg_vorbis --disable format_siren7 --disable format_siren14 menuselect.makeopts
  menuselect/menuselect --disable format_g719 --disable format_g723 --disable format_g729 --disable format_h263 --disable format_h264 menuselect.makeopts
  menuselect/menuselect --disable res_format_attr_opus --disable res_fax --disable res_format_attr_h263 --disable res_format_attr_h264 menuselect.makeopts
  menuselect/menuselect --disable app_festival --disable app_mp3 --disable app_ices --disable app_image menuselect.makeopts
  menuselect/menuselect --disable astcanary --disable astdb2sqlite3 --disable astdb2bdb menuselect.makeopts
  menuselect/menuselect --disable MOH-OPSOUND-WAV --enable MOH-OPSOUND-GSM menuselect.makeopts
  menuselect/menuselect --disable EXTRA-SOUNDS-EN-WAV --enable EXTRA-SOUNDS-EN-GSM menuselect.makeopts
  make
}

package(){
  cd ${srcdir}/asterisk-${pkgver}
  make DESTDIR=${pkgdir} install

  mv ${pkgdir}/var/run ${pkgdir}
  rm -rf ${pkgdir}/run
  rm -rf ${pkgdir}/var/log/asterisk

  cd ${srcdir}/asterisk-mini-${_mini_ver}

  install -D -m 644 systemd/sysusers.d/asterisk.conf ${pkgdir}/usr/lib/sysusers.d/asterisk.conf

  for conf in asterisk alsa cdr cdr_adaptive_odbc cdr_syslog cel cel_odbc confbridge extensions indications logger modules musiconhold pjsip res_odbc voicemail; do
      install -D -m 644 asterisk/${conf}.conf ${pkgdir}/etc/asterisk/${conf}.conf
  done

  install -D -m 644 systemd/asterisk.service ${pkgdir}/usr/lib/systemd/system/asterisk.service
  install -D -m 644 systemd/asterisk.service.d/cpu-scheduling-policy.conf ${pkgdir}/usr/lib/systemd/system/asterisk.service.d/cpu-scheduling-policy.conf
  install -D -m 644 systemd/postgresql.service.d/cpu-scheduling-policy.conf ${pkgdir}/usr/lib/systemd/system/postgresql.service.d/cpu-scheduling-policy.conf

  install -D -m 644 alsa/modules-load.d/snd-dummy.conf ${pkgdir}/etc/modules-load.d/snd-dummy.conf
  install -D -m 644 alsa/modprobe.d/snd-dummy.conf ${pkgdir}/etc/modprobe.d/snd-dummy.conf

  install -D -m 644 odbc/odbcinst.ini ${pkgdir}/usr/share/asterisk-mini/odbc/odbcinst.ini
  install -D -m 644 odbc/odbc.ini ${pkgdir}/usr/share/asterisk-mini/odbc/odbc.ini

  for sql in cdr cel voicemessages; do
      install -D -m 644 postgresql/postgresql-${sql}.sql ${pkgdir}/usr/share/asterisk-mini/postgresql/postgresql-${sql}.sql
  done
}
