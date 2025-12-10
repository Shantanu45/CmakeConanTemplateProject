set(TEST_PROJECT_NAME Test)

set(UNGROUPED_FILES
	"main.cpp"
)

source_group("" FILES ${UNGROUPED_FILES})

set(TESTS
	"SampleTest.cpp"
)

source_group("tests" FILES ${TESTS})

find_package(GTest REQUIRED)
# For Windows: Prevent overriding the parent project's compiler/linker settings
set(gtest_force_shared_crt ON CACHE BOOL "" FORCE)

set(ALL_FILES
	${UNGROUPED_FILES}
	${TESTS}
)

add_executable(${TEST_PROJECT_NAME}
	${ALL_FILES}
)

setup_msvc_options(${TEST_PROJECT_NAME})

set(TEST_INCLUDE 
"${PROJECT_SOURCE_DIR}/src"
)

target_include_directories(${TEST_PROJECT_NAME} PRIVATE ${TEST_INCLUDE})

# Link
set(ADDITIONAL_LIBRARY_DEPENDENCIES
	gtest::gtest
	spdlog::spdlog
)

target_link_libraries(${TEST_PROJECT_NAME} PUBLIC ${ADDITIONAL_LIBRARY_DEPENDENCIES})

