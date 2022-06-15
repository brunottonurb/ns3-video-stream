set(source_files
    helper/video-stream-helper.cc
    model/video-stream-client.cc
    model/video-stream-server.cc
)

set(header_files
    helper/video-stream-helper.h
    model/video-stream-client.h
    model/video-stream-server.h
)

build_lib(
    LIBNAME video-stream
    SOURCE_FILES ${source_files}
    HEADER_FILES ${header_files}
    LIBRARIES_TO_LINK
        ${libinternet-apps}
)