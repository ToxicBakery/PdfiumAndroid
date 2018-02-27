
cmake_minimum_required(VERSION 3.4.1)

# modft2
add_library(lib_ft2 SHARED IMPORTED)
set_target_properties(lib_ft2 PROPERTIES IMPORTED_LOCATION ${CMAKE_SOURCE_DIR}/lib/${ANDROID_ABI}/libmodft2.so)

# modpng
add_library(lib_png SHARED IMPORTED)
set_target_properties(lib_png PROPERTIES IMPORTED_LOCATION ${CMAKE_SOURCE_DIR}/lib/${ANDROID_ABI}/libmodpng.so)

# modpdfium
add_library(lib_pdfium SHARED IMPORTED)
set_target_properties(lib_pdfium PROPERTIES IMPORTED_LOCATION ${CMAKE_SOURCE_DIR}/lib/${ANDROID_ABI}/libmodpdfium.so)

# jniPdfium
set(CMAKE_CXX_FLAGS "${CMAKE_C_FLAGS} -DHAVE_PTHREADS")
set(CMAKE_CXX_STANDARD 11)
include_directories(include)
add_library(jniPdfium SHARED mainJNILib.cpp)
set_target_properties(jniPdfium PROPERTIES LINKER_LANGUAGE CXX)
target_include_directories(jniPdfium PRIVATE include/fpdf)
target_link_libraries(jniPdfium android log jnigraphics lib_ft2 lib_png lib_pdfium)
