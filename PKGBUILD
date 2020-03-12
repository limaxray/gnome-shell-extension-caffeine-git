# Maintainer: XZS <d dot f dot fischer at web dot de>
# Contributor: sanduhrs <stefan.auditor@erdfisch.de>
# This PKGBUILD is maintained on GitHub <https://github.com/dffischer/gnome-shell-extensions>.
# You may find it convenient to file issues and pull requests there.

pkgname=gnome-shell-extension-caffeine-git
pkgver=r130
pkgrel=1
_extid="caffeine@patapon.info"
pkgdesc="Fill the cup to inhibit auto suspend and screensaver."
arch=(any)
url="https://github.com/eonpatapon/gnome-shell-extension-caffeine"
license=(GPLv2)
install=gschemas.install

depends=('gnome-shell')
makedepends=('git')
source=("${pkgname}::git+${url}")
sha256sums=('SKIP')

pkgver() {
	cd "${srcdir}/${pkgname}"
	printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

build() {
  cd "${srcdir}/${pkgname}"
  msg2 'Updating locales...'
  ./update-locale.sh &> /dev/null
}
package() {
	usrdir="${pkgdir}/usr/share"
	extdir="${usrdir}/gnome-shell/extensions/${_extid}"
	schdir="${usrdir}/glib-2.0/schemas"

	cd "${srcdir}/${pkgname}/${_extid}"

  	msg2 'Installing extension...'
	install -dm755 "${extdir}"
	for file in $(find -maxdepth 1 -type f -iregex '.*\.\(js\|json\|css\)$'); do
		install -m644 "${file}" "${extdir}"
	done

  	msg2 'Installing icons...'
	install -dm755 "${extdir}/icons"
	for file in $(find 'icons' -maxdepth 1 -type f -iregex '.*\.\(svg\|png\)$'); do
		install -m644 "${file}" "${extdir}/icons"
	done

  	msg2 'Installing translations...'
    for dir in $(find 'locale' -type d -name 'LC_MESSAGES'); do
		install -dm755 "${usrdir}/${dir}"
		for file in $(find "${dir}" -type f -iregex '.*\.mo$'); do
			install -m644 "${file}" "${usrdir}/${dir}"
		done
	done

	msg2 'Installing schemas...'
	install -dm755 "${schdir}"
	for file in $(find 'schemas' -maxdepth 1 -type f -iregex '.*\.xml$'); do
		install -m644 "${file}" "${schdir}"
	done
}



