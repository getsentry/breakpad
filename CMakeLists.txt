# The list of files is drived from: breakpad/Makefile.am
cmake_minimum_required(VERSION 3.12)
project(sentry_breakpad)

set(CMAKE_CXX_STANDARD 11)

if(CMAKE_SYSTEM_NAME STREQUAL "Linux")
    set(LINUX TRUE)
endif()

# set static runtime, if enabled
if(SENTRY_BUILD_RUNTIMESTATIC AND MSVC)
    set(CMAKE_MSVC_RUNTIME_LIBRARY "MultiThreaded$<$<CONFIG:Debug>:Debug>")
endif()

if(LINUX)
    option(BREAKPAD_PIC "Build breakpad as position independent code" ON)
else()
    set(BREAKPAD_PIC ON)
endif()
if(BREAKPAD_PIC)
    set(CMAKE_POSITION_INDEPENDENT_CODE ON)
endif()

set(BREAKPAD_SOURCES_COMMON
    src/common/convert_UTF.cc
    src/common/convert_UTF.h
    src/common/md5.cc
    src/common/md5.h
    src/common/string_conversion.cc
    src/common/string_conversion.h
)

set(BREAKPAD_SOURCES_COMMON_EXTRA
)

set(BREAKPAD_SOURCES_COMMON_EXTRA_UNIX
    src/common/dwarf/bytereader.cc
    src/common/dwarf/bytereader.h
    src/common/dwarf/dwarf2diehandler.cc
    src/common/dwarf/dwarf2diehandler.h
    src/common/dwarf/dwarf2reader.cc
    src/common/dwarf/dwarf2reader.h
    src/common/dwarf/elf_reader.cc
    src/common/dwarf/elf_reader.h
    src/common/dwarf_cfi_to_module.cc
    src/common/dwarf_cfi_to_module.h
    src/common/dwarf_cu_to_module.cc
    src/common/dwarf_cu_to_module.h
    src/common/dwarf_line_to_module.cc
    src/common/dwarf_line_to_module.h
    src/common/dwarf_range_list_handler.cc
    src/common/dwarf_range_list_handler.h
    src/common/path_helper.cc
    src/common/path_helper.h
    src/common/language.cc
    src/common/language.h
    src/common/module.cc
    src/common/module.h
    src/common/stabs_to_module.cc
    src/common/stabs_to_module.h
    src/common/stabs_reader.cc
    src/common/stabs_reader.h
)

set(BREAKPAD_SOURCES_COMMON_LINUX
    src/common/linux/elf_core_dump.cc
    src/common/linux/elfutils.cc
    src/common/linux/elfutils.h
    src/common/linux/file_id.cc
    src/common/linux/file_id.h
    src/common/linux/guid_creator.cc
    src/common/linux/guid_creator.h
    src/common/linux/linux_libc_support.cc
    src/common/linux/memory_mapped_file.cc
    src/common/linux/safe_readlink.cc
)

set(BREAKPAD_SOURCES_COMMON_EXTRA_LINUX
    src/common/linux/crc32.h
    src/common/linux/crc32.cc
    src/common/linux/dump_symbols.h
    src/common/linux/dump_symbols.cc
    src/common/linux/elf_symbols_to_module.cc
    src/common/linux/elf_symbols_to_module.h
)

set(BREAKPAD_SOURCES_COMMON_LINUX_GETCONTEXT
    src/common/linux/breakpad_getcontext.S
)

set(BREAKPAD_SOURCES_COMMON_ANDROID
    src/common/android/include/sys/procfs.h
)

set(BREAKPAD_SOURCES_COMMON_WINDOWS
    src/common/windows/guid_string.cc
    src/common/windows/guid_string.h
)

set(BREAKPAD_SOURCES_COMMON_EXTRA_WINDOWS
    src/common/windows/dia_util.cc
    src/common/windows/dia_util.h
    src/common/windows/omap.cc
    src/common/windows/omap.h
    src/common/windows/pdb_source_line_writer.cc
    src/common/windows/pdb_source_line_writer.h
    src/common/windows/pe_source_line_writer.cc
    src/common/windows/pe_source_line_writer.h
    src/common/windows/pe_util.cc
    src/common/windows/pe_util.h
    src/common/windows/string_utils.cc
    src/common/windows/string_utils-inl.h
)

set(BREAKPAD_SOURCES_COMMON_APPLE
    src/common/mac/file_id.cc
    src/common/mac/file_id.h
    src/common/mac/macho_id.cc
    src/common/mac/macho_id.h
    src/common/mac/macho_utilities.cc
    src/common/mac/macho_utilities.h
    src/common/mac/macho_walker.cc
    src/common/mac/macho_walker.h
    src/common/mac/string_utilities.cc
    src/common/mac/string_utilities.h
)

set(BREAKPAD_SOURCES_COMMON_MAC
    src/common/mac/MachIPC.mm
    src/common/mac/bootstrap_compat.cc
    src/common/mac/bootstrap_compat.h
)

set(BREAKPAD_SOURCES_COMMON_EXTRA_APPLE
    src/common/mac/arch_utilities.cc
    src/common/mac/arch_utilities.h
    src/common/mac/dump_syms.cc
    src/common/mac/dump_syms.h
    src/common/mac/macho_reader.cc
    src/common/mac/macho_reader.h
)

set(BREAKPAD_SOURCES_CLIENT_LINUX
    src/client/minidump_file_writer-inl.h
    src/client/minidump_file_writer.cc
    src/client/minidump_file_writer.h
    src/client/linux/crash_generation/crash_generation_client.cc
    src/client/linux/crash_generation/crash_generation_server.cc
    src/client/linux/dump_writer_common/thread_info.cc
    src/client/linux/dump_writer_common/ucontext_reader.cc
    src/client/linux/handler/exception_handler.cc
    src/client/linux/handler/exception_handler.h
    src/client/linux/handler/minidump_descriptor.cc
    src/client/linux/handler/minidump_descriptor.h
    src/client/linux/log/log.cc
    src/client/linux/log/log.h
    src/client/linux/microdump_writer/microdump_writer.cc
    src/client/linux/microdump_writer/microdump_writer.h
    src/client/linux/minidump_writer/linux_core_dumper.cc
    src/client/linux/minidump_writer/linux_dumper.cc
    src/client/linux/minidump_writer/linux_ptrace_dumper.cc
    src/client/linux/minidump_writer/minidump_writer.cc
)

set(BREAKPAD_SOURCES_CLIENT_WINDOWS
    src/client/windows/crash_generation/crash_generation_client.cc
    src/client/windows/crash_generation/crash_generation_client.h
    src/client/windows/handler/exception_handler.cc
    src/client/windows/handler/exception_handler.h
)

set(BREAKPAD_SOURCES_CLIENT_APPLE
    src/client/minidump_file_writer-inl.h
    src/client/minidump_file_writer.cc
    src/client/minidump_file_writer.h
    src/client/mac/handler/breakpad_nlist_64.cc
    src/client/mac/handler/breakpad_nlist_64.h
    src/client/mac/handler/dynamic_images.cc
    src/client/mac/handler/dynamic_images.h
    src/client/mac/handler/exception_handler.cc
    src/client/mac/handler/exception_handler.h
    src/client/mac/handler/minidump_generator.cc
    src/client/mac/handler/minidump_generator.h
)

set(BREAKPAD_SOURCES_CLIENT_MAC
    src/client/mac/crash_generation/crash_generation_client.cc
    src/client/mac/crash_generation/crash_generation_client.h
)

set(BREAKPAD_SOURCES_CLIENT_IOS
    src/client/ios/exception_handler_no_mach.cc
    src/client/ios/exception_handler_no_mach.h
    src/client/ios/handler/ios_exception_minidump_generator.h
    src/client/ios/handler/ios_exception_minidump_generator.mm
    src/client/mac/crash_generation/ConfigFile.h
    src/client/mac/crash_generation/ConfigFile.mm
    src/client/mac/handler/mach_vm_compat.h
    src/client/mac/handler/protected_memory_allocator.cc
    src/client/mac/handler/protected_memory_allocator.h
    src/client/mac/handler/ucontext_compat.h
)

set(BREAKPAD_SOURCES_DUMPSYMS_LINUX
    src/tools/linux/dump_syms/dump_syms.cc
)

set(BREAKPAD_SOURCES_DUMPSYMS_WINDOWS
    src/tools/windows/dump_syms/dump_syms.cc
)

set(BREAKPAD_SOURCES_DUMPSYMS_MAC
    src/tools/mac/dump_syms/dump_syms_tool.cc
)

set(BREAKPAD_SOURCES_MACHODUMP_MAC
    src/tools/mac/dump_syms/macho_dump.cc
)

add_library(breakpad_common OBJECT)
add_library(breakpad_common_extra OBJECT EXCLUDE_FROM_ALL)
add_library(breakpad_client STATIC)
add_executable(dump_syms)

target_sources(breakpad_common PRIVATE ${BREAKPAD_SOURCES_COMMON})
target_link_libraries(breakpad_client PRIVATE $<BUILD_INTERFACE:breakpad_common>)

target_sources(breakpad_common_extra PRIVATE ${BREAKPAD_SOURCES_COMMON_EXTRA})
target_link_libraries(breakpad_common_extra PUBLIC breakpad_common)

target_link_libraries(dump_syms PRIVATE breakpad_common breakpad_common_extra)

if(LINUX OR ANDROID)
    target_sources(breakpad_common PRIVATE ${BREAKPAD_SOURCES_COMMON_LINUX})
    target_sources(breakpad_common_extra PRIVATE ${BREAKPAD_SOURCES_COMMON_EXTRA_UNIX} ${BREAKPAD_SOURCES_COMMON_EXTRA_LINUX})
    target_sources(breakpad_client PRIVATE ${BREAKPAD_SOURCES_CLIENT_LINUX})
    target_sources(dump_syms PRIVATE ${BREAKPAD_SOURCES_DUMPSYMS_LINUX})
    if(ANDROID)
        target_sources(breakpad_common PRIVATE ${BREAKPAD_SOURCES_COMMON_ANDROID})
        target_include_directories(breakpad_common PUBLIC src/common/android/include)
    endif()
        if(LINUX)
            find_package(Threads REQUIRED)
            target_link_libraries(breakpad_common_extra PRIVATE Threads::Threads)
        endif()

    include(CheckFunctionExists)
    check_function_exists(getcontext HAVE_GETCONTEXT)
    if(HAVE_GETCONTEXT)
        target_compile_definitions(breakpad_common PUBLIC HAVE_GETCONTEXT)
        target_sources(breakpad_common PRIVATE ${BREAKPAD_SOURCES_COMMON_LINUX_GETCONTEXT})
    endif()
endif()

if(APPLE)
    target_sources(breakpad_common PRIVATE ${BREAKPAD_SOURCES_COMMON_APPLE})
    target_sources(breakpad_common_extra PRIVATE ${BREAKPAD_SOURCES_COMMON_EXTRA_UNIX} ${BREAKPAD_SOURCES_COMMON_EXTRA_APPLE})
    target_sources(breakpad_client PRIVATE ${BREAKPAD_SOURCES_CLIENT_APPLE})
    target_sources(dump_syms PRIVATE ${BREAKPAD_SOURCES_DUMPSYMS_MAC})
    add_executable(macho_dump ${BREAKPAD_SOURCES_MACHODUMP_MAC})
    target_link_libraries(macho_dump PRIVATE breakpad_common breakpad_common_extra)
        target_compile_definitions(breakpad_common PRIVATE HAVE_MACH_O_NLIST_H)
        target_compile_definitions(breakpad_common_extra PRIVATE HAVE_MACH_O_NLIST_H)
    if(NOT IOS)
        target_sources(breakpad_common PRIVATE ${BREAKPAD_SOURCES_COMMON_MAC})
        target_sources(breakpad_client PRIVATE ${BREAKPAD_SOURCES_CLIENT_MAC})
    else()
        target_sources(breakpad_client PRIVATE ${BREAKPAD_SOURCES_CLIENT_IOS})
    endif()

    target_link_libraries(breakpad_common PRIVATE "-framework CoreFoundation")
endif()

if(WIN32)
    target_sources(breakpad_common PRIVATE ${BREAKPAD_SOURCES_COMMON_WINDOWS})
    target_sources(breakpad_common_extra PRIVATE ${BREAKPAD_SOURCES_COMMON_EXTRA_WINDOWS})
    target_sources(breakpad_client PRIVATE ${BREAKPAD_SOURCES_CLIENT_WINDOWS})
    target_sources(dump_syms PRIVATE ${BREAKPAD_SOURCES_DUMPSYMS_WINDOWS})

    target_compile_definitions(breakpad_common PUBLIC _UNICODE UNICODE)

    target_compile_options(breakpad_common_extra PUBLIC
        "-I$(VsInstallDir)/DIA SDK/include"
    )
    if(CMAKE_SYSTEM_PROCESSOR MATCHES "^([xX]86(_64)?|amd64|AMD64|[iI]?[3-7]86|intel|INTEL)$")
        if(CMAKE_SIZEOF_VOID_P EQUAL 8)
            set(diaguids_libsubdir "/amd64")
        else()
            set(diaguids_libsubdir "")
        endif()
    elseif(CMAKE_SYSTEM_PROCESSOR MATCHES "^(aarch64|AARCH64|arm.*)$")
        if(CMAKE_SIZEOF_VOID_P EQUAL 8)
            set(diaguids_libsubdir "/arm64")
        else()
            set(diaguids_libsubdir "/arm")
        endif()
    else()
        message(FATAL_ERROR "Unknown CMAKE_SYSTEM_PROCESSOR (${CMAKE_SYSTEM_PROCESSOR}). Don't know where diaguids library lives.")
    endif()
    target_link_options(breakpad_common_extra PUBLIC
        "-LIBPATH:$(VsInstallDir)/DIA SDK/lib${diaguids_libsubdir}"
    )
    target_link_libraries(breakpad_common_extra PRIVATE dbghelp diaguids imagehlp)
endif()

# breakpad has includes directly to `third_party/lss/...`,
# which are being resolved correctly when we add the current directory to
# the include directories. A giant hack, yes, but it works
target_include_directories(breakpad_common
    PUBLIC
        "$<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/src>"
        "$<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}>"
)
target_include_directories(breakpad_client
    PUBLIC
        "$<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}>"
)
