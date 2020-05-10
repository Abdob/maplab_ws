cmake_minimum_required(VERSION 2.8.3)
project(lpsolve)

add_definitions(-O3 -DYY_NEVER_INTERACTIVE -DPARSER_LP -DINVERSE_ACTIVE=INVERSE_LUSOL -DRoleIsExternalInvEngine)

include_directories(bfp bfp/bfp_LUSOL bfp/bfp_LUSOL/LUSOL colamd shared ${PROJECT_SOURCE_DIR})

add_library(${PROJECT_NAME} SHARED lp_MDO.c shared/commonlib.c colamd/colamd.c shared/mmio.c shared/myblas.c ini.c fortify.c lp_rlp.c lp_crash.c bfp/bfp_LUSOL/lp_LUSOL.c bfp/bfp_LUSOL/LUSOL/lusol.c lp_Hash.c lp_lib.c lp_wlp.c lp_matrix.c lp_mipbb.c lp_MPS.c lp_params.c lp_presolve.c lp_price.c lp_pricePSE.c lp_report.c lp_scale.c lp_simplex.c lp_SOS.c lp_utils.c yacc_read.c)
target_link_libraries(${PROJECT_NAME} dl m)

add_executable(${PROJECT_NAME}_exe lp_solve/lp_solve.c)
target_link_libraries(${PROJECT_NAME}_exe ${PROJECT_NAME})

install(FILES ${CMAKE_CURRENT_BINARY_DIR}/lib${PROJECT_NAME}${CMAKE_SHARED_LIBRARY_SUFFIX} DESTINATION lib)

file(GLOB_RECURSE PROJECT_HEADERS ${PROJECT_SOURCE_DIR}/*.h)
install(FILES ${PROJECT_HEADERS} DESTINATION include/lp_solve)