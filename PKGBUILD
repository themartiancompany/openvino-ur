# Maintainer: Daniel Bermond <dbermond@archlinux.org>

pkgname=openvino
pkgver=2022.2.0
pkgrel=2
pkgdesc='A toolkit for developing artificial inteligence and deep learning applications'
arch=('x86_64')
url='https://docs.openvinotoolkit.org/'
license=('Apache')
depends=('protobuf' 'numactl' 'libxml2')
# GPU (clDNN) plugin: only Intel GPUs are supported:
# https://github.com/openvinotoolkit/openvino/issues/452#issuecomment-722941119
optdepends=('intel-compute-runtime: for GPU (clDNN) plugin'
            'ocl-icd: for GPU (clDNN) plugin'
            'libusb: for Myriad plugin'
            'python: for Python API'
            'python-numpy: for Python API'
            'cython: for Python API'
            'python-py-cpuinfo: for benchmark tool'
            'python-progress: for benchmark tool'
            'opencv: for benchmark and cross_check tools')
makedepends=('git' 'git-lfs' 'cmake' 'intel-compute-runtime' 'libusb' 'ocl-icd' 'opencv'
             'python' 'cython' 'shellcheck')
provides=('intel-openvino')
conflicts=('intel-openvino')
replaces=('intel-openvino')
options=('!emptydirs')
# supported firmwares: VPU_SUPPORTED_FIRMWARES in src/plugins/intel_myriad/myriad_dependencies.cmake
_firmware_ver=20220307_34 # FIRMWARE_PACKAGE_VERSION in src/plugins/intel_myriad/myriad_dependencies.cmake
_gnaver=03.00.00.1455.2 # GNA_VERSION in cmake/dependencies.cmake
_tbbver=2020_20200415 # cmake/dependencies.cmake
_tbbbind_ver=2_5_static_lin_v2 # cmake/dependencies.cmake
source=("git+https://github.com/openvinotoolkit/openvino.git#tag=${pkgver}"
        "https://download.01.org/opencv/master/openvinotoolkit/thirdparty/unified/VPU/pcie-ma2x8x/firmware_pcie-ma2x8x_${_firmware_ver}.zip"
        "https://download.01.org/opencv/master/openvinotoolkit/thirdparty/unified/VPU/usb-ma2x8x/firmware_usb-ma2x8x_${_firmware_ver}.zip"
        "https://download.01.org/opencv/master/openvinotoolkit/thirdparty/unified/GNA/GNA_${_gnaver}.zip"
        "https://download.01.org/opencv/master/openvinotoolkit/thirdparty/linux/tbb${_tbbver}_lin_strip.tgz"
        "https://download.01.org/opencv/master/openvinotoolkit/thirdparty/linux/tbbbind_${_tbbbind_ver}.tgz"
        'oneDNN-openvinotoolkit'::'git+https://github.com/openvinotoolkit/oneDNN.git'
        'git+https://github.com/herumi/xbyak.git'
        'git+https://github.com/madler/zlib.git'
        'git+https://github.com/zeux/pugixml.git'
        'git+https://github.com/opencv/ade.git'
        'git+https://github.com/gflags/gflags.git'
        'googletest-openvinotoolkit'::'git+https://github.com/openvinotoolkit/googletest.git'
        'git+https://github.com/KhronosGroup/OpenCL-ICD-Loader.git'
        'git+https://github.com/KhronosGroup/OpenCL-Headers.git'
        'git+https://github.com/KhronosGroup/OpenCL-CLHPP.git'
        'git+https://github.com/onnx/onnx.git'
        'git+https://github.com/protocolbuffers/protobuf.git'
        'git+https://github.com/pybind/pybind11.git'
        'git+https://github.com/intel/ittapi.git'
        'git+https://github.com/nithinn/ncc.git'
        'git+https://github.com/oneapi-src/oneDNN.git'
        'git+https://github.com/openvinotoolkit/open_model_zoo.git'
        'git+https://github.com/nlohmann/json.git'
        'git+https://github.com/pboettch/json-schema-validator.git'
        'openvino.conf'
        'setupvars.sh'
        '010-ade-disable-werror.patch'
        '020-openvino-use-protobuf-shared-libs.patch')
noextract=("firmware_usb-ma2x8x_${_firmware_ver}.zip"
           "firmware_pcie-ma2x8x_${_firmware_ver}.zip")
sha256sums=('SKIP'
            'aabff3d817431792ef9e17056448979c2cdbb484ad4b0af9e68cb874ee10eef5'
            '877c4e1616d14a94dd2764f4f32f1c1aa2180dcd64ad1823b31efdc3f56ad593'
            'e52785d3f730fefb4e794bb7ab40c8676537ef2f7c69c5b4bb89a5d3cc0bbe60'
            '95b2f3b0b70c7376a0c7de351a355c2c514b42c4966e77e3e34271a599501008'
            '865e7894c58402233caf0d1b288056e0e6ab2bf7c9d00c9dc60561c484bc90f4'
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
            '48b6a93bb54c36f9bc87a7f326b0a634f752f34f57f90a60dccc13f92fd96a9d'
            'cfcc5af35d7a50f83c780716f69f8a800b14bcf143f7abafd31a7a0dcb8c9ae8'
            '502fcbb3fcbb66aa5149ad2cc5f1fa297b51ed12c5c9396a16b5795a03860ed0'
            'f80b04310c3ba71acfbc04e4e83784ab45540659d257afc3b0924c0eef9921b7')

export GIT_LFS_SKIP_SMUDGE='1'

prepare() {
    git -C openvino lfs install --local
    git -C openvino lfs pull "$(printf '%s' "${source[0]/git+/}" | sed 's/#.*$//')"
    
    git -C openvino submodule init
    git -C openvino config --local submodule.src/plugins/intel_cpu/thirdparty/onednn.url "${srcdir}/oneDNN-openvinotoolkit"
    git -C openvino config --local submodule.thirdparty/xbyak.url "${srcdir}/xbyak"
    git -C openvino config --local submodule.thirdparty/zlib/zlib.url "${srcdir}/zlib"
    git -C openvino config --local submodule.thirdparty/pugixml.url "${srcdir}/pugixml"
    git -C openvino config --local submodule.thirdparty/ade.url "${srcdir}/ade"
    git -C openvino config --local submodule.thirdparty/gflags/gflags.url "${srcdir}/gflags"
    git -C openvino config --local submodule.thirdparty/gtest/gtest.url "${srcdir}/googletest-openvinotoolkit"
    git -C openvino config --local submodule.thirdparty/ocl/icd_loader.url "${srcdir}/OpenCL-ICD-Loader"
    git -C openvino config --local submodule.thirdparty/ocl/cl_headers.url "${srcdir}/OpenCL-Headers"
    git -C openvino config --local submodule.thirdparty/ocl/clhpp_headers.url "${srcdir}/OpenCL-CLHPP"
    git -C openvino config --local submodule.thirdparty/onnx.url "${srcdir}/onnx"
    git -C openvino config --local submodule.thirdparty/protobuf.url "${srcdir}/protobuf"
    git -C openvino config --local submodule.src/bindings/python/thirdparty/pybind11.url "${srcdir}/pybind11"
    git -C openvino config --local submodule.thirdparty/ittapi/ittapi.url "${srcdir}/ittapi"
    git -C openvino config --local submodule.ncc.url "${srcdir}/ncc"
    git -C openvino config --local submodule.thirdparty/onednn_gpu.url "${srcdir}/oneDNN"
    git -C openvino config --local submodule.tools/pot/thirdparty/open_model_zoo.url "${srcdir}/open_model_zoo"
    git -C openvino config --local submodule.thirdparty/json/nlohmann_json.url "${srcdir}/json"
    git -C openvino config --local submodule.thirdparty/json/nlohmann_json_schema_validator.url "${srcdir}/json-schema-validator"
    git -C openvino -c protocol.file.allow='always' submodule update
    
    mkdir -p openvino/temp/vpu/firmware/{pcie,usb}-ma2x8x
    bsdtar -xf "firmware_pcie-ma2x8x_${_firmware_ver}.zip" -C openvino/temp/vpu/firmware/pcie-ma2x8x
    bsdtar -xf "firmware_usb-ma2x8x_${_firmware_ver}.zip"  -C openvino/temp/vpu/firmware/usb-ma2x8x
    cp -af "gna_${_gnaver}" openvino/temp
    cp -af tbb openvino/temp
    cp -af "tbbbind_${_tbbbind_ver/_static*/}" openvino/temp
    
    printf '%s\n' "${source[1]}" > openvino/temp/vpu/firmware/pcie-ma2x8x/ie_dependency.info
    printf '%s\n' "${source[2]}" > openvino/temp/vpu/firmware/usb-ma2x8x/ie_dependency.info
    printf '%s\n' "${source[3]}" > "openvino/temp/gna_${_gnaver}/ie_dependency.info"
    printf '%s\n' "${source[4]}" > openvino/temp/tbb/ie_dependency.info
    printf '%s\n' "${source[5]}" > "openvino/temp/tbbbind_${_tbbbind_ver/_static*/}/ie_dependency.info"
    
    patch -d openvino/thirdparty/ade -Np1 -i "${srcdir}/010-ade-disable-werror.patch"
    patch -d openvino -Np1 -i "${srcdir}/020-openvino-use-protobuf-shared-libs.patch"
}

build() {
    local _ocvmaj
    _ocvmaj="$(opencv_version | awk -F'.' '{ print $1 }')"
    
    local -x OpenCV_DIR="/usr/lib/cmake/opencv${_ocvmaj}"
    
    # note: does not accept 'None' build type
    cmake -B build -S openvino \
        -DBUILD_TESTING:BOOL='OFF' \
        -DCMAKE_BUILD_TYPE:STRING='Release' \
        -DCMAKE_INSTALL_PREFIX:PATH='/opt/intel/openvino' \
        -DENABLE_AVX512F:BOOL='OFF' \
        -DENABLE_PROFILING_ITT:BOOL='OFF' \
        -DENABLE_PYTHON:BOOL='ON' \
        -DENABLE_OPENCV:BOOL='OFF' \
        -DENABLE_CLANG_FORMAT:BOOL='OFF' \
        -DENABLE_NCC_STYLE:BOOL='OFF' \
        -DENABLE_SYSTEM_PROTOBUF:BOOL='ON' \
        -DENABLE_ONEDNN_FOR_GPU:BOOL='OFF' \
        -DTREAT_WARNING_AS_ERROR:BOOL='OFF' \
        -Wno-dev
    make -C build
}

package() {
    make -C build DESTDIR="$pkgdir" install
    install -D -m644 openvino.conf -t "${pkgdir}/etc/ld.so.conf.d"
    
    #local _gnaver
    #local _gnasover
    #local _gnasover_full
    #local _gnadir="${pkgdir}/opt/intel/openvino/runtime/lib/intel64"
    #_gnaver="$(find openvino/temp -maxdepth 1 -type d -name 'gna_*' | sed 's/.*_//')"
    #_gnasover="$(find -L "$_gnadir" -type f -regextype 'posix-basic' -regex '.*/libgna\.so\.[0-9]*$' | sed 's/.*\.//')"
    #_gnasover_full="$(find -L "$_gnadir" -type f -regextype 'posix-basic' -regex '.*/libgna\.so\.[0-9]*\..*' | sed 's/.*\.so\.//')"
    
    #rm "${_gnadir}/libgna.so."{"${_gnasover}","${_gnasover_full}"}
    #mv "${_gnadir}/libgna.so"{,."${_gnasover_full}"}
    #ln -s "libgna.so.${_gnasover_full}" "${_gnadir}/libgna.so.${_gnasover}"
    #ln -s "libgna.so.${_gnasover}" "${_gnadir}/libgna.so"
    
    #cp -dr --no-preserve='ownership' "openvino/temp/gna_${_gnaver}/include" \
    #    "${pkgdir}/opt/intel/openvino/runtime/include/gna"
    #chmod -R a+r "${pkgdir}/opt/intel/openvino/runtime/include/gna"
}
