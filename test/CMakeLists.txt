add_executable(multicut_message_passing_test multicut_message_passing_test.cu)
target_link_libraries(multicut_message_passing_test dCOO multicut_message_passing)

add_executable(cc_gpu_test cc_gpu_test.cu)
target_link_libraries(cc_gpu_test ECL-CC_11)

add_executable(rama_cuda_test rama_cuda_test.cu)
target_link_libraries(rama_cuda_test rama_cuda)

add_executable(maximum_matching_vertex_based_test maximum_matching_vertex_based_test.cu)
target_link_libraries(maximum_matching_vertex_based_test dCOO maximum_matching_vertex_based)

#add_executable(maximum_matching_thrust_test maximum_matching_thrust_test.cu)
#target_link_libraries(maximum_matching_thrust_test dCOO maximum_matching_thrust)

add_executable(edge_contractions_woc_test edge_contractions_woc_test.cu)
target_link_libraries(edge_contractions_woc_test dCOO edge_contractions_woc)

add_executable(compute_offsets_test compute_offsets_test.cu)

add_executable(compute_unique_test compute_unique_test.cu)

add_executable(conflicted_cycles_test conflicted_cycles_test.cu)
target_link_libraries(conflicted_cycles_test conflicted_cycles_cuda)

add_executable(persistency_preprocessor_test persistency_preprocessor_test.cu)
target_link_libraries(persistency_preprocessor_test persistency_preprocessor)
