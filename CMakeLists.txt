cmake_minimum_required(VERSION 3.22 FATAL_ERROR)
project(
    cmake-template
    VERSION 0.1.0
    DESCRIPTION "Template for CMake projects."
    LANGUAGES CXX
)

set(CMAKE_CXX_COMPILER clang)
set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED True)

set(CMAKE_EXPORT_COMPILE_COMMANDS ON)
set(CMAKE_VERBOSE_MAKEFILE OFF)

set(CMAKE_BUILD_TYPE "RelWithDebInfo")

set(COMPILE_LIBRARY_FLAGS
    "-stdlib=libc++"
)
set(COMPILE_OPTIMIZATION_FLAGS
    "-fno-omit-frame-pointer"
)
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

foreach(flag
        ${COMPILE_LIBRARY_FLAGS}
        ${COMPILE_OPTIMIZATION_FLAGS}
        ${COMPILE_DIAGNOSTIC_FLAGS})
    add_compile_options(${flag})
endforeach()

set(LINK_LINKER_FLAGS
    "-fuse-ld=lld"
)
set(LINK_LIBRARY_FLAGS
    "-rtlib=compiler-rt"
    "-lc++"
    "-lc++abi"
    "-lm"
    "-lpthread"
)
foreach(flag
        ${LINK_LINKER_FLAGS}
        ${LINK_LIBRARY_FLAGS})
    add_link_options(${flag})
endforeach()

add_subdirectory(src)
