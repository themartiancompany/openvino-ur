# Maintainer: Daniel Bermond <dbermond@archlinux.org>

# only Intel GPUs are supported:
# https://github.com/openvinotoolkit/openvino/issues/452#issuecomment-722941119

_py="python"
_pkg=openvino
_proj="${_pkg}toolkit"
pkgname="${_pkg}"
pkgver=2024.4.0
pkgrel=2
_pkgdesc=(
  "A toolkit for developing artificial"
  "inteligence and deep learning applications"
)
pkgdesc="${_pkgdesc[*]}"
arch=(
  'x86_64'
  'i686'
  'arm'
  'aarch64'
  'armv7l'
  'armv6l'
  'mips'
  'powerpc'
)
url="https://docs.${_proj}.org"
license=(
  'Apache-2.0'
)
depends=(
  'pugixml'
  'onetbb'
)
optdepends=(
  'intel-compute-runtime: for Intel GPU plugin'
  'ocl-icd: for Intel GPU plugin'
  'level-zero-loader: for Intel NPU plugin'
  'snappy: for tensorflow frontend'
  "${_py}: for Python API"
  "${_py}-numpy: for Python API"
  "${_py}-packaging: for Python API"
  "${_py}-pillow: for Python API"
)
makedepends=(
  'git'
  'git-lfs'
  'cmake'
  'opencl-clhpp'
  'opencl-headers'
  'ocl-icd'
  'opencv'
  'snappy'
  "${_py}"
  "${_py}-setuptools"
  'fdupes'
  'patchelf'
  'shellcheck'
)
provides=(
  "intel-${_pkg}"
)
conflicts=(
  "intel-${_pkg}"
)
replaces=(
  "intel-${_pkg}"
)
options=(
  '!emptydirs'
)
_http="https://github.com"
_ns="${_proj}"
_url="${_http}/${_ns}/${_pkg}"
source=(
  "git+${_url}.git#tag=${pkgver}"
  "oneDNN-${_proj}::git+${_http}/${_ns}/oneDNN.git"
  "git+${_http}/herumi/xbyak.git"
  "git+${_http}/madler/zlib.git"
  "git+${_http}/zeux/pugixml.git"
  "git+${_http}/gflags/gflags.git"
  "googletest-${_proj}::git+${_http}/${_ns}/googletest.git"
  "git+${_http}/KhronosGroup/OpenCL-ICD-Loader.git"
  "git+${_http}/KhronosGroup/OpenCL-Headers.git"
  "git+${_http}/KhronosGroup/OpenCL-CLHPP.git"
  "git+${_http}/onnx/onnx.git"
  "git+${_http}/protocolbuffers/protobuf.git"
  "git+${_http}/pybind/pybind11.git"
  "git+${_http}/intel/ittapi.git"
  "git+${_http}/nithinn/ncc.git"
  "git+${_http}/oneapi-src/oneDNN.git"
  "git+${_http}/${_ns}/open_model_zoo.git"
  "git+${_http}/nlohmann/json.git"
  "git+${_http}/google/flatbuffers.git"
  "git+${_http}/google/snappy.git"
  "git+${_http}/ARM-software/ComputeLibrary.git"
  "git+${_http}/${_ns}/mlas.git"
  "git+${_http}/oneapi-src/level-zero.git"
  "git+${_http}/intel/level-zero-npu-extensions.git"
  "git+${_http}/${_ns}/telemetry.git"
  "git+${_http}/libxsmm/libxsmm.git"
  "git+${_http}/${_ns}/shl.git"
  "${_pkg}.conf"
  'setupvars.sh'
  "010-${_pkg}-disable-werror.patch"
  "020-${_pkg}-use-protobuf-shared-libs.patch"
  "030-${_pkg}-level-zero-disable-werror.patch"
)
sha256sums=(
  '556f335d199fb4c3dcd919f27eeca120eafc1814f0f4d42f2b1b8e681bc136e4'
  'SKIP'
  'SKIP'
  'SKIP'
  'SKIP'
  'SKIP'
  'SKIP'
  'SKIP'
  'SKIP'
  'SKIP'
  'SKIP'
  'SKIP'
  'SKIP'
  'SKIP'
  'SKIP'
  'SKIP'
  'SKIP'
  'SKIP'
  'SKIP'
  'SKIP'
  'SKIP'
  'SKIP'
  'SKIP'
  'SKIP'
  'SKIP'
  'SKIP'
  'SKIP'
  '335a55533ab26bd1f63683921baf33b8e8e3f2732a94554916d202ee500f90af'
  'e5024ad3382f285fe63dc58faca379f11a669bbe9f5d90682c59ad588aab434c'
  'c12e827abec2de978ab22f0c7667ebd632fb551e54aecbeade0cff1491dae3f3'
  '9c10b6d9cc6ba4722fae449f401875c538d5aa544d89edf3260fe766f946dbb8'
  '51dc09683a319f9a939369d47d6752b41fea61737e6886a5814fc75f3dc1cef1'
)

export \
  GIT_LFS_SKIP_SMUDGE='1'

_submodule_url_config() {
  local \
    _submodule_path="${1}" \
    _directory="${2}"
  git \
    -C \
    "${_pkg}" \
    config \
      --local \
        "submodule.${_submodule_path}.url" \
	"${_directory}"
}

_submodules_url_config() {
  _submodule_url_config \
    "src/plugins/intel_cpu/thirdparty/onednn" \
    "${srcdir}/oneDNN-${_proj}"
  _submodule_url_config \
    "thirdparty/xbyak" \
    "${srcdir}/xbyak"
  _submodule_url_config \
    "thirdparty/zlib/zlib" \
    "${srcdir}/zlib"
  _submodule_url_config \
    "thirdparty/pugixml" \
    "${srcdir}/pugixml"
  _submodule_url_config \
    "thirdparty/gflags/gflags" \
    "${srcdir}/gflags"
  _submodule_url_config \
    "thirdparty/gtest/gtest" \
    "${srcdir}/googletest-openvinotoolkit"
  _submodule_url_config \
    "thirdparty/ocl/icd_loader" \
    "${srcdir}/OpenCL-ICD-Loader"
  _submodule_url_config \
    "thirdparty/ocl/cl_headers" \
    "${srcdir}/OpenCL-Headers"
  _submodule_url_config \
    "thirdparty/ocl/clhpp_headers" \
    "${srcdir}/OpenCL-CLHPP"
  _submodule_url_config \
    "thirdparty/onnx" \
    "${srcdir}/onnx"
  _submodule_url_config \
    "thirdparty/protobuf" \
    "${srcdir}/protobuf"
  _submodule_url_config \
    "src/bindings/python/thirdparty/pybind11" \
    "${srcdir}/pybind11"
  _submodule_url_config \
    "thirdparty/ittapi/ittapi" \
    "${srcdir}/ittapi"
  _submodule_url_config \
    "ncc" \
    "${srcdir}/ncc"
  _submodule_url_config \
    "thirdparty/onednn_gpu" \
    "${srcdir}/oneDNN"
  _submodule_url_config \
    "tools/pot/thirdparty/open_model_zoo" \
    "${srcdir}/open_model_zoo"
  _submodule_url_config \
    "thirdparty/json/nlohmann_json" \
    "${srcdir}/json"
  _submodule_url_config \
    "thirdparty/flatbuffers/flatbuffers" \
    "${srcdir}/flatbuffers"
  _submodule_url_config \
    "thirdparty/snappy" \
    "${srcdir}/snappy"
  _submodule_url_config \
    "ARMComputeLibrary" \
    "${srcdir}/ComputeLibrary"
  _submodule_url_config \
    "src/plugins/intel_cpu/thirdparty/mlas" \
    "${srcdir}/mlas"
  _submodule_url_config \
    "src/plugins/intel_npu/thirdparty/level-zero" \
    "${srcdir}/level-zero"
  _submodule_url_config \
    "src/plugins/intel_npu/thirdparty/level-zero-ext" \
    "${srcdir}/level-zero-npu-extensions"
  _submodule_url_config \
    "thirdparty/telemetry" \
    "${srcdir}/telemetry"
  _submodule_url_config \
    "src/plugins/intel_cpu/thirdparty/libxsmm" \
    "${srcdir}/libxsmm"
  _submodule_url_config \
    "src/plugins/intel_cpu/thirdparty/shl" \
    "${srcdir}/shl"

}

prepare() {
  git \
    -C \
      "${_pkg}" \
    lfs \
      install \
        --local
  git \
    -C \
      "${_pkg}" \
    lfs \
      pull \
        "$(printf \
	     '%s' \
	     "${source[0]/git+/}" | \
	     sed \
	       's/#.*$//')"
  git \
    -C \
      "${_pkg}" \
    submodule \
      init
  _submodules_url_config
  git \
    -C \
      "${_pkg}" \
      -c \
        protocol.file.allow='always' \
    submodule \
      update
  patch \
    -d \
      "${_pkg}" \
    -Np1 \
    -i \
    "${srcdir}/010-${_pkg}-disable-werror.patch"
  patch \
    -d \
      "${_pkg}" \
    -Np1 \
    -i \
    "${srcdir}/020-${_pkg}-use-protobuf-shared-libs.patch"
  patch \
    -d \
      "${_pkg}/src/plugins/intel_npu/thirdparty/level-zero" \
    -Np1 \
    -i \
    "${srcdir}/030-${_pkg}-level-zero-disable-werror.patch"
}

build() {
  local \
    _cmake_opts=()
  # fix warning: "_FORTIFY_SOURCE" redefined
  # note: upstream forces _FORTIFY_SOURCE=2
  export \
    CFLAGS="${CFLAGS/-Wp,-D_FORTIFY_SOURCE=?/}" \
    CXXFLAGS="${CXXFLAGS/-Wp,-D_FORTIFY_SOURCE=?/}"
  _cmake_opts+=(
    -DBUILD_TESTING:BOOL='OFF'
    -DCMAKE_BUILD_TYPE:STRING='Release'
    -DCMAKE_INSTALL_PREFIX:PATH="/opt/intel/${_pkg}"
    -DENABLE_SSE42:BOOL='OFF'
    -DENABLE_AVX2:BOOL='OFF'
    -DENABLE_AVX512F:BOOL='OFF'
    -DENABLE_CLANG_FORMAT:BOOL='OFF'
    -DENABLE_INTEL_NPU:BOOL='OFF'
    -DENABLE_NCC_STYLE:BOOL='OFF'
    -DENABLE_PYTHON:BOOL='ON'
    -DENABLE_SYSTEM_PUGIXML:BOOL='ON'
    -DENABLE_SYSTEM_TBB:BOOL='ON'
    -DENABLE_SYSTEM_OPENCL:BOOL='ON'
    -DENABLE_SYSTEM_PROTOBUF:BOOL='OFF'
    -DENABLE_SYSTEM_FLATBUFFERS:BOOL='OFF'
    -DENABLE_SYSTEM_SNAPPY:BOOL='ON'
    -Wno-dev
  )
  # note: does not accept 'None' build type
  # note: npu plugin needs avx and does not build with the default x86_64 arch
  cmake \
    -B build \
    -S "${_pkg}" \
    -G 'Unix Makefiles' \
    "${_cmake_opts[@]}"
  cmake \
    --build \
      build
}

package() {
  DESTDIR="$pkgdir" \
  cmake \
    --install \
      build
  install \
    -Dm644 \
    "${_pkg}.conf" \
    -t \
    "${pkgdir}/etc/ld.so.conf.d"
}
