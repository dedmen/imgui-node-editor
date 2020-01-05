project(imgui)

set(_imgui_Sources
    imgui.cpp
    imgui_demo.cpp
    imgui_draw.cpp
    imgui_widgets.cpp
    imconfig.h
    imgui.h
    imgui_internal.h
    imstb_rectpack.h
    imstb_textedit.h
    imstb_truetype.h
)

source_group("" FILES ${_imgui_Sources})

add_library(${PROJECT_NAME} STATIC ${_imgui_Sources})


if(CMAKE_COMPILER_IS_GNUCXX)
    set(CMAKE_CXX_FLAGS "-std=c++1z -O2 -s -fPIC -fpermissive -static-libgcc -static-libstdc++")#-march=i686 -m32
    set(CMAKE_FIND_LIBRARY_SUFFIXES ".a")
    set(CMAKE_SHARED_LINKER_FLAGS "-shared -static-libgcc -static-libstdc++")
else()
    set(CMAKE_CXX_FLAGS_DEBUG "/D_DEBUG /MTd /Zi /Ob0 /Od /RTC1 /MP /EHsc")
    set(CMAKE_CXX_FLAGS_RELEASE "/MT /Zi /O2 /Ob1 /EHsc /MP") #with debug info
    set(CMAKE_SHARED_LINKER_FLAGS_RELEASE "/OPT:REF /DEBUG:FULL") 
endif()

target_include_directories(${PROJECT_NAME} PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})

target_compile_definitions(${PROJECT_NAME} PUBLIC "ImDrawIdx=unsigned int")

set_property(TARGET ${PROJECT_NAME} PROPERTY FOLDER "ThirdParty")
