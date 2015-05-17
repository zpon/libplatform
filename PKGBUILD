buildarch=4

pkgname=libplatform
pkgver=1.0.5_20150517
pkgrel=1
pkgdesc="Pulse-Eight's Platform support library used by libCEC and binary add-ons for Kodi"
arch=('armv7h')
url="https://github.com/Pulse-Eight/platform"
license=('GPL')
depends=('udev' 'lockdev')
conflicts=('libplatform')
provides=('libplatform')
makedepends=('git')

_gitname="platform"
_gitroot="git://github.com/Pulse-Eight"
_gitbranch="master"

prepare() {
  cd "${srcdir}"

  msg2 "Connecting to GIT server..."
  
  if [[ -d "${_gitname}" ]]; then
     cd "${_gitname}" && git pull origin "$_gitbranch"
     msg2 "The local files are updated."
  else
     git clone --recursive --branch ${_gitbranch} --depth 1 "${_gitroot}/${_gitname}"
  fi
  
  msg2 "GIT checkout done or server timeout." 
}

build() {
  cd "${srcdir}/${_gitname}"

  # Remove build dir if it already exist
  if [ -d build ] ; then
    rm -r build
  fi

  mkdir build
  cd build
  cmake -DCMAKE_INSTALL_PREFIX=/usr -DBUILD_SHARED_LIBS=1 ..
  make
}

package() {
  cd "${srcdir}/${_gitname}"
  cd build
  # Running make install
  make DESTDIR="${pkgdir}" install
}
