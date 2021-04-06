cmake_minimum_required(VERSION 3.7)
set(NNOM_PROJECT_NAME nnom-lib)

project(${NNOM_PROJECT_NAME})

set(CMAKE_C_STANDARD 11)
set(CMAKE_CXX_STANDARD 14)

if (UNIX AND NOT APPLE)
    set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -fPIC")
endif (UNIX AND NOT APPLE)

if (MSVC)
    add_compile_options(/W3)
else ()
    add_compile_options(-Wall -Wextra -Wpedantic)
endif ()

include_directories(
        port
        inc
        inc/layers

        src/layers
        src/core
        src/backends
)
set(SOURCE_FILES
        port/nnom_port.h

        inc/nnom.h
        src/core/nnom.c
        inc/nnom_layers.h
        src/core/nnom_layers.c
        inc/nnom_local.h
        src/backends/nnom_local.c
        src/backends/nnom_local_q15.c
        inc/nnom_tensor.h
        src/core/nnom_tensor.c
        inc/nnom_utils.h
        src/core/nnom_utils.c

        inc/layers/nnom_avgpool.h
        src/layers/nnom_avgpool.c

        inc/layers/nnom_activation.h
        src/layers/nnom_activation.c

        inc/layers/nnom_baselayer.h
        src/layers/nnom_baselayer.c

        inc/layers/nnom_concat.h
        src/layers/nnom_concat.c

        inc/layers/nnom_conv2d.h
        src/layers/nnom_conv2d.c

        inc/layers/nnom_conv2d_trans.h
        src/layers/nnom_conv2d_trans.c

        inc/layers/nnom_cropping.h
        src/layers/nnom_cropping.c

        inc/layers/nnom_dense.h
        src/layers/nnom_dense.c

        inc/layers/nnom_dw_conv2d.h
        src/layers/nnom_dw_conv2d.c

        inc/layers/nnom_flatten.h
        src/layers/nnom_flatten.c

        inc/layers/nnom_global_pool.h
        src/layers/nnom_global_pool.c

        inc/layers/nnom_gru_cell.h
        src/layers/nnom_gru_cell.c

        inc/layers/nnom_input.h
        src/layers/nnom_input.c

        inc/layers/nnom_lambda.h
        src/layers/nnom_lambda.c

        inc/layers/nnom_lstm_cell.h
        src/layers/nnom_lstm_cell.c

        inc/layers/nnom_matrix.h
        src/layers/nnom_maxpool.c

        inc/layers/nnom_output.h
        src/layers/nnom_output.c

        inc/layers/nnom_rnn.h
        src/layers/nnom_rnn.c

        inc/layers/nnom_simple_cell.h
        src/layers/nnom_simple_cell.c

        inc/layers/nnom_softmax.h
        src/layers/nnom_softmax.c

        inc/layers/nnom_sumpool.h
        src/layers/nnom_sumpool.c

        inc/layers/nnom_upsample.h
        src/layers/nnom_upsample.c

        inc/layers/nnom_zero_padding.h
        src/layers/nnom_zero_padding.c
        )

add_library(${NNOM_PROJECT_NAME} ${SOURCE_FILES})