# nestkernel/CMakeLists.txt
#
# This file is part of NEST.
#
# Copyright (C) 2004 The NEST Initiative
#
# NEST is free software: you can redistribute it and/or modify
# it under the terms of the GNU General Public License as published by
# the Free Software Foundation, either version 2 of the License, or
# (at your option) any later version.
#
# NEST is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU General Public License for more details.
#
# You should have received a copy of the GNU General Public License
# along with NEST.  If not, see <http://www.gnu.org/licenses/>.

set( nestkernel_sources
    universal_data_logger_impl.h universal_data_logger.h
    recordables_map.h
    archiving_node.h archiving_node.cpp
    common_synapse_properties.h common_synapse_properties.cpp
    sibling_container.h sibling_container.cpp
    subnet.h subnet.cpp
    connection.h
    connection_label.h
    common_properties_hom_w.h
    syn_id_delay.h
    connector_base.h connector_base.cpp
    connector_model.h connector_model_impl.h connector_model.cpp
    connection_id.h connection_id.cpp
    device.h device.cpp
    dynamicloader.h dynamicloader.cpp
    event.h event.cpp
    exceptions.h exceptions.cpp
    genericmodel.h genericmodel_impl.h
    gid_collection.h gid_collection.cpp
    histentry.h histentry.cpp
    model.h model.cpp
    model_manager.h model_manager_impl.h model_manager.cpp
    nest_types.h
    nest_datums.h nest_datums.cpp
    nest_names.cpp nest_names.h
    nestmodule.h nestmodule.cpp
    nest_time.h nest_time.cpp
    nest_timeconverter.h nest_timeconverter.cpp
    modelrange.h modelrange.cpp
    modelrange_manager.h modelrange_manager.cpp
    multirange.h multirange.cpp
    node.h node.cpp
    nodelist.h nodelist.cpp
    proxynode.h proxynode.cpp
    recording_device.h recording_device.cpp
    pseudo_recording_device.h
    ring_buffer.h ring_buffer.cpp
    spikecounter.h spikecounter.cpp
    stimulating_device.h
    target_identifier.h
    sparse_node_array.h sparse_node_array.cpp
    conn_parameter.h conn_parameter.cpp
    conn_builder.h conn_builder_impl.h conn_builder.cpp
    conn_builder_factory.h
    music_event_handler.h music_event_handler.cpp
    music_manager.cpp music_manager.h
    nest.h nest.cpp
    synaptic_element.h synaptic_element.cpp
    growth_curve.h growth_curve.cpp
    growth_curve_factory.h
    kernel_manager.h kernel_manager.cpp
    vp_manager.h vp_manager_impl.h vp_manager.cpp
    io_manager.h io_manager.cpp
    mpi_manager.h mpi_manager_impl.h mpi_manager.cpp
    simulation_manager.h simulation_manager.cpp
    connection_manager.h connection_manager_impl.h connection_manager.cpp
    sp_manager.h sp_manager_impl.h sp_manager.cpp
    delay_checker.h delay_checker.cpp
    rng_manager.h rng_manager.cpp
    event_delivery_manager.h event_delivery_manager_impl.h
    event_delivery_manager.cpp
    node_manager.h node_manager.cpp
    logging_manager.h logging_manager.cpp
    manager_interface.h
    )

add_library( nestkernel ${nestkernel_sources} )
target_link_libraries( nestkernel
    nestutil random sli_lib
    ${LTDL_LIBRARIES} ${MPI_CXX_LIBRARIES} ${MUSIC_LIBRARIES}
    )

target_include_directories( nestkernel PRIVATE
    ${PROJECT_SOURCE_DIR}/libnestutil
    ${PROJECT_BINARY_DIR}/libnestutil
    ${PROJECT_SOURCE_DIR}/librandom
    ${PROJECT_SOURCE_DIR}/sli
    )

install( TARGETS nestkernel
    LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
    ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR}
    RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
    )

FILTER_HEADERS("${nestkernel_sources}" install_headers )
install( FILES ${install_headers}
    DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/nest)
