macro(simd_fail message)
  if(REQUIRE_SIMD)
    message(FATAL_ERROR "${message}.")
  else()
    message(WARNING "${message}.  Performance will suffer.")
    set(WITH_SIMD 0 PARENT_SCOPE)
  endif()
endmacro()

###############################################################################
# Fat Xcode binaries (MB patch)
###############################################################################

if( CMAKE_GENERATOR STREQUAL "Xcode" )

option( MB_XCODE_USE_INTEL_SIMD "Allow using SIMD on Intel CPUs under Xcode generator (requires NASM)" ON )

if ( MB_XCODE_USE_INTEL_SIMD )
    set( intel_x64_asm_sources
        ${CMAKE_CURRENT_LIST_DIR}/x86_64/jsimdcpu.asm
        ${CMAKE_CURRENT_LIST_DIR}/x86_64/jfdctflt-sse.asm
        ${CMAKE_CURRENT_LIST_DIR}/x86_64/jccolor-sse2.asm
        ${CMAKE_CURRENT_LIST_DIR}/x86_64/jcgray-sse2.asm
        ${CMAKE_CURRENT_LIST_DIR}/x86_64/jchuff-sse2.asm
        ${CMAKE_CURRENT_LIST_DIR}/x86_64/jcphuff-sse2.asm
        ${CMAKE_CURRENT_LIST_DIR}/x86_64/jcsample-sse2.asm
        ${CMAKE_CURRENT_LIST_DIR}/x86_64/jdcolor-sse2.asm
        ${CMAKE_CURRENT_LIST_DIR}/x86_64/jdmerge-sse2.asm
        ${CMAKE_CURRENT_LIST_DIR}/x86_64/jdsample-sse2.asm
        ${CMAKE_CURRENT_LIST_DIR}/x86_64/jfdctfst-sse2.asm
        ${CMAKE_CURRENT_LIST_DIR}/x86_64/jfdctint-sse2.asm
        ${CMAKE_CURRENT_LIST_DIR}/x86_64/jidctflt-sse2.asm
        ${CMAKE_CURRENT_LIST_DIR}/x86_64/jidctfst-sse2.asm
        ${CMAKE_CURRENT_LIST_DIR}/x86_64/jidctint-sse2.asm
        ${CMAKE_CURRENT_LIST_DIR}/x86_64/jidctred-sse2.asm
        ${CMAKE_CURRENT_LIST_DIR}/x86_64/jquantf-sse2.asm
        ${CMAKE_CURRENT_LIST_DIR}/x86_64/jquanti-sse2.asm
        ${CMAKE_CURRENT_LIST_DIR}/x86_64/jccolor-avx2.asm
        ${CMAKE_CURRENT_LIST_DIR}/x86_64/jcgray-avx2.asm
        ${CMAKE_CURRENT_LIST_DIR}/x86_64/jcsample-avx2.asm
        ${CMAKE_CURRENT_LIST_DIR}/x86_64/jdcolor-avx2.asm
        ${CMAKE_CURRENT_LIST_DIR}/x86_64/jdmerge-avx2.asm
        ${CMAKE_CURRENT_LIST_DIR}/x86_64/jdsample-avx2.asm
        ${CMAKE_CURRENT_LIST_DIR}/x86_64/jfdctint-avx2.asm
        ${CMAKE_CURRENT_LIST_DIR}/x86_64/jidctint-avx2.asm
        ${CMAKE_CURRENT_LIST_DIR}/x86_64/jquanti-avx2.asm
    )
    set( intel_x86_asm_sources
        ${CMAKE_CURRENT_LIST_DIR}/i386/jsimdcpu.asm
        ${CMAKE_CURRENT_LIST_DIR}/i386/jfdctflt-3dn.asm
        ${CMAKE_CURRENT_LIST_DIR}/i386/jidctflt-3dn.asm
        ${CMAKE_CURRENT_LIST_DIR}/i386/jquant-3dn.asm
        ${CMAKE_CURRENT_LIST_DIR}/i386/jccolor-mmx.asm
        ${CMAKE_CURRENT_LIST_DIR}/i386/jcgray-mmx.asm
        ${CMAKE_CURRENT_LIST_DIR}/i386/jcsample-mmx.asm
        ${CMAKE_CURRENT_LIST_DIR}/i386/jdcolor-mmx.asm
        ${CMAKE_CURRENT_LIST_DIR}/i386/jdmerge-mmx.asm
        ${CMAKE_CURRENT_LIST_DIR}/i386/jdsample-mmx.asm
        ${CMAKE_CURRENT_LIST_DIR}/i386/jfdctfst-mmx.asm
        ${CMAKE_CURRENT_LIST_DIR}/i386/jfdctint-mmx.asm
        ${CMAKE_CURRENT_LIST_DIR}/i386/jidctfst-mmx.asm
        ${CMAKE_CURRENT_LIST_DIR}/i386/jidctint-mmx.asm
        ${CMAKE_CURRENT_LIST_DIR}/i386/jidctred-mmx.asm
        ${CMAKE_CURRENT_LIST_DIR}/i386/jquant-mmx.asm
        ${CMAKE_CURRENT_LIST_DIR}/i386/jfdctflt-sse.asm
        ${CMAKE_CURRENT_LIST_DIR}/i386/jidctflt-sse.asm
        ${CMAKE_CURRENT_LIST_DIR}/i386/jquant-sse.asm
        ${CMAKE_CURRENT_LIST_DIR}/i386/jccolor-sse2.asm
        ${CMAKE_CURRENT_LIST_DIR}/i386/jcgray-sse2.asm
        ${CMAKE_CURRENT_LIST_DIR}/i386/jchuff-sse2.asm
        ${CMAKE_CURRENT_LIST_DIR}/i386/jcphuff-sse2.asm
        ${CMAKE_CURRENT_LIST_DIR}/i386/jcsample-sse2.asm
        ${CMAKE_CURRENT_LIST_DIR}/i386/jdcolor-sse2.asm
        ${CMAKE_CURRENT_LIST_DIR}/i386/jdmerge-sse2.asm
        ${CMAKE_CURRENT_LIST_DIR}/i386/jdsample-sse2.asm
        ${CMAKE_CURRENT_LIST_DIR}/i386/jfdctfst-sse2.asm
        ${CMAKE_CURRENT_LIST_DIR}/i386/jfdctint-sse2.asm
        ${CMAKE_CURRENT_LIST_DIR}/i386/jidctflt-sse2.asm
        ${CMAKE_CURRENT_LIST_DIR}/i386/jidctfst-sse2.asm
        ${CMAKE_CURRENT_LIST_DIR}/i386/jidctint-sse2.asm
        ${CMAKE_CURRENT_LIST_DIR}/i386/jidctred-sse2.asm
        ${CMAKE_CURRENT_LIST_DIR}/i386/jquantf-sse2.asm
        ${CMAKE_CURRENT_LIST_DIR}/i386/jquanti-sse2.asm
        ${CMAKE_CURRENT_LIST_DIR}/i386/jccolor-avx2.asm
        ${CMAKE_CURRENT_LIST_DIR}/i386/jcgray-avx2.asm
        ${CMAKE_CURRENT_LIST_DIR}/i386/jcsample-avx2.asm
        ${CMAKE_CURRENT_LIST_DIR}/i386/jdcolor-avx2.asm
        ${CMAKE_CURRENT_LIST_DIR}/i386/jdmerge-avx2.asm
        ${CMAKE_CURRENT_LIST_DIR}/i386/jdsample-avx2.asm
        ${CMAKE_CURRENT_LIST_DIR}/i386/jfdctint-avx2.asm
        ${CMAKE_CURRENT_LIST_DIR}/i386/jidctint-avx2.asm
        ${CMAKE_CURRENT_LIST_DIR}/i386/jquanti-avx2.asm
    )

    enable_language( ASM_NASM )
    message(STATUS "CMAKE_ASM_NASM_COMPILER = ${CMAKE_ASM_NASM_COMPILER}")

    function( create_simd_objects libsimd cpu_type sources )
        set( libsimd_output "${CMAKE_CURRENT_BINARY_DIR}/${cpu_type}/libsimdobjects.a" )
        set( ${libsimd} ${libsimd_output} PARENT_SCOPE )

        set( OBJDIR "${CMAKE_CURRENT_BINARY_DIR}/${cpu_type}/objs" )
        file( WRITE ${CMAKE_CURRENT_BINARY_DIR}/empty.c )
        if ( cpu_type STREQUAL "x86_64" )
            set( cpu_define "__x86_64__" )
            set( format     "macho64"    )
        else()
            set( cpu_define "__i386__" )
            set( format     "macho"    )
        endif()
        set( CMAKE_ASM_NASM_FLAGS ${CMAKE_ASM_NASM_FLAGS} -DMACHO -D${cpu_define} -DPIC -I\"${CMAKE_CURRENT_SOURCE_DIR}/nasm/\" -I\"${CMAKE_CURRENT_SOURCE_DIR}/${cpu_type}/\" -g )
        file( MAKE_DIRECTORY ${OBJDIR} )
        # Xcode 10 and newer no longer ship with nasm and even if it's manually added, the invocation is wrong
        foreach( file ${sources} )
            set( OBJECT_DEPENDS "" )
            if( ${file} MATCHES jccolor )
                string(REGEX REPLACE "jccolor" "jccolext" DEPFILE ${file})
                set(OBJECT_DEPENDS ${OBJECT_DEPENDS}
                    ${CMAKE_CURRENT_SOURCE_DIR}/${DEPFILE})
            endif()
            if(${file} MATCHES jcgray)
                string(REGEX REPLACE "jcgray" "jcgryext" DEPFILE ${file})
                set(OBJECT_DEPENDS ${OBJECT_DEPENDS}
                    ${CMAKE_CURRENT_SOURCE_DIR}/${DEPFILE})
            endif()
            if(${file} MATCHES jdcolor)
                string(REGEX REPLACE "jdcolor" "jdcolext" DEPFILE ${file})
                set(OBJECT_DEPENDS ${OBJECT_DEPENDS}
                    ${CMAKE_CURRENT_SOURCE_DIR}/${DEPFILE})
            endif()
            if(${file} MATCHES jdmerge)
                string(REGEX REPLACE "jdmerge" "jdmrgext" DEPFILE ${file})
                set(OBJECT_DEPENDS ${OBJECT_DEPENDS}
                    ${CMAKE_CURRENT_SOURCE_DIR}/${DEPFILE})
            endif()
            set(OBJECT_DEPENDS ${OBJECT_DEPENDS} ${INC_FILES})

            get_filename_component( filename ${file} NAME )
            set(SIMD_OBJ ${OBJDIR}/${filename}${CMAKE_C_OUTPUT_EXTENSION})
            add_custom_command(
                OUTPUT
                    ${SIMD_OBJ}
                DEPENDS
                    ${file} ${OBJECT_DEPENDS}
                COMMAND
                    ${CMAKE_ASM_NASM_COMPILER} -f${format} ${CMAKE_ASM_NASM_FLAGS} ${file} -o${SIMD_OBJ}
            )
            set( SIMD_OBJS ${SIMD_OBJS} ${SIMD_OBJ} )
        endforeach()
        add_custom_command(
            OUTPUT
                ${libsimd_output}
            DEPENDS
                ${SIMD_OBJS}
            COMMAND
                libtool -static -arch_only ${cpu_type} ${SIMD_OBJS} -o ${libsimd_output}
        )
        set( ${simd_objs} ${SIMD_OBJS} PARENT_SCOPE )
    endfunction()

    # Intel x64 is required for MacOS, iOS simulator
    # For Mac Catalyst use the C fallback implementation as object files produced by NASM cannot be linked
    # into a Mac Catalyst binary (link error: "building for Mac Catalyst, but linking in object file built for ,")
    set( need_x64 OFF )
    if ( NOT DEFINED MB_IOS_SDK OR MB_IOS_SDK STREQUAL "simulator" )
        unset( intel_x64_objs )
        create_simd_objects( intel_x64_objs x86_64 "${intel_x64_asm_sources}" )

        add_custom_target( Intel64Assemble DEPENDS ${intel_x64_objs} )
        set( need_x64 ON )
    endif()

    # Intel i386 is required only for iOS simulator
    set( need_x86 OFF )
    if ( MB_IOS_SDK STREQUAL "simulator" )
        unset( intel_x86_objs )
        create_simd_objects( intel_x86_objs i386 "${intel_x86_asm_sources}" )

        add_custom_target( Intel32Assemble DEPENDS ${intel_x86_objs} )
        set( need_x86 ON )
    endif()
endif( MB_XCODE_USE_INTEL_SIMD )

# Arm7 sources need to be compiled with gas-preprocessor.pl (unlike arm64 sources, which can be compiled with xcode)
set( need_arm7 OFF )
if ( MB_IOS_SDK STREQUAL "device" )
    set( arm_asm_source   arm/jsimd_neon.S )

    set( gas_preprocessor ${CMAKE_CURRENT_LIST_DIR}/gas-preprocessor.pl )
    enable_language( ASM )

    set( OBJDIR "${CMAKE_CURRENT_BINARY_DIR}/arm/objs" )
    file( MAKE_DIRECTORY ${OBJDIR} )
    set( libsimd_arm_output "${CMAKE_CURRENT_BINARY_DIR}/arm/libsimdobjects.a" )

    separate_arguments( CMAKE_ASM_FLAGS_SEP UNIX_COMMAND "${CMAKE_ASM_FLAGS}" )

    add_custom_command(
        OUTPUT
            ${libsimd_arm_output}
        DEPENDS
            ${arm_asm_source}
        COMMAND
            ${gas_preprocessor} ${CMAKE_ASM_COMPILER} ${CMAKE_ASM_FLAGS_SEP} -arch armv7 -fembed-bitcode -x assembler-with-cpp -c ${CMAKE_CURRENT_LIST_DIR}/${arm_asm_source} -o ${OBJDIR}/jsimd_neon.S.o
        COMMAND
            libtool -static -arch_only armv7 ${OBJDIR}/jsimd_neon.S.o -o ${libsimd_arm_output}
    )

    add_custom_target( Armv7Assemble DEPENDS ${libsimd_arm_output} )
    set( need_arm7 ON )
endif()

# Now create fat binary out of SIMD objects
set( need_simd_objects_lib OFF )
unset( lipo_flags )
unset( lipo_deps  )

if ( need_x86 )
    set( need_simd_objects_lib ON )
    set( intel_x86_sources i386/jsimd.c )
    list( APPEND lipo_flags -arch i386 ${intel_x86_objs} )
    list( APPEND lipo_deps Intel32Assemble )
endif()

if ( need_x64 )
    set( need_simd_objects_lib ON )
    set( intel_x64_sources x86_64/jsimd.c )
    list( APPEND lipo_flags -arch x86_64 ${intel_x64_objs} )
    list( APPEND lipo_deps Intel64Assemble )
endif()

if ( MB_IOS_SDK STREQUAL "maccatalyst" )
    # need Intel, but use C implementation
    set( intel_x64_sources ../jsimd_none.c )
endif()

if ( need_arm7 )
    set( need_simd_objects_lib ON )
    set( arm_sources arm/jsimd.c )
    list( APPEND lipo_flags -arch armv7 ${libsimd_arm_output} )
    list( APPEND lipo_deps Armv7Assemble )
endif()

if ( need_simd_objects_lib )
    if ( CMAKE_ARCHIVE_OUTPUT_DIRECTORY )
        set( simd_objs_lib ${CMAKE_ARCHIVE_OUTPUT_DIRECTORY}/$CONFIGURATION/libsimdobjects.a )
    else()
        set( simd_objs_lib ${CMAKE_BINARY_DIR}/$CONFIGURATION/libsimdobjects.a )
    endif()
    add_custom_command(
        OUTPUT
            ${simd_objs_lib}
        DEPENDS
            ${lipo_deps}
        COMMAND
            lipo -create ${lipo_flags} -output ${simd_objs_lib}
    )
    add_custom_target( FatAssemblyLibs DEPENDS ${simd_objs_lib} )
endif()

set( arm64_asm_sources arm64/jsimd_neon.S )

set( arm64_sources ${arm64_asm_sources} arm64/jsimd.c )

set_source_files_properties( ${arm64_asm_sources}
    PROPERTIES
        XCODE_EXPLICIT_FILE_TYPE sourcecode.asm
        LANGUAGE                 ASM
)

if ( NOT MB_XCODE_USE_INTEL_SIMD )
    # use C implementation for Intel
    set( intel_generic_sources ../jsimd_none.c )
endif()

add_library( simd STATIC ${arm64_sources} ${arm_sources} ${intel_x64_sources} ${intel_x86_sources} ${intel_generic_sources} )

if ( need_simd_objects_lib )
    add_dependencies( simd FatAssemblyLibs )
    target_link_libraries( simd PUBLIC ${simd_objs_lib} )
endif()

string( REPLACE ";" " " ARM64_SRCS   "${arm64_sources}"     )
string( REPLACE ";" " " ARM_SRCS     "${arm_sources}"       )
string( REPLACE ";" " " INTEL64_SRCS "${intel_x64_sources}" )
string( REPLACE ";" " " INTEL32_SRCS "${intel_x86_sources}" )

set_target_properties( simd PROPERTIES
    XCODE_ATTRIBUTE_EXCLUDED_SOURCE_FILE_NAMES[arch=x86_64] "${ARM64_SRCS} ${ARM_SRCS} ${INTEL32_SRCS}"
    XCODE_ATTRIBUTE_EXCLUDED_SOURCE_FILE_NAMES[arch=i386]   "${ARM64_SRCS} ${ARM_SRCS} ${INTEL64_SRCS}"
    XCODE_ATTRIBUTE_EXCLUDED_SOURCE_FILE_NAMES[arch=armv7]  "${INTEL64_SRCS} ${INTEL32_SRCS} ${intel_generic_sources} ${ARM64_SRCS}"
    XCODE_ATTRIBUTE_EXCLUDED_SOURCE_FILE_NAMES[arch=armv7s] "${INTEL64_SRCS} ${INTEL32_SRCS} ${intel_generic_sources} ${ARM64_SRCS}"
    XCODE_ATTRIBUTE_EXCLUDED_SOURCE_FILE_NAMES[arch=arm64]  "${INTEL64_SRCS} ${INTEL32_SRCS} ${intel_generic_sources} ${ARM_SRCS}"
)

if( CMAKE_POSITION_INDEPENDENT_CODE OR ENABLE_SHARED )
  set_target_properties( simd PROPERTIES POSITION_INDEPENDENT_CODE 1 )
endif()

# MB patch end

###############################################################################
# x86[-64] (NASM)
###############################################################################

elseif(CPU_TYPE STREQUAL "x86_64" OR CPU_TYPE STREQUAL "i386")

set(CMAKE_ASM_NASM_FLAGS_DEBUG_INIT "-g")
set(CMAKE_ASM_NASM_FLAGS_RELWITHDEBINFO_INIT "-g")

# Allow the location of the NASM executable to be specified using the ASM_NASM
# environment variable.  This should happen automatically, but unfortunately
# enable_language(ASM_NASM) doesn't parse the ASM_NASM environment variable
# until after CMAKE_ASM_NASM_COMPILER has been populated with the results of
# searching for NASM or YASM in the PATH.
if(NOT DEFINED CMAKE_ASM_NASM_COMPILER AND DEFINED ENV{ASM_NASM})
  set(CMAKE_ASM_NASM_COMPILER $ENV{ASM_NASM})
endif()

if(CPU_TYPE STREQUAL "x86_64")
  if(CYGWIN)
    set(CMAKE_ASM_NASM_OBJECT_FORMAT win64)
  endif()
elseif(CPU_TYPE STREQUAL "i386")
  if(BORLAND)
    set(CMAKE_ASM_NASM_OBJECT_FORMAT obj)
  elseif(CYGWIN)
    set(CMAKE_ASM_NASM_OBJECT_FORMAT win32)
  endif()
endif()

if(NOT REQUIRE_SIMD)
  include(CheckLanguage)
  check_language(ASM_NASM)
  if(NOT CMAKE_ASM_NASM_COMPILER)
    simd_fail("SIMD extensions disabled: could not find NASM compiler")
    return()
  endif()
endif()
enable_language(ASM_NASM)
message(STATUS "CMAKE_ASM_NASM_COMPILER = ${CMAKE_ASM_NASM_COMPILER}")

if(CMAKE_ASM_NASM_OBJECT_FORMAT MATCHES "macho*")
  set(CMAKE_ASM_NASM_FLAGS "${CMAKE_ASM_NASM_FLAGS} -DMACHO")
elseif(CMAKE_ASM_NASM_OBJECT_FORMAT MATCHES "elf*")
  set(CMAKE_ASM_NASM_FLAGS "${CMAKE_ASM_NASM_FLAGS} -DELF")
  set(CMAKE_ASM_NASM_DEBUG_FORMAT "dwarf2")
endif()
if(CPU_TYPE STREQUAL "x86_64")
  if(WIN32 OR CYGWIN)
    set(CMAKE_ASM_NASM_FLAGS "${CMAKE_ASM_NASM_FLAGS} -DWIN64")
  endif()
  set(CMAKE_ASM_NASM_FLAGS "${CMAKE_ASM_NASM_FLAGS} -D__x86_64__")
elseif(CPU_TYPE STREQUAL "i386")
  if(BORLAND)
    set(CMAKE_ASM_NASM_FLAGS "${CMAKE_ASM_NASM_FLAGS} -DOBJ32")
  elseif(WIN32 OR CYGWIN)
    set(CMAKE_ASM_NASM_FLAGS "${CMAKE_ASM_NASM_FLAGS} -DWIN32")
  endif()
endif()

message(STATUS "CMAKE_ASM_NASM_OBJECT_FORMAT = ${CMAKE_ASM_NASM_OBJECT_FORMAT}")

if(NOT CMAKE_ASM_NASM_OBJECT_FORMAT)
  simd_fail("SIMD extensions disabled: could not determine NASM object format")
  return()
endif()

get_filename_component(CMAKE_ASM_NASM_COMPILER_TYPE
  "${CMAKE_ASM_NASM_COMPILER}" NAME_WE)
if(CMAKE_ASM_NASM_COMPILER_TYPE MATCHES "yasm")
  foreach(var CMAKE_ASM_NASM_FLAGS_DEBUG CMAKE_ASM_NASM_FLAGS_RELWITHDEBINFO)
    if(${var} STREQUAL "-g")
      if(CMAKE_ASM_NASM_DEBUG_FORMAT)
        set_property(CACHE ${var} PROPERTY VALUE "-g ${CMAKE_ASM_NASM_DEBUG_FORMAT}")
      else()
        set_property(CACHE ${var} PROPERTY VALUE "")
      endif()
    endif()
  endforeach()
endif()

if(NOT WIN32 AND (CMAKE_POSITION_INDEPENDENT_CODE OR ENABLE_SHARED))
  set(CMAKE_ASM_NASM_FLAGS "${CMAKE_ASM_NASM_FLAGS} -DPIC")
endif()

string(TOUPPER ${CMAKE_BUILD_TYPE} CMAKE_BUILD_TYPE_UC)
set(EFFECTIVE_ASM_NASM_FLAGS "${CMAKE_ASM_NASM_FLAGS} ${CMAKE_ASM_NASM_FLAGS_${CMAKE_BUILD_TYPE_UC}}")
message(STATUS "CMAKE_ASM_NASM_FLAGS = ${EFFECTIVE_ASM_NASM_FLAGS}")

set(CMAKE_ASM_NASM_FLAGS "${CMAKE_ASM_NASM_FLAGS} -I\"${CMAKE_CURRENT_SOURCE_DIR}/nasm/\" -I\"${CMAKE_CURRENT_SOURCE_DIR}/${CPU_TYPE}/\"")

set(GREP grep)
if(CMAKE_SYSTEM_NAME STREQUAL "SunOS")
  set(GREP ggrep)
endif()
add_custom_target(jsimdcfg COMMAND
  ${CMAKE_C_COMPILER} -E -I${CMAKE_BINARY_DIR} -I${CMAKE_CURRENT_BINARY_DIR}
    -I${CMAKE_CURRENT_SOURCE_DIR}
    ${CMAKE_CURRENT_SOURCE_DIR}/nasm/jsimdcfg.inc.h |
  ${GREP} -E '^[\;%]|^\ %' | sed 's%_cpp_protection_%%' |
  sed 's@% define@%define@g' >${CMAKE_CURRENT_SOURCE_DIR}/nasm/jsimdcfg.inc)

if(CPU_TYPE STREQUAL "x86_64")
  set(SIMD_SOURCES x86_64/jsimdcpu.asm x86_64/jfdctflt-sse.asm
    x86_64/jccolor-sse2.asm x86_64/jcgray-sse2.asm x86_64/jchuff-sse2.asm
    x86_64/jcphuff-sse2.asm x86_64/jcsample-sse2.asm x86_64/jdcolor-sse2.asm
    x86_64/jdmerge-sse2.asm x86_64/jdsample-sse2.asm x86_64/jfdctfst-sse2.asm
    x86_64/jfdctint-sse2.asm x86_64/jidctflt-sse2.asm x86_64/jidctfst-sse2.asm
    x86_64/jidctint-sse2.asm x86_64/jidctred-sse2.asm x86_64/jquantf-sse2.asm
    x86_64/jquanti-sse2.asm
    x86_64/jccolor-avx2.asm x86_64/jcgray-avx2.asm x86_64/jcsample-avx2.asm
    x86_64/jdcolor-avx2.asm x86_64/jdmerge-avx2.asm x86_64/jdsample-avx2.asm
    x86_64/jfdctint-avx2.asm x86_64/jidctint-avx2.asm x86_64/jquanti-avx2.asm)
else()
  set(SIMD_SOURCES i386/jsimdcpu.asm i386/jfdctflt-3dn.asm
    i386/jidctflt-3dn.asm i386/jquant-3dn.asm
    i386/jccolor-mmx.asm i386/jcgray-mmx.asm i386/jcsample-mmx.asm
    i386/jdcolor-mmx.asm i386/jdmerge-mmx.asm i386/jdsample-mmx.asm
    i386/jfdctfst-mmx.asm i386/jfdctint-mmx.asm i386/jidctfst-mmx.asm
    i386/jidctint-mmx.asm i386/jidctred-mmx.asm i386/jquant-mmx.asm
    i386/jfdctflt-sse.asm i386/jidctflt-sse.asm i386/jquant-sse.asm
    i386/jccolor-sse2.asm i386/jcgray-sse2.asm i386/jchuff-sse2.asm
    i386/jcphuff-sse2.asm i386/jcsample-sse2.asm i386/jdcolor-sse2.asm
    i386/jdmerge-sse2.asm i386/jdsample-sse2.asm i386/jfdctfst-sse2.asm
    i386/jfdctint-sse2.asm i386/jidctflt-sse2.asm i386/jidctfst-sse2.asm
    i386/jidctint-sse2.asm i386/jidctred-sse2.asm i386/jquantf-sse2.asm
    i386/jquanti-sse2.asm
    i386/jccolor-avx2.asm i386/jcgray-avx2.asm i386/jcsample-avx2.asm
    i386/jdcolor-avx2.asm i386/jdmerge-avx2.asm i386/jdsample-avx2.asm
    i386/jfdctint-avx2.asm i386/jidctint-avx2.asm i386/jquanti-avx2.asm)
endif()

if(MSVC_IDE)
  set(OBJDIR "${CMAKE_CURRENT_BINARY_DIR}/${CMAKE_CFG_INTDIR}")
  string(REGEX REPLACE " " ";" CMAKE_ASM_NASM_FLAGS "${CMAKE_ASM_NASM_FLAGS}")
elseif(XCODE)
  set(OBJDIR "${CMAKE_CURRENT_BINARY_DIR}")
  string(REGEX REPLACE " " ";" CMAKE_ASM_NASM_FLAGS "${CMAKE_ASM_NASM_FLAGS}")
endif()

file(GLOB INC_FILES nasm/*.inc)

foreach(file ${SIMD_SOURCES})
  set(OBJECT_DEPENDS "")
  if(${file} MATCHES jccolor)
    string(REGEX REPLACE "jccolor" "jccolext" DEPFILE ${file})
    set(OBJECT_DEPENDS ${OBJECT_DEPENDS}
      ${CMAKE_CURRENT_SOURCE_DIR}/${DEPFILE})
  endif()
  if(${file} MATCHES jcgray)
    string(REGEX REPLACE "jcgray" "jcgryext" DEPFILE ${file})
    set(OBJECT_DEPENDS ${OBJECT_DEPENDS}
      ${CMAKE_CURRENT_SOURCE_DIR}/${DEPFILE})
  endif()
  if(${file} MATCHES jdcolor)
    string(REGEX REPLACE "jdcolor" "jdcolext" DEPFILE ${file})
    set(OBJECT_DEPENDS ${OBJECT_DEPENDS}
      ${CMAKE_CURRENT_SOURCE_DIR}/${DEPFILE})
  endif()
  if(${file} MATCHES jdmerge)
    string(REGEX REPLACE "jdmerge" "jdmrgext" DEPFILE ${file})
    set(OBJECT_DEPENDS ${OBJECT_DEPENDS}
      ${CMAKE_CURRENT_SOURCE_DIR}/${DEPFILE})
  endif()
  set(OBJECT_DEPENDS ${OBJECT_DEPENDS} ${INC_FILES})
  if(MSVC_IDE OR XCODE)
    # The CMake Visual Studio generators do not work properly with the ASM_NASM
    # language, so we have to go rogue here and use a custom command like we
    # did in prior versions of libjpeg-turbo.  (This is why we can't have nice
    # things.)
    string(REGEX REPLACE "${CPU_TYPE}/" "" filename ${file})
    set(SIMD_OBJ ${OBJDIR}/${filename}${CMAKE_C_OUTPUT_EXTENSION})
    add_custom_command(OUTPUT ${SIMD_OBJ} DEPENDS ${file} ${OBJECT_DEPENDS}
      COMMAND ${CMAKE_ASM_NASM_COMPILER} -f${CMAKE_ASM_NASM_OBJECT_FORMAT}
        ${CMAKE_ASM_NASM_FLAGS} ${CMAKE_CURRENT_SOURCE_DIR}/${file}
        -o${SIMD_OBJ})
    set(SIMD_OBJS ${SIMD_OBJS} ${SIMD_OBJ})
  else()
    set_source_files_properties(${file} PROPERTIES OBJECT_DEPENDS
      "${OBJECT_DEPENDS}")
  endif()
endforeach()

if(MSVC_IDE OR XCODE)
  set(SIMD_OBJS ${SIMD_OBJS} PARENT_SCOPE)
  add_library(simd OBJECT ${CPU_TYPE}/jsimd.c)
  add_custom_target(simd-objs DEPENDS ${SIMD_OBJS})
  add_dependencies(simd simd-objs)
else()
  add_library(simd OBJECT ${SIMD_SOURCES} ${CPU_TYPE}/jsimd.c)
endif()
if(NOT WIN32 AND (CMAKE_POSITION_INDEPENDENT_CODE OR ENABLE_SHARED))
  set_target_properties(simd PROPERTIES POSITION_INDEPENDENT_CODE 1)
endif()


###############################################################################
# Arm (GAS)
###############################################################################

elseif(CPU_TYPE STREQUAL "arm64" OR CPU_TYPE STREQUAL "arm")

enable_language(ASM)

set(CMAKE_ASM_FLAGS "${CMAKE_C_FLAGS} ${CMAKE_ASM_FLAGS}")

string(TOUPPER ${CMAKE_BUILD_TYPE} CMAKE_BUILD_TYPE_UC)
set(EFFECTIVE_ASM_FLAGS "${CMAKE_ASM_FLAGS} ${CMAKE_ASM_FLAGS_${CMAKE_BUILD_TYPE_UC}}")
message(STATUS "CMAKE_ASM_FLAGS = ${EFFECTIVE_ASM_FLAGS}")

# Test whether we need gas-preprocessor.pl
if(CPU_TYPE STREQUAL "arm")
  file(WRITE ${CMAKE_CURRENT_BINARY_DIR}/gastest.S "
    .text
    .fpu neon
    .arch armv7a
    .object_arch armv4
    .arm
    pld [r0]
    vmovn.u16 d0, q0")
else()
  file(WRITE ${CMAKE_CURRENT_BINARY_DIR}/gastest.S "
    .text
    MYVAR .req x0
    movi v0.16b, #100
    mov MYVAR, #100
    .unreq MYVAR")
endif()

separate_arguments(CMAKE_ASM_FLAGS_SEP UNIX_COMMAND "${CMAKE_ASM_FLAGS}")
execute_process(COMMAND ${CMAKE_ASM_COMPILER} ${CMAKE_ASM_FLAGS_SEP}
    -x assembler-with-cpp -c ${CMAKE_CURRENT_BINARY_DIR}/gastest.S
  RESULT_VARIABLE RESULT OUTPUT_VARIABLE OUTPUT ERROR_VARIABLE ERROR WORKING_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR} ) # MB patch
if(NOT RESULT EQUAL 0)
  message(STATUS "GAS appears to be broken.  Trying gas-preprocessor.pl ...")
  execute_process(COMMAND gas-preprocessor.pl ${CMAKE_ASM_COMPILER}
      ${CMAKE_ASM_FLAGS_SEP} -x assembler-with-cpp -c
      ${CMAKE_CURRENT_BINARY_DIR}/gastest.S
    RESULT_VARIABLE RESULT OUTPUT_VARIABLE OUTPUT ERROR_VARIABLE ERROR)
  if(NOT RESULT EQUAL 0)
    simd_fail("SIMD extensions disabled: GAS is not working properly")
    return()
  else()
    message(STATUS "Using gas-preprocessor.pl")
    configure_file(gas-preprocessor.in gas-preprocessor @ONLY)
    set(CMAKE_ASM_COMPILER ${CMAKE_CURRENT_BINARY_DIR}/gas-preprocessor)
  endif()
else()
  message(STATUS "GAS is working properly")
endif()

file(REMOVE ${CMAKE_CURRENT_BINARY_DIR}/gastest.S)

add_library(simd OBJECT ${CPU_TYPE}/jsimd_neon.S ${CPU_TYPE}/jsimd.c)

if(CMAKE_POSITION_INDEPENDENT_CODE OR ENABLE_SHARED)
  set_target_properties(simd PROPERTIES POSITION_INDEPENDENT_CODE 1)
endif()


###############################################################################
# MIPS (GAS)
###############################################################################

elseif(CPU_TYPE STREQUAL "mips" OR CPU_TYPE STREQUAL "mipsel")

enable_language(ASM)

string(TOUPPER ${CMAKE_BUILD_TYPE} CMAKE_BUILD_TYPE_UC)
set(EFFECTIVE_ASM_FLAGS "${CMAKE_ASM_FLAGS} ${CMAKE_ASM_FLAGS_${CMAKE_BUILD_TYPE_UC}}")
message(STATUS "CMAKE_ASM_FLAGS = ${EFFECTIVE_ASM_FLAGS}")

set(CMAKE_REQUIRED_FLAGS -mdspr2)

check_c_source_compiles("
  #if !(defined(__mips__) && __mips_isa_rev >= 2)
  #error MIPS DSPr2 is currently only available on MIPS32r2 platforms.
  #endif
  int main(void) {
    int c = 0, a = 0, b = 0;
    __asm__ __volatile__ (
      \"precr.qb.ph %[c], %[a], %[b]\"
      : [c] \"=r\" (c)
      : [a] \"r\" (a), [b] \"r\" (b)
    );
    return c;
  }" HAVE_DSPR2)

unset(CMAKE_REQUIRED_FLAGS)

if(NOT HAVE_DSPR2)
  simd_fail("SIMD extensions not available for this CPU")
  return()
endif()

add_library(simd OBJECT mips/jsimd_dspr2.S mips/jsimd.c)

if(CMAKE_POSITION_INDEPENDENT_CODE OR ENABLE_SHARED)
  set_target_properties(simd PROPERTIES POSITION_INDEPENDENT_CODE 1)
endif()

###############################################################################
# Loongson (Intrinsics)
###############################################################################

elseif(CPU_TYPE STREQUAL "loongson")

set(SIMD_SOURCES loongson/jccolor-mmi.c loongson/jcsample-mmi.c
  loongson/jdcolor-mmi.c loongson/jdsample-mmi.c loongson/jfdctint-mmi.c
  loongson/jidctint-mmi.c loongson/jquanti-mmi.c)

if(CMAKE_COMPILER_IS_GNUCC)
  foreach(file ${SIMD_SOURCES})
    set_property(SOURCE ${file} APPEND_STRING PROPERTY COMPILE_FLAGS
      " -fno-strict-aliasing")
  endforeach()
endif()

add_library(simd OBJECT ${SIMD_SOURCES} loongson/jsimd.c)

if(CMAKE_POSITION_INDEPENDENT_CODE OR ENABLE_SHARED)
  set_target_properties(simd PROPERTIES POSITION_INDEPENDENT_CODE 1)
endif()

###############################################################################
# PowerPC (Intrinsics)
###############################################################################

elseif(CPU_TYPE STREQUAL "powerpc")

set(CMAKE_REQUIRED_FLAGS -maltivec)

check_c_source_compiles("
  #include <altivec.h>
  int main(void) {
    __vector int vi = { 0, 0, 0, 0 };
    int i[4];
    vec_st(vi, 0, i);
    return i[0];
  }" HAVE_ALTIVEC)

unset(CMAKE_REQUIRED_FLAGS)

if(NOT HAVE_ALTIVEC)
  simd_fail("SIMD extensions not available for this CPU (PowerPC SPE)")
  return()
endif()

set(SIMD_SOURCES powerpc/jccolor-altivec.c powerpc/jcgray-altivec.c
  powerpc/jcsample-altivec.c powerpc/jdcolor-altivec.c
  powerpc/jdmerge-altivec.c powerpc/jdsample-altivec.c
  powerpc/jfdctfst-altivec.c powerpc/jfdctint-altivec.c
  powerpc/jidctfst-altivec.c powerpc/jidctint-altivec.c
  powerpc/jquanti-altivec.c)

set_source_files_properties(${SIMD_SOURCES} PROPERTIES
  COMPILE_FLAGS -maltivec)

add_library(simd OBJECT ${SIMD_SOURCES} powerpc/jsimd.c)

if(CMAKE_POSITION_INDEPENDENT_CODE OR ENABLE_SHARED)
  set_target_properties(simd PROPERTIES POSITION_INDEPENDENT_CODE 1)
endif()

###############################################################################
# None
###############################################################################

else()

simd_fail("SIMD extensions not available for this CPU (${CMAKE_SYSTEM_PROCESSOR})")

endif() # CPU_TYPE
