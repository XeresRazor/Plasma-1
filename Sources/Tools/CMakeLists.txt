find_package(Qt5Core)
set_package_properties(Qt5Core PROPERTIES
    URL "http://www.qt.io/"
    DESCRIPTION "Cross-platform GUI framework for C++"
    TYPE OPTIONAL
    PURPOSE "Required for building GUI tools for Plasma"
)

find_package(Qt5Widgets)
set_package_properties(Qt5Widgets PROPERTIES
    URL "http://www.qt.io/"
    DESCRIPTION "Cross-platform GUI framework for C++"
    TYPE OPTIONAL
    PURPOSE "Required for building GUI tools for Plasma"
)

if(Qt5Core_FOUND AND Qt5Widgets_FOUND)
    set(Qt5_LIBS_FOUND 1)
else()
    set(Qt5_LIBS_FOUND 0)
endif()

if(PLASMA_BUILD_TOOLS)
    if(Qt5_LIBS_FOUND)
        add_subdirectory(plLocalizationEditor)
        add_subdirectory(plResBrowser)

        add_dependencies(tools
            plLocalizationEditor
            plResBrowser
        )
    endif()

    if(WIN32)
        add_subdirectory(plShaderAssembler)
        add_dependencies(tools plShaderAssembler)
    endif()

    if(FREETYPE_FOUND AND Qt5_LIBS_FOUND)
        add_subdirectory(plFontConverter)
        add_dependencies(tools plFontConverter)
    endif()
endif()

# Max Stuff goes below here...
if(3dsm_FOUND AND 3dsm_BUILD_PLUGIN)
    add_subdirectory(MaxComponent)
    add_subdirectory(MaxConvert)
    add_subdirectory(MaxExport)
    add_subdirectory(MaxMain)
    add_subdirectory(MaxPlasmaLights)
    add_subdirectory(MaxPlasmaMtls)
endif()
