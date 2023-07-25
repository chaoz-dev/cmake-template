cmake_minimum_required(VERSION 3.25 FATAL_ERROR)
set(CMAKE_CXX_COMPILER clang)

project(
    cmake-template
    VERSION 0.2.0
    DESCRIPTION "Template for CMake projects."
    LANGUAGES CXX
)

# cc configurations.
set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED True)
set(CMAKE_BUILD_TYPE "RelWithDebInfo")
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

# cc compiler flags.
set(CC_LIBRARY_FLAGS "-stdlib=libc++")
set(CC_OPTIMIZATION_FLAGS "-fno-omit-frame-pointer")
# Suppress warnings when building external dependencies.
set(CC_EXTERNAL_DIAGNOSTIC_FLAGS "-w")
foreach(flag
        ${CC_LIBRARY_FLAGS}
        ${CC_OPTIMIZATION_FLAGS}
        ${CC_EXTERNAL_DIAGNOSTIC_FLAGS})
    add_compile_options(${flag})
endforeach()

# cc linker flags.
set(LD_LINKER_FLAGS "-fuse-ld=lld")
set(LD_LIBRARY_FLAGS
    "-rtlib=compiler-rt"
    "-lc++"
    "-lc++abi"
    "-lm"
    "-lpthread"
)
foreach(flag
        ${LD_LINKER_FLAGS}
        ${LD_LIBRARY_FLAGS})
    add_link_options(${flag})
endforeach()

# Find dependencies.
find_package(Threads)

include(FetchContent)

FetchContent_Declare(
    gtest
    GIT_REPOSITORY  https://github.com/google/googletest.git
    GIT_TAG         v1.13.0
    OVERRIDE_FIND_PACKAGE
)

FetchContent_Declare(
    glog
    GIT_REPOSITORY  https://github.com/google/glog.git
    GIT_TAG         v0.6.0
    OVERRIDE_FIND_PACKAGE
)

FetchContent_MakeAvailable(
    glog
    gtest
)

# cc compiler flags.
# These are the diagnostic flags that the project uses.
set(COMPILE_DIAGNOSTIC_FLAGS
    # General warnings and errors.
    "-Wall"
    "-Wconversion"
    "-Wdeprecated"
    "-Werror"
    "-Wextra"
    "-Wformat"
    "-Wmost"
    "-Wpedantic"
    "-Wthread-safety"
    "-Wunreachable-code-aggressive"
    "-Wunused"

    # Specific warnings and errors.
    "-Wabstract-vbase-init"
    "-Walloca"
    "-Warray-bounds-pointer-arithmetic"
    "-Wassign-enum"
    "-Watomic-properties"
    "-Watomic-implicit-seq-cst"
    "-Wbad-function-cast"
    "-Wcast-function-type"
    "-Wcast-qual"
    "-Wconditional-uninitialized"
    "-Wctad-maybe-unsupported"
    "-Wdeprecated-implementations"
    "-Wdouble-promotion"
    "-Wduplicate-enum"
    "-Wduplicate-method-arg"
    "-Wduplicate-method-match"
    "-Wfloat-equal"
    "-Wheader-hygiene"
    "-Widiomatic-parentheses"
    "-Winconsistent-missing-destructor-override"
    "-Wloop-analysis"
    "-Wmethod-signatures"
    "-Wnon-virtual-dtor"
    "-Wnullable-to-nonnull-conversion"
    "-Wold-style-cast"
    "-Woverriding-method-mismatch"
    "-Wpacked"
    "-Wpointer-arith"
    "-Wquoted-include-in-framework-header"
    "-Wredundant-parens"
    "-Wreserved-identifier"
    "-Wshift-sign-overflow"
    "-Wsuggest-destructor-override"
    "-Wsuggest-override"
    "-Wsuper-class-method-mismatch"
    "-Wswitch-enum"
    "-Wundefined-func-template"
    "-Wundefined-reinterpret-cast"
    "-Wvector-conversion"
)
add_compile_options(${COMPILE_DIAGNOSTIC_FLAGS})

enable_testing()
