add_library(multicut_text_parser multicut_text_parser.cpp)

add_library(dCOO dCOO.cu)
target_link_libraries(dCOO ECL-CC_11)

add_library(multicut_message_passing multicut_message_passing.cu)

add_library(conflicted_cycles_cuda conflicted_cycles_cuda.cu)
target_link_libraries(conflicted_cycles_cuda dCOO)

add_library(dual_solver dual_solver.cu)
target_link_libraries(dual_solver dCOO conflicted_cycles_cuda multicut_message_passing)

add_library(maximum_matching_vertex_based maximum_matching_vertex_based.cu)
target_link_libraries(maximum_matching_vertex_based dCOO)

#add_library(maximum_matching_thrust maximum_matching_thrust.cu)
#target_link_libraries(maximum_matching_thrust dCOO)

add_library(edge_contractions_woc_thrust edge_contractions_woc_thrust.cu)
target_link_libraries(edge_contractions_woc_thrust dCOO ECL-CC_11 gpuMST_boruvka)

add_library(edge_contractions_woc edge_contractions_woc.cu)
target_link_libraries(edge_contractions_woc edge_contractions_woc_thrust dCOO ECL-CC_11 gpuMST_boruvka)

add_library(persistency_preprocessor persistency_preprocessor.cu)
target_link_libraries(persistency_preprocessor dCOO dual_solver edge_contractions_woc rama_cuda)

add_library(rama_cuda rama_cuda.cu)
target_link_libraries(rama_cuda dCOO dual_solver maximum_matching_vertex_based edge_contractions_woc persistency_preprocessor)

add_executable(rama_text_input rama_text_input.cu)
target_link_libraries(rama_text_input multicut_text_parser rama_cuda persistency_preprocessor)

pybind11_add_module(rama_py rama_py.cu)
target_link_libraries(rama_py PRIVATE multicut_text_parser rama_cuda) 

if(WITH_TORCH)
    find_library(TORCH_PYTHON_LIBRARY torch_python PATHS "${TORCH_INSTALL_PREFIX}/lib")
    message(STATUS "TORCH_PYTHON_LIBRARY: ${TORCH_PYTHON_LIBRARY}") # https://github.com/pytorch/pytorch/issues/38122#issuecomment-694203281
    target_link_libraries(rama_py PRIVATE "${TORCH_LIBRARIES}" ${TORCH_PYTHON_LIBRARY}) 
endif()
