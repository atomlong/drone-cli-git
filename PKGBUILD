# Maintainer: Robin Appelman <robin@icewind.nl>

pkgname=drone-cli-git
pkgver=1.4.0.r2.g75f1ec6
pkgrel=1
pkgdesc='Drone CLI'
arch=('any')
url='http://docs.drone.io/cli-installation/'
license=('Apache')
makedepends=('go')
source=("git+https://github.com/drone/drone-cli.git")
sha256sums=('SKIP')
provides=('drone-cli')
conflicts=('drone-cli')

_gitname='drone-cli'

pkgver() {
  cd "$_gitname"
  git describe --long --tags | sed 's/^v//;s/\([^-]*-g\)/r\1/;s/-/./g'
}

build() {
  cd "${_gitname}"
  go build \
    -buildmode=pie \
    -trimpath \
    -modcacherw \
    -ldflags "-X main.version=${pkgver} -extldflags ${LDFLAGS}" \
    -o drone ./drone
}

package() {
  cd "${_gitname}"
  # binary
  install -D -m755 drone/drone "${pkgdir}/usr/bin/drone"
  # doc files
  install -D -m644 README.md "${pkgdir}/usr/share/doc/${pkgname}/README.md"
}
