cmake_minimum_required(VERSION 3.16)
project(port_webp CXX)


if (MSVC)
    #set(CMAKE_DEBUG_POSTFIX "d")
    add_definitions(-D_CRT_SECURE_NO_DEPRECATE)
    add_definitions(-D_CRT_NONSTDC_NO_DEPRECATE)
    include_directories(${CMAKE_CURRENT_SOURCE_DIR})
endif ()


list(APPEND library_source

   src/dsp/dsp.upsampling_mips_dsp_r2.c
   src/dsp/dsp.enc_mips32.c
   src/dsp/dsp.lossless_mips_dsp_r2.c
   src/dsp/dsp.rescaler_mips_dsp_r2.c
   src/dsp/dsp.lossless_mips32.c
   src/dsp/dsp.filters_mips_dsp_r2.c
   src/dsp/dsp.enc_mips_dsp_r2.c
   src/dsp/dsp.argb_mips_dsp_r2.c
   src/dsp/dsp.cost_mips32.c
   src/dsp/dsp.cost_mips_dsp_r2.c
   src/dsp/dsp.dec_mips32.c
   src/dsp/dsp.dec_mips_dsp_r2.c
   src/dsp/dsp.rescaler_mips32.c
   src/dsp/dsp.yuv_mips_dsp_r2.c
   src/dsp/dsp.upsampling_neon.c
   src/dsp/dsp.enc_neon.c
   src/dsp/dsp.dec_neon.c
   src/dsp/dsp.upsampling_sse2.c

   src/dec/dec.alpha.c
        src/dec/dec.buffer.c
        src/dec/dec.frame.c
        src/dec/dec.idec.c
        src/dec/dec.io.c
        src/dec/dec.quant.c
        src/dec/dec.tree.c
        src/dec/dec.vp8.c
        src/dec/dec.vp8l.c
        src/dec/dec.webp.c
        src/demux/demux.demux.c
        src/dsp/dsp.alpha_processing.c
        src/dsp/dsp.alpha_processing_mips_dsp_r2.c
        src/dsp/dsp.alpha_processing_sse2.c
        src/dsp/dsp.argb.c
        src/dsp/dsp.argb_sse2.c
        src/dsp/dsp.cost.c
        src/dsp/dsp.cost_sse2.c
        src/dsp/dsp.cpu.c
        src/dsp/dsp.dec.c
        src/dsp/dsp.dec_clip_tables.c
        src/dsp/dsp.dec_sse2.c
        src/dsp/dsp.enc.c
        src/dsp/dsp.enc_avx2.c
        src/dsp/dsp.enc_sse2.c
        src/dsp/dsp.filters.c
        src/dsp/dsp.filters_sse2.c
   include/port_webp/dsp/dsp.h
        src/dsp/dsp.lossless.c
        src/dsp/dsp.lossless_neon.c
        src/dsp/dsp.lossless_sse2.c
        src/dsp/dsp.rescaler.c
        src/dsp/dsp.upsampling.c
        src/dsp/dsp.yuv.c
        src/dsp/dsp.yuv_mips32.c
        src/dsp/dsp.yuv_sse2.c
   include/port_webp/dsp/lossless.h
   include/port_webp/dsp/mips_macro.h
   include/port_webp/dsp/neon.h
   include/port_webp/dsp/yuv.h
   include/port_webp/dsp/yuv_tables_sse2.h
   include/port_webp/enc/backward_references.h
   include/port_webp/enc/cost.h
        src/enc/enc.alpha.c
        src/enc/enc.analysis.c
        src/enc/enc.backward_references.c
        src/enc/enc.config.c
        src/enc/enc.cost.c
        src/enc/enc.filter.c
        src/enc/enc.frame.c
        src/enc/enc.histogram.c
        src/enc/enc.iterator.c
        src/enc/enc.near_lossless.c
        src/enc/enc.picture.c
        src/enc/enc.picture_csp.c
        src/enc/enc.picture_psnr.c
        src/enc/enc.picture_rescale.c
        src/enc/enc.picture_tools.c
        src/enc/enc.quant.c
        src/enc/enc.syntax.c
        src/enc/enc.token.c
        src/enc/enc.tree.c
        src/enc/enc.vp8l.c
        src/enc/enc.webpenc.c
   include/port_webp/enc/histogram.h
   include/port_webp/enc/vp8enci.h
   include/port_webp/enc/vp8li.h
        src/mux/mux.anim_encode.c
        src/mux/mux.muxedit.c
        src/mux/mux.muxinternal.c
        src/mux/mux.muxread.c
   include/port_webp/mux/muxi.h
   include/port_webp/utils/bit_reader.h
   include/port_webp/utils/bit_reader_inl.h
   include/port_webp/utils/bit_writer.h
   include/port_webp/utils/color_cache.h
   include/port_webp/utils/endian_inl.h
   include/port_webp/utils/filters.h
   include/port_webp/utils/huffman.h
   include/port_webp/utils/huffman_encode.h
   include/port_webp/utils/quant_levels.h
   include/port_webp/utils/quant_levels_dec.h
   include/port_webp/utils/random.h
   include/port_webp/utils/rescaler.h
   include/port_webp/utils/thread.h
        src/utils/utils.bit_reader.c
        src/utils/utils.bit_writer.c
        src/utils/utils.color_cache.c
        src/utils/utils.filters.c
   include/port_webp/utils/utils.h
        src/utils/utils.huffman.c
        src/utils/utils.huffman_encode.c
        src/utils/utils.quant_levels.c
        src/utils/utils.quant_levels_dec.c
        src/utils/utils.random.c
        src/utils/utils.rescaler.c
        src/utils/utils.thread.c
        src/utils/utils.utils.c
        include/port_webp/webp/decode.h
   include/port_webp/webp/demux.h
   include/port_webp/webp/encode.h
   include/port_webp/webp/format_constants.h
   include/port_webp/webp/mux.h
   include/port_webp/webp/mux_types.h
   include/port_webp/webp/types.h
)


add_library(${PROJECT_NAME} SHARED ${library_source})


target_compile_definitions(${PROJECT_NAME} PRIVATE OPJ_EXPORTS)

if(MSVC)

    set_target_properties(${PROJECT_NAME} PROPERTIES WINDOWS_EXPORT_ALL_SYMBOLS ON )
    target_compile_options(${PROJECT_NAME} PRIVATE "/MD$<$<CONFIG:Debug>:d>")
    target_link_options(${PROJECT_NAME} PRIVATE "/DEFAULTLIB:msvcrt$<$<CONFIG:Debug>:d>")
    target_link_options(${PROJECT_NAME} PRIVATE "/IMPLIB:${LIBRARY_OUTPUT_PATH}/${PROJECT_NAME}.lib")
    #    target_link_options(${PROJECT_NAME} PRIVATE "/DEF:${CMAKE_CURRENT_SOURCE_DIR}/${PROJECT_NAME}.def")


endif()



target_include_directories(${PROJECT_NAME} PRIVATE ${CMAKE_CURRENT_SOURCE_DIR})
target_include_directories(${PROJECT_NAME} PRIVATE ${CMAKE_CURRENT_SOURCE_DIR}/..)
target_include_directories(${PROJECT_NAME} PRIVATE ${CMAKE_CURRENT_SOURCE_DIR}/../webp)
target_include_directories(${PROJECT_NAME} PRIVATE ${CMAKE_CURRENT_SOURCE_DIR}/../jxr/common)
target_include_directories(${PROJECT_NAME} PRIVATE ${CMAKE_CURRENT_SOURCE_DIR}/include/FreeImage)
target_include_directories(${PROJECT_NAME} PRIVATE ${CMAKE_CURRENT_SOURCE_DIR}/../../../operating_system/operating_system-${OPERATING_SYSTEM_LOWERED_NAME}/configuration/FreeImage)



