# The Flutter tooling requires that developers have CMake 3.10 or later
# installed. You should not increase this version, as doing so will cause
# the plugin to fail to compile for some customers of the plugin.
cmake_minimum_required(VERSION 3.10)

# Project-level configuration.
set(PROJECT_NAME "record_linux")
project(${PROJECT_NAME} LANGUAGES CXX)

# This value is used when generating builds using this plugin, so it must
# not be changed.
set(PLUGIN_NAME "record_linux_plugin")

# Define the plugin library target. Its name must not be changed (see comment
# on PLUGIN_NAME above).
#
# Any new source files that you add to the plugin should be added here.
add_library(${PLUGIN_NAME} SHARED
  "record_linux_plugin.cc"
)

# Apply a standard set of build settings that are configured in the
# application-level CMakeLists.txt. This can be removed for plugins that want
# full control over build settings.
apply_standard_settings(${PLUGIN_NAME})

# Symbols are hidden by default to reduce the chance of accidental conflicts
# between plugins. This should not be removed; any symbols that should be
# exported should be explicitly exported with the FLUTTER_PLUGIN_EXPORT macro.
set_target_properties(${PLUGIN_NAME} PROPERTIES
  CXX_VISIBILITY_PRESET hidden)
target_compile_definitions(${PLUGIN_NAME} PRIVATE FLUTTER_PLUGIN_IMPL)

# Source include directories and library dependencies. Add any plugin-specific
# dependencies here.
target_include_directories(${PLUGIN_NAME} INTERFACE
  "${CMAKE_CURRENT_SOURCE_DIR}/include")
target_link_libraries(${PLUGIN_NAME} PRIVATE flutter)
target_link_libraries(${PLUGIN_NAME} PRIVATE PkgConfig::GTK)

# List of absolute paths to libraries that should be bundled with the plugin.
# This list could contain prebuilt libraries, or libraries created by an
# external build triggered from this build file.
set(record_linux_bundled_libraries
  ""
  "${CMAKE_CURRENT_SOURCE_DIR}/fmedia/fmedia"
  "${CMAKE_CURRENT_SOURCE_DIR}/fmedia/fmedia.conf"
  "${CMAKE_CURRENT_SOURCE_DIR}/fmedia/mod/aac.so"
  "${CMAKE_CURRENT_SOURCE_DIR}/fmedia/mod/afilter.so"
  "${CMAKE_CURRENT_SOURCE_DIR}/fmedia/mod/alac.so"
  "${CMAKE_CURRENT_SOURCE_DIR}/fmedia/mod/ape.so"
  "${CMAKE_CURRENT_SOURCE_DIR}/fmedia/mod/core.so"
  "${CMAKE_CURRENT_SOURCE_DIR}/fmedia/mod/direct-sound.so"
  "${CMAKE_CURRENT_SOURCE_DIR}/fmedia/mod/dynanorm.so"
  "${CMAKE_CURRENT_SOURCE_DIR}/fmedia/mod/flac.so"
  "${CMAKE_CURRENT_SOURCE_DIR}/fmedia/mod/fmt.so"
  "${CMAKE_CURRENT_SOURCE_DIR}/fmedia/mod/libALAC-ff.so"
  "${CMAKE_CURRENT_SOURCE_DIR}/fmedia/mod/libDynamicAudioNormalizer-ff.so"
  "${CMAKE_CURRENT_SOURCE_DIR}/fmedia/mod/libfdk-aac-ff.so"
  "${CMAKE_CURRENT_SOURCE_DIR}/fmedia/mod/libFLAC-ff.so"
  "${CMAKE_CURRENT_SOURCE_DIR}/fmedia/mod/libMAC-ff.so"
  "${CMAKE_CURRENT_SOURCE_DIR}/fmedia/mod/libmp3lame-ff.so"
  "${CMAKE_CURRENT_SOURCE_DIR}/fmedia/mod/libmpc-ff.so"
  "${CMAKE_CURRENT_SOURCE_DIR}/fmedia/mod/libmpg123-ff.so"
  "${CMAKE_CURRENT_SOURCE_DIR}/fmedia/mod/libogg-ff.so"
  "${CMAKE_CURRENT_SOURCE_DIR}/fmedia/mod/libopus-ff.so"
  "${CMAKE_CURRENT_SOURCE_DIR}/fmedia/mod/libsoxr-ff.so"
  "${CMAKE_CURRENT_SOURCE_DIR}/fmedia/mod/libvorbis-ff.so"
  "${CMAKE_CURRENT_SOURCE_DIR}/fmedia/mod/libvorbisenc-ff.so"
  "${CMAKE_CURRENT_SOURCE_DIR}/fmedia/mod/libwavpack-ff.so"
  "${CMAKE_CURRENT_SOURCE_DIR}/fmedia/mod/mpc.so"
  "${CMAKE_CURRENT_SOURCE_DIR}/fmedia/mod/mpeg.so"
  "${CMAKE_CURRENT_SOURCE_DIR}/fmedia/mod/net.so"
  "${CMAKE_CURRENT_SOURCE_DIR}/fmedia/mod/opus.so"
  "${CMAKE_CURRENT_SOURCE_DIR}/fmedia/mod/plist.so"
  "${CMAKE_CURRENT_SOURCE_DIR}/fmedia/mod/soxr.so"
  "${CMAKE_CURRENT_SOURCE_DIR}/fmedia/mod/tui.so"
  "${CMAKE_CURRENT_SOURCE_DIR}/fmedia/mod/vorbis.so"
  "${CMAKE_CURRENT_SOURCE_DIR}/fmedia/mod/wasapi.so"
  "${CMAKE_CURRENT_SOURCE_DIR}/fmedia/mod/wavpack.so"
  PARENT_SCOPE
)
