set(SOURCES
    "Include/Babylon/Dispatchable.h"
    "Include/Babylon/AppRuntime.h"
    "Source/AppRuntime.cpp"
    "Source/AppRuntime_${NAPI_JAVASCRIPT_ENGINE}.cpp"
    "Source/AppRuntime_${BABYLON_NATIVE_PLATFORM}.${BABYLON_NATIVE_PLATFORM_IMPL_EXT}"
    "Source/WorkQueue.cpp"
    "Source/WorkQueue.h")

add_library(AppRuntime ${SOURCES})
warnings_as_errors(AppRuntime)

target_include_directories(AppRuntime
    PRIVATE "Include/Babylon"
    INTERFACE "Include")

if(UNIX AND NOT APPLE AND NOT ANDROID)
    target_include_directories(AppRuntime INTERFACE "/usr/include/webkitgtk-4.0/")
endif()

target_link_to_dependencies(AppRuntime
    PRIVATE arcana
    PUBLIC JsRuntime)

target_compile_definitions(AppRuntime
    PRIVATE NOMINMAX)

set_property(TARGET AppRuntime PROPERTY FOLDER Core)
source_group(TREE ${CMAKE_CURRENT_SOURCE_DIR} FILES ${SOURCES})

