CMAKE_MINIMUM_REQUIRED(VERSION 2.8.3)
PROJECT(wave_kinematics)

IF (CMAKE_COMPILER_IS_GNUCXX)
  ADD_DEFINITIONS(-std=gnu++0x)
ENDIF()

# EXTERNAL PACKAGES
FIND_PACKAGE(Kindr)

# INCLUDES
INCLUDE_DIRECTORIES(/usr/include/eigen3)

#LIBRARY
ADD_LIBRARY(
    wave_kinematics
    STATIC
    src/rotation.cpp
    src/quadrotor.cpp
)
SET(
    WAVE_KINEMATICS_TEST_DEPS
    wave_kinematics
    wave_controls
    wave_utils
    gtest
    pthread
)

# UNIT TESTS
SET(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${PROJECT_BINARY_DIR}/tests)
ADD_EXECUTABLE(
    # TARGET
    wave_kinematics_tests
    # TESTS
    tests/rotation_test.cpp
    tests/quadrotor_test.cpp
    # TEST RUNNER
    tests/test_runner.cpp
)
TARGET_LINK_LIBRARIES(wave_kinematics_tests ${WAVE_KINEMATICS_TEST_DEPS})