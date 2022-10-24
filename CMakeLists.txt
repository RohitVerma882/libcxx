cmake_minimum_required(VERSION 3.13.4)
project(libcxx)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++20 -fvisibility-global-new-delete-hidden -fvisibility=hidden -fvisibility-inlines-hidden -Wno-macro-redefined -Wno-unknown-attributes -ffunction-sections -fdata-sections")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -DLIBCXX_BUILDING_LIBCXXABI -D_LIBCPP_NO_EXCEPTIONS -D_LIBCPP_NO_RTTI -D_LIBCPP_BUILDING_LIBRARY -D_LIBCPP_DISABLE_VISIBILITY_ANNOTATIONS -D__STDC_FORMAT_MACROS -D_LIBCXXABI_NO_EXCEPTIONS -DHAS_THREAD_LOCAL")

#
# cxx
#
set(LIBCXX_SOURCES
    src/algorithm.cpp
    src/any.cpp
    src/atomic.cpp
    src/barrier.cpp
    src/bind.cpp
    src/charconv.cpp
    src/chrono.cpp
    src/condition_variable.cpp
    src/condition_variable_destructor.cpp
    src/debug.cpp
    src/exception.cpp
    src/filesystem/directory_iterator.cpp
    src/filesystem/int128_builtins.cpp
    src/filesystem/operations.cpp
    src/functional.cpp
    src/future.cpp
    src/hash.cpp
    src/ios.cpp
    src/iostream.cpp
    src/locale.cpp
    src/memory.cpp
    src/mutex.cpp
    src/mutex_destructor.cpp
    src/new.cpp
    src/optional.cpp
    src/random.cpp
    src/regex.cpp
    src/shared_mutex.cpp
    src/stdexcept.cpp
    src/string.cpp
    src/strstream.cpp
    src/system_error.cpp
    src/thread.cpp
    src/typeinfo.cpp
    src/utility.cpp
    src/valarray.cpp
    src/variant.cpp
    src/vector.cpp)

set(LIBCXXABI_SOURCES
    src/abi/abort_message.cpp
    src/abi/cxa_aux_runtime.cpp
    src/abi/cxa_default_handlers.cpp
    src/abi/cxa_exception_storage.cpp
    src/abi/cxa_guard.cpp
    src/abi/cxa_handlers.cpp
    src/abi/cxa_noexception.cpp
    src/abi/cxa_thread_atexit.cpp
    src/abi/cxa_unexpected.cpp
    src/abi/cxa_vector.cpp
    src/abi/cxa_virtual.cpp
    src/abi/stdlib_exception.cpp
    src/abi/stdlib_new_delete.cpp
    src/abi/stdlib_stdexcept.cpp
    src/abi/stdlib_typeinfo.cpp)
    
add_library(cxx STATIC ${LIBCXX_SOURCES} ${LIBCXXABI_SOURCES})

target_include_directories(cxx PUBLIC
    $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
    $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include/abi>)
    
add_library(libcxx::cxx ALIAS cxx)