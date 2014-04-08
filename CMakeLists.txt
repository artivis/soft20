cmake_minimum_required(VERSION 2.8.3)
project(soft20)

find_package(catkin REQUIRED COMPONENTS
  
)


catkin_package(

)


include_directories(
  ${catkin_INCLUDE_DIRS} include
)

## Declare cpp libraries

add_library(	soft20-sym

	     	src/lib0/cospmls.c
		src/lib0/FFTcode.c
		src/lib0/fft_grids.c
		src/lib0/fft_grids_so3.c
		src/lib0/FST_semi_memo.c
		src/lib0/indextables.c
		src/lib0/legendreTransforms.c
		src/lib0/newFCT.c
		src/lib0/oddweights.c
		src/lib0/OURmods.c
		src/lib0/OURperms.c
		src/lib0/permroots.c
		src/lib0/rotate_so3.c
		src/lib0/rotate_so3_mem.c
		src/lib0/so3_correlate_sym.c
		src/lib0/soft.c
		src/lib0/soft_sym.c
		src/lib0/weights.c
		src/lib0/wignerTransforms_sym.c
		src/lib0/wrap_s2_rotate.c
		src/lib0/wrap_soft.c
		src/lib0/wrap_soft_sym.c
		src/lib0/wrap_soft_sym_cor2.c
)

add_library(	soft20-fftw

		src/lib1/rotate_so3_fftw.c
		src/lib1/rotate_so3_utils.c
		src/lib1/s2_cospmls.c
		src/lib1/s2_legendreTransforms.c
		src/lib1/s2_semi_fly.c
		src/lib1/s2_semi_memo.c
		src/lib1/so3_correlate_fftw.c
		src/lib1/soft_fftw.c
		src/lib1/soft_fftw_nt.c
		src/lib1/soft_fftw_pc.c
		src/lib1/utils_vec_cx.c
		src/lib1/wignerTransforms_fftw.c
		src/lib1/wrap_s2_rotate_fftw.c
		src/lib1/wrap_soft_fftw.c
		src/lib1/wrap_soft_fftw_cor2.c
)
target_link_libraries(soft20-fftw -lfftw3)

add_library(	soft20-common

		src/common/csecond.c
		src/common/makeweights.c
		src/common/makeWigner.c
		src/common/s2_primitive.c
		src/common/utils_so3.c
		src/common/wignerTransforms.c
)


## Declare cpp executables

add_executable(test_genWig examples/test_genWig.c)
target_link_libraries(test_genWig soft20-common m)

add_executable(test_Wigner_Analysis examples/test_Wigner_Analysis.c)
target_link_libraries(test_Wigner_Analysis soft20-common m)

add_executable(test_Wigner_angle examples/test_Wigner_angle.c)
target_link_libraries(test_Wigner_angle soft20-common m)

add_executable(test_Wigner_Naive examples/test_Wigner_Naive.c)
target_link_libraries(test_Wigner_Naive soft20-common m)

add_executable(test_Wigner_Synthesis examples/test_Wigner_Synthesis.c)
target_link_libraries(test_Wigner_Synthesis soft20-common m)

add_executable(test_wigSpec examples/test_wigSpec.c)
target_link_libraries(test_wigSpec soft20-common m)



add_executable(test_s2_rotate examples0/test_s2_rotate.c)
target_link_libraries(test_s2_rotate soft20-sym soft20-common m)

add_executable(test_s2_rotate_mem examples0/test_s2_rotate_mem.c)
target_link_libraries(test_s2_rotate_mem soft20-sym soft20-common m)

add_executable(test_s2_rotate_wrap examples0/test_s2_rotate_wrap.c)
target_link_libraries(test_s2_rotate_wrap soft20-sym soft20-common m)

add_executable(test_soft examples0/test_soft.c)
target_link_libraries(test_soft soft20-sym soft20-common m)

add_executable(test_soft_for examples0/test_soft_for.c)
target_link_libraries(test_soft_for soft20-sym soft20-common m)

add_executable(test_soft_inv examples0/test_soft_inv.c)
target_link_libraries(test_soft_inv soft20-sym soft20-common m)

add_executable(test_soft_sym examples0/test_soft_sym.c)
target_link_libraries(test_soft_sym soft20-sym soft20-common m)

add_executable(test_soft_sym_correlate2 examples0/test_soft_sym_correlate2.c)
target_link_libraries(test_soft_sym_correlate2 soft20-sym soft20-common m)

add_executable(test_soft_sym_correlate2_wrap examples0/test_soft_sym_correlate2_wrap.c)
target_link_libraries(test_soft_sym_correlate2_wrap soft20-sym soft20-common m)

add_executable(test_soft_sym_correlate examples0/test_soft_sym_correlate.c)
target_link_libraries(test_soft_sym_correlate soft20-sym soft20-common m)

add_executable(test_soft_sym_for examples0/test_soft_sym_for.c)
target_link_libraries(test_soft_sym_for soft20-sym soft20-common m)

add_executable(test_soft_sym_inv examples0/test_soft_sym_inv.c)
target_link_libraries(test_soft_sym_inv soft20-sym soft20-common m)



add_executable(test_s2_rotate_fftw examples1/test_s2_rotate_fftw.c)
target_link_libraries(test_s2_rotate_fftw soft20-fftw soft20-common m)

add_executable(test_s2_rotate_fftw_mem examples1/test_s2_rotate_fftw_mem.c)
target_link_libraries(test_s2_rotate_fftw_mem soft20-fftw soft20-common m)

add_executable(test_s2_rotate_fftw_wrap examples1/test_s2_rotate_fftw_wrap.c)
target_link_libraries(test_s2_rotate_fftw_wrap soft20-fftw soft20-common m)

add_executable(test_soft_fftw examples1/test_soft_fftw.c)
target_link_libraries(test_soft_fftw soft20-fftw soft20-common m)

add_executable(test_soft_fftw_correlate2 examples1/test_soft_fftw_correlate2.c)
target_link_libraries(test_soft_fftw_correlate2 soft20-fftw soft20-common m)

add_executable(test_soft_fftw_correlate2_wrap examples1/test_soft_fftw_correlate2_wrap.c)
target_link_libraries(test_soft_fftw_correlate2_wrap soft20-fftw soft20-common m)

add_executable(test_soft_fftw_for examples1/test_soft_fftw_for.c)
target_link_libraries(test_soft_fftw_for soft20-fftw soft20-common m)

add_executable(test_soft_fftw_inv examples1/test_soft_fftw_inv.c)
target_link_libraries(test_soft_fftw_inv soft20-fftw soft20-common m)

add_executable(test_soft_fftw_nt examples1/test_soft_fftw_nt.c)
target_link_libraries(test_soft_fftw_nt soft20-fftw soft20-common m)

add_executable(test_soft_fftw_pc examples1/test_soft_fftw_pc.c)
target_link_libraries(test_soft_fftw_pc soft20-fftw soft20-common m)

