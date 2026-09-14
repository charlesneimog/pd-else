include(FetchContent)

set(FFMPEG_DISABLE_CMAKE_WARNINGS
    ON
    CACHE BOOL "" FORCE)
set(FFMPEG_LICENSE
    LGPLV2_1
    CACHE STRING "" FORCE)

FetchContent_Declare(
    ffmpeg
    GIT_REPOSITORY https://github.com/Pawday/ffmpeg-cmake.git
    GIT_TAG dea60f9dbe2f0052f4f9a6685016da9bc748e85a)

FetchContent_MakeAvailable(ffmpeg)

add_library(ffmpeg_required INTERFACE)
add_library(FFmpeg::required ALIAS ffmpeg_required)
target_link_libraries(
    ffmpeg_required
    INTERFACE ffmpeg.avcodec.static_pic
              ffmpeg.swscale.static_pic
              ffmpeg.avutil.static_pic
              ffmpeg.avcodec.headers
              ffmpeg.swscale.headers
              ffmpeg.avutil.headers
              ${CMAKE_DL_LIBS})
