
pkgname='asterisk-mini'
pkgver='16.2.0'
pkgrel=1
pkgdesc='A complete PBX solution'
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
provides=("asterisk=${pkgver}")
depends=('popt' 'libxml2' 'jansson' 'libxslt' 'sqlite3' 'zlib' 'alsa-lib' 'gsm' 'libilbc' 'speexdsp' 'unixodbc' 'libedit')
makedepends=('curl' 'lua' 'libsrtp' 'speex')
optdepends=('alsa-utils' 'curl' 'lua' 'libsrtp' 'psqlodbc' 'mariadb-connector-odbc' 'sqliteodbc' 'asterisk-g72x')
install='asterisk.install'

_ast_dl='http://downloads.asterisk.org/pub/telephony'
_pjp_dl='http://www.pjsip.org/release'
_mini_ver='1.1'
source=("${_ast_dl}/asterisk/releases/asterisk-${pkgver}.tar.gz"
        "${_pjp_dl}/2.8/pjproject-2.8.tar.bz2"
	"pjproject-2.8.md5::${_pjp_dl}/2.8/MD5SUM.TXT"
	"${_ast_dl}/sounds/releases/asterisk-core-sounds-en-gsm-1.6.1.tar.gz"
	"${_ast_dl}/sounds/releases/asterisk-core-sounds-en-gsm-1.6.1.tar.gz.sha1"
	"${_ast_dl}/sounds/releases/asterisk-extra-sounds-en-gsm-1.5.2.tar.gz"
	"${_ast_dl}/sounds/releases/asterisk-extra-sounds-en-gsm-1.5.2.tar.gz.sha1"
	"${_ast_dl}/sounds/releases/asterisk-moh-opsound-gsm-2.03.tar.gz"
	"${_ast_dl}/sounds/releases/asterisk-moh-opsound-gsm-2.03.tar.gz.sha1"
	"asterisk-mini-${_mini_ver}.tar.gz::http://github.com/RoEdAl/asterisk-mini/archive/v${_mini_ver}.tar.gz")
sha256sums=('6bbe4537bd97b10bdfce5ef70524905ea27aede621c50ebf6a459d433bd74e2b'
            '503d0bd7f9f13dc1492ac9b71b761b1089851fbb608b9a13996edc3c42006f79'
            '291c890edd14b7a873c5c0eca67adef82eab8b3d7cb9800e6acf92731ae63a8b'
            'd79c3d2044d41da8f363c447dfccc140be86b4fcc41b1ca5a60a80da52f24f2d'
            'c5be5c60f1450419494008c195c08f8aa1e88d6d978001a310c9516f93d18bfb'
            'a872eb41868a75b8b4ea677d46f2659870c7190037e1d97853b4b060e60e9d7c'
            '92c00ca0148f11e85a3af8bfa6ceb4e6091cb1c053a7e29c88484192c1d9ff25'
            'b0fb7b52b05094a3d5298c965e98717f9907d65a9ec47604ac05d8b06a96e940'
            '5db48fc22600cbf3d0ca4da298627c2a35b89b9e9f8ea1d24c466a5b0362cde0'
            '2ef1237bf565d371790b9383da2727cf71726773a2ebaf86ea181e41f44797c0')
noextract=(
	'pjproject-2.7.2.tar.bz2'
	'asterisk-core-sounds-en-gsm-1.6.1.tar.gz'
	'asterisk-extra-sounds-en-gsm-1.5.2.tar.gz'
	'asterisk-moh-opsound-gsm-2.03.tar.gz')

build(){
  cd asterisk-${pkgver}

  export CFLAGS="${CFLAGS} -ffile-prefix-map=$(pwd)/=/"
  export CXXFLAGS="${CXXFLAGS} -ffile-prefix-map=$(pwd)/=/"

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
    --without-postgres \
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
    --without-unbound \
    --without-vorbis \
    --without-ogg \
    --without-opus \
    --without-opusfile

  make menuselect.makeopts
  menuselect/menuselect \
    --enable ODBC_STORAGE \
    --disable codec_speex \
    --enable func_speex  \
    --enable cdr_syslog \
    --disable format_siren7 \
    --disable format_siren14 \
    --disable format_g719 \
    --disable format_g723 \
    --disable format_h263 \
    --disable format_h264 \
    --disable res_format_attr_opus \
    --disable res_fax \
    --disable res_format_attr_h263 \
    --disable res_format_attr_h264 \
    --disable res_config_pgsql \
    --disable res_format_attr_siren14 \
    --disable res_format_attr_siren7 \
    --disable res_format_attr_vp8 \
    --disable res_speech \
    --disable res_config_ldap \
    --disable res_format_attr_silk \
    --enable res_snmp \
    --disable app_festival \
    --disable app_mp3 \
    --disable app_ices \
    --disable app_image \
    --disable app_sms \
    --enable app_flash \
    --disable astdb2sqlite3 \
    --disable astdb2bdb \
    --disable MOH-OPSOUND-WAV \
    --enable MOH-OPSOUND-GSM \
    --disable EXTRA-SOUNDS-EN-WAV \
    --enable EXTRA-SOUNDS-EN-GSM \
    menuselect.makeopts

  make
}

package(){
  cd asterisk-${pkgver}

  make DESTDIR=${pkgdir} install

  mv ${pkgdir}/var/run ${pkgdir}
  rm -rf ${pkgdir}/run
  rm -rf ${pkgdir}/var/log

  cd ../asterisk-mini-${_mini_ver}

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
