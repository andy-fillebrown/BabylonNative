set(SOURCES
    "Include/Shared/Babylon/Plugins/ExternalTexture.h"
    "Source/ExternalTexture_${GRAPHICS_API}.cpp"
    "Source/ExternalTexture.cpp")

add_library(ExternalTexture ${SOURCES})
warnings_as_errors(ExternalTexture)

target_include_directories(ExternalTexture
    PUBLIC "Include/Shared"
    PRIVATE "Source")

target_link_to_dependencies(ExternalTexture
    PRIVATE napi_extensions
    PUBLIC JsRuntime
    PUBLIC GraphicsDevice
    PRIVATE JsRuntimeInternal
    PRIVATE GraphicsDeviceContext
    PRIVATE Graphics
    PRIVATE bgfx
    PRIVATE bimg
    PRIVATE bx)

target_compile_definitions(ExternalTexture
    PRIVATE NOMINMAX
    PRIVATE ${GRAPHICS_API_UPPER})

set_property(TARGET ExternalTexture PROPERTY FOLDER Plugins)
source_group(TREE ${CMAKE_CURRENT_SOURCE_DIR} FILES ${SOURCES})