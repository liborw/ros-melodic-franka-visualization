pkgname="ros-melodic-franka-visualization"
pkgver="0.6.0"
pkgrel=2
pkgdesc="This package contains visualization tools for Franka Emika."
arch=('i686' 'x86_64' 'aarch64' 'armv7h' 'armv6h')
url="http://wiki.ros.org/franka_visualization"
license=('Apache 2.0')

ros_makedepends=(
'ros-melodic-catkin'
)

makedepends=(
'cmake'
'ros-build-tools'
${ros_makedepends[@]}
)

ros_depends=(
'ros-melodic-sensor-msgs'
'ros-melodic-roscpp'
'ros-melodic-libfranka'
'ros-melodic-franka-description'
'ros-melodic-xacro'
)

depends=(
${ros_depends[@]}
)

provides=($pkgname)
conflicts=($pkgname)

_dir="franka_ros-$pkgver/franka_visualization"
source=("$pkgname-$pkgver.tar.gz::https://github.com/frankaemika/franka_ros/archive/$pkgver.tar.gz")
sha256sums=(6bfc7f743569e7491d44b82e1b9c39ace55881b7f42e4952e202e13d1e70a6b9)


build() {
	# Use ROS environment variables
  	source /usr/share/ros-build-tools/clear-ros-env.sh
  	[ -f /opt/ros/melodic/setup.bash ] && source /opt/ros/melodic/setup.bash

	# Create build directory
  	[ -d ${srcdir}/build ] || mkdir ${srcdir}/build
  	cd ${srcdir}/build

	# Build project
	cmake ${srcdir}/${_dir} \
	      -DCMAKE_BUILD_TYPE=Release \
	      -DCATKIN_BUILD_BINARY_PACKAGE=ON \
	      -DCMAKE_INSTALL_PREFIX=/opt/ros/melodic \
	      -DPYTHON_EXECUTABLE=/usr/bin/python3 \
	      -DSETUPTOOLS_DEB_LAYOUT=OFF
	make
}

package() {
	cd "${srcdir}/build"
	make DESTDIR="${pkgdir}/" install
}
