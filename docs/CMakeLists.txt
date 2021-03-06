FIND_PACKAGE(Sphinx REQUIRED)

IF(NOT DEFINED SPHINX_THEME)
    SET(SPHINX_THEME nature)
ENDIF(NOT DEFINED SPHINX_THEME)

IF(NOT DEFINED SPHINX_THEME_DIR)
    SET(SPHINX_THEME_DIR)
ENDIF(NOT DEFINED SPHINX_THEME_DIR)

SET(BINARY_BUILD_DIR "${CMAKE_CURRENT_BINARY_DIR}/_build")
SET(BINARY_CACHE_DIR "${CMAKE_CURRENT_BINARY_DIR}/_doctrees")
SET(SPHINX_HTML_DIR "${CMAKE_CURRENT_BINARY_DIR}/html")

CONFIGURE_FILE(
    "${CMAKE_CURRENT_SOURCE_DIR}/conf.py.in"
    "${BINARY_BUILD_DIR}/conf.py"
    @ONLY)

ADD_CUSTOM_TARGET(PBNJDoc ALL
    ${SPHINX_EXECUTABLE}
        -q -b html
        -c "${BINARY_BUILD_DIR}"
        -d "${BINARY_CACHE_DIR}"
        "${CMAKE_CURRENT_SOURCE_DIR}"
        "${SPHINX_HTML_DIR}"
    COMMENT "Building documentation with Sphinx")
