
set(_mpas_framework_src
    mpas_abort.F
    mpas_attlist.F
    mpas_block_creator.F
    mpas_block_decomp.F
    mpas_bootstrapping.F
    mpas_c_interfacing.F
    mpas_constants.F
    mpas_decomp.F
    mpas_derived_types.F
    mpas_dmpar.F
    mpas_domain_routines.F
    mpas_field_accessor.F
    mpas_field_routines.F
    mpas_forcing.F
    mpas_framework.F
    mpas_hash.F
    mpas_io.F
    mpas_io_streams.F
    mpas_io_units.F
    mpas_kind_types.F
    mpas_log.F
    mpas_pool_routines.F
    mpas_sort.F
    mpas_stream_list.F
    mpas_stream_manager.F
    mpas_threading.F
    mpas_timekeeping.F
    mpas_timer.F
    pool_hash.c
    random_id.c
    regex_matching.c
    xml_stream_parser.c)

add_library(framework ${_mpas_framework_src})
mpas_fortran_target(framework)
add_library(MPAS::framework ALIAS framework)

set_target_properties(framework PROPERTIES OUTPUT_NAME mpas_framework)

target_link_libraries(framework PUBLIC MPAS::external::esmf)
target_link_libraries(framework PUBLIC MPAS::external::ezxml)
target_link_libraries(framework PUBLIC PIO::PIO_Fortran PIO::PIO_C)
target_link_libraries(framework PUBLIC PnetCDF::PnetCDF_Fortran)
target_link_libraries(framework PUBLIC NetCDF::NetCDF_Fortran)
target_link_libraries(framework PUBLIC MPI::MPI_Fortran)

if(MPAS_PROFILE)
    target_link_libraries(framework PUBLIC GPTL::GPTL)
endif()

install(TARGETS framework EXPORT ${PROJECT_NAME}Exports
        ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR}
        LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR})
