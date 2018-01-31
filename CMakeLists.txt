project(libnyquist)

include( FindPkgConfig )
include( CheckLibraryExists )

pkg_search_module(LIBGPAC gpac)
pkg_search_module(LIBMODPLUG libmodplug)
pkg_search_module(LIBOPUSFILE opusfile)
pkg_search_module(LIBVORBIS libvorbis)
pkg_search_module(LIBVORBISFILE libvorbisfile)
pkg_search_module(LIBOGG libogg)
pkg_search_module(LIBFLAC flac)
pkg_search_module(LIBOPUS opus)
pkg_search_module(LIBMPCDEC libmpcdec)
pkg_search_module(LIBWAVPACK wavpack)

check_library_exists(vorbisfile ov_streams "" HAVE_LIBVORBISFILE)
check_library_exists(mpcdec mpc_demux_decode "" HAVE_LIBMPCDEC)

set(SOURCES
    include/libnyquist/AudioDecoder.h
    include/libnyquist/CafDecoder.h
    include/libnyquist/Common.h
    include/libnyquist/Dither.h
    include/libnyquist/FlacDecoder.h
    include/libnyquist/IMA4Util.h
    include/libnyquist/ModplugDecoder.h
    include/libnyquist/MusepackDecoder.h
    include/libnyquist/OpusDecoder.h
    include/libnyquist/PostProcess.h
    include/libnyquist/RiffUtils.h
    include/libnyquist/VorbisDecoder.h
    include/libnyquist/WavDecoder.h
    include/libnyquist/WavEncoder.h
    include/libnyquist/WavPackDecoder.h
    src/AudioDecoder.cpp
    src/CafDecoder.cpp
    src/Common.cpp
    src/FlacDecoder.cpp
#    src/FlacDependencies.c
    src/ModplugDecoder.cpp
#    src/ModplugDependencies.cpp
    src/MusepackDecoder.cpp
#    src/MusepackDependencies.c
    src/OpusDecoder.cpp
#    src/OpusDependencies.c
    src/RiffUtils.cpp
    src/VorbisDecoder.cpp
#    src/VorbisDependencies.c
    src/WavDecoder.cpp
    src/WavEncoder.cpp
    src/WavPackDecoder.cpp
#    src/WavPackDependencies.c
)

include_directories(
  ${CMAKE_SOURCE_DIR}/include/libnyquist
  ${CMAKE_SOURCE_DIR}/third_party
  ${CMAKE_SOURCE_DIR}/third_party/flac
  ${CMAKE_SOURCE_DIR}/third_party/flac/src/include
  ${CMAKE_SOURCE_DIR}/third_party/rtaudio
  third_party/opus/libopus/include
  third_party/wavpack/include
)

add_definitions(-DNDEBUG)

set(BUILD_SHARED_LIBS TRUE)

add_library(nyquist ${SOURCES})
target_link_libraries(nyquist ${LIBMODPLUG_LIBRARIES} ${LIBOPUSFILE_LIBRARIES} ${LIBFLAC_LIBRARIES} ${LIBOPUS_LIBRARIES} ${LIBWAVPACK_LIBRARIES})
