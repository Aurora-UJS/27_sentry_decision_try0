cmake_minimum_required(VERSION 3.22)
# TODO: 新建项目时修改这里的名称
project(RoboModule CXX)

# --- 1. 全局 C++ 标准设置 ---
set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON) # 必须开启，给 clangd 提供代码补全语义

# --- 2. 编译器优化：自动启用 LLD 链接器 ---
if(CMAKE_CXX_COMPILER_ID MATCHES "Clang")
    add_link_options("-fuse-ld=lld")
    message(STATUS "⚡ Enabled LLD linker for Clang")
endif()

# --- 3. 自动化基建：无感安装 pre-commit ---
find_program(PRE_COMMIT_EXECUTABLE pre-commit)
if(PRE_COMMIT_EXECUTABLE)
    execute_process(
        COMMAND ${PRE_COMMIT_EXECUTABLE} install
        WORKING_DIRECTORY ${CMAKE_SOURCE_DIR}
        OUTPUT_QUIET
        RESULT_VARIABLE PRE_COMMIT_RES
    )
    if(PRE_COMMIT_RES EQUAL 0)
        message(STATUS "🛡️ pre-commit hooks are active.")
    endif()
else()
    message(WARNING "⚠️ pre-commit not found! Code style checks bypassed.")
endif()

# --- 4. 引入 Conan 依赖 ---
# Conan 2.0 推荐的集成方式，如果在环境中找到了依赖就链接
find_package(fmt QUIET)
find_package(spdlog QUIET)

# --- 5. 编译目标 ---
add_executable(${PROJECT_NAME} src/main.cpp)

# 如果使用了 Conan 下载的库，则进行链接
if(fmt_FOUND AND spdlog_FOUND)
    target_link_libraries(${PROJECT_NAME} PRIVATE fmt::fmt spdlog::spdlog)
endif()