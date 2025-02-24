cmake_minimum_required(VERSION 2.1)
project(MyProject)

# 设置编译选项以生成覆盖率信息
set(CMAKE_CXX_COMPILER /usr/bin/g++)
if(CMAKE_CXX_COMPILER_ID MATCHES "GNU|Clang|g")
message(CMAKE_CXX_COMPILER_ID, $CMAKE_CXX_COMPILER_ID)
# 添加目标以生成覆盖率报告
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} --coverage")
    set(CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS} --coverage")
endif()

# 添加源文件
set(SOURCES
    src/main.cpp
#    src/example.cpp
)

# 创建可执行文件
add_executable(MyProject ${SOURCES})

# 添加测试
enable_testing()
#add_subdirectory(tests)
message(CMAKE_CXX_COMPILER_ID, $CMAKE_CXX_COMPILER_ID)
# 添加目标以生成覆盖率报告
if(CMAKE_CXX_COMPILER_ID MATCHES "GNU|Clang|g")
message(CMAKE_CXX_COMPILER_ID, $CMAKE_CXX_COMPILER_ID)
# 添加目标以生成覆盖率报告
    find_program(LCOV lcov)
    find_program(GENHTML genhtml)

    if(LCOV AND GENHTML)
message(CMAKE_CXX_COMPILER_ID, $CMAKE_CXX_COMPILER_ID)
        add_custom_target(coverage3
            COMMAND ${LCOV} --directory . --capture --output-file coverage.info
            #COMMAND ${LCOV} --remove coverage.info '/usr/*' 'tests/*' --output-file coverage.info
            COMMAND ${GENHTML} --demangle-cpp --legend --title "Coverage Report" --output-directory coverage coverage.info
            WORKING_DIRECTORY ${CMAKE_BINARY_DIR}
            COMMENT "Generating coverage report"
        )
message(WORKING_DIRECTORY , ${CMAKE_BINARY_DIR})
    endif()
endif()
