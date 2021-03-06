PROJECT(wave_utils)

# LIBRARY
WAVE_ADD_LIBRARY(${PROJECT_NAME}
    src/config.cpp
    src/data.cpp
    src/file.cpp
    src/math.cpp
    src/time.cpp)

# Use these headers when building, and make clients use them
WAVE_INCLUDE_DIRECTORIES(${PROJECT_NAME} PUBLIC include)

# Depend on these modules and external libraries, and make clients use them
TARGET_LINK_LIBRARIES(${PROJECT_NAME} PUBLIC
    Eigen3::Eigen
    yaml-cpp
    opencv_core)

# UNIT TESTS
WAVE_ADD_TEST(
    ${PROJECT_NAME}_tests
    tests/utils/config_test.cpp
    tests/utils/data_test.cpp
    tests/utils/file_test.cpp
    tests/utils/math_test.cpp
    tests/utils/time_test.cpp
)
TARGET_LINK_LIBRARIES(
    ${PROJECT_NAME}_tests
    ${PROJECT_NAME}
)

# COPY TEST DATA
FILE(COPY tests/data DESTINATION ${PROJECT_BINARY_DIR}/tests)
