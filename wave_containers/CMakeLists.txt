PROJECT(wave_containers)

# Define a header-only library
WAVE_ADD_LIBRARY(${PROJECT_NAME})
WAVE_INCLUDE_DIRECTORIES(${PROJECT_NAME} INTERFACE include)
TARGET_LINK_LIBRARIES(${PROJECT_NAME} INTERFACE
    Eigen3::Eigen
    Boost::boost)

# UNIT TESTS
WAVE_ADD_TEST(${PROJECT_NAME}_tests
    tests/measurement_test.cpp
    tests/landmark_measurement_test.cpp)

TARGET_LINK_LIBRARIES(${PROJECT_NAME}_tests ${PROJECT_NAME})

IF(BUILD_BENCHMARKS)
    WAVE_ADD_BENCHMARK(${PROJECT_NAME}_benchmark
        tests/measurement_container_benchmark.cpp)
    TARGET_LINK_LIBRARIES(${PROJECT_NAME}_benchmark ${PROJECT_NAME})
ENDIF(BUILD_BENCHMARKS)