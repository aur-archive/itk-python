# Maintainer: Christofer Bertonha <chritoferbertonha@gmail.com>

pkgname=itk-python
pkgver=3.20.1
pkgrel=1
pkgdesc='Insight Segmentation and Registration Toolkit (ITK).'
arch=('i686' 'x86_64')
url='http://www.itk.org/'
license=('BSD')
depends=('python2' 'zlib' 'libpng' 'libtiff' 'vtk')
makedepends=('cmake' 'python2' 'zlib' 'libpng' 'libtiff' 'vtk' 'cableswig-cvs')
source=("http://downloads.sourceforge.net/project/itk/itk/${pkgver:0:4}/InsightToolkit-${pkgver}.tar.gz")
provides=('insight-toolkit')
conflicts=('insight-toolkit')
md5sums=('90342ffa78bd88ae48b3f62866fbf050')

build() {
  cd ${srcdir}/InsightToolkit-${pkgver}

  sed \
    -e 's#png_set_gray_1_2_4_to_8#png_set_expand_gray_1_2_4_to_8#g' \
    -i Code/IO/itkPNGImageIO.cxx

  mkdir -p ../build && cd ../build

  cmake \
    -DCMAKE_BUILD_TYPE:STRING=Release \
    -DBUILD_TESTING:BOOL=OFF \
    -DBUILD_EXAMPLES:BOOL=OFF \
    -DBUILD_SHARED_LIBS:BOOL=ON \
    -DCMAKE_INSTALL_PREFIX:FILEPATH=/usr \
    -DITK_USE_SYSTEM_GDCM:BOOL=ON \
    -DITK_USE_SYSTEM_LIBXML2:BOOL=ON \
    -DITK_USE_SYSTEM_PNG:BOOL=ON \
    -DITK_USE_SYSTEM_TIFF:BOOL=ON \
    -DITK_USE_SYSTEM_ZLIB:BOOL=ON \
    -DITK_USE_REVIEW:BOOL=ON \
    -DUSE_WRAP_ITK:BOOL=ON \
    -DWRAP_ITK_JAVA:BOOL=OFF \
    -DWRAP_ITK_TCL:BOOL=OFF \
    -DWRAP_ITK_PYTHON:BOOL=ON \
    ../InsightToolkit-${pkgver}

  make
}

package() {
  cd ${srcdir}/build

  make DESTDIR=${pkgdir} install

  # install BSD license
  install -d ${pkgdir}/usr/share/licenses/insight-toolkit
  install -m 644 ../InsightToolkit-${pkgver}/Copyright.txt \
    ${pkgdir}/usr/share/licenses/insight-toolkit
}
