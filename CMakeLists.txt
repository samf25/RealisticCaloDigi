########################################################
# cmake file for building Gaudi Calo Digi/Reco Package
# @author Samuel Ferraro
########################################################

# sources
FILE( GLOB _plugin_sources src/*.cc )
gaudi_add_module(RealisticCaloDigiK4FWCPlugins
		SOURCES ${_plugin_sources}
		LINK k4FWCore::k4FWCore
			Gaudi::GaudiKernel
			EDM4HEP::edm4hep
			${ROOT_LIBRARIES}
            ${CLHEP_LIBRARIES}
			DD4hep::DDCore)

INSTALL( TARGETS RealisticCaloDigiK4FWCPlugins 
	EXPORT ${CMAKE_PROJECT_NAME}Targets
	RUNTIME DESTINATION "${CMAKE_INSTALL_BINDIR}" COMPONENT bin 
	LIBRARY DESTINATION "${CMAKE_INSTALL_LIBDIR}" COMPONENT shlib
	PUBLIC_HEADER DESTINATION "${CMAKE_INSTALL_INCLUDEDIR}/@{CMAKE_PROJECT_NAME}"
	COMPONENT dev )

TARGET_INCLUDE_DIRECTORIES(RealisticCaloDigiK4FWCPlugins
		PRIVATE	./include
			${CMAKE_CURRENT_BINARY_DIR}
    		${Gaudi_INCLUDE_DIRS}
			${ROOT_INCLUDE_DIRS}
			${DD4hep_INCLUDE_DIRS})

SET( GAUDI_GENCONF_DIR "genConfDir" )
if (${Gaudi_VERSION} VERSION_LESS 35.1)
	SET( GAUDI_GENCONF_DIR "genConf" )
endif()
