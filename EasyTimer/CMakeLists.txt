# CMakeList.txt: EasyTimer에 대한 CMake 프로젝트, 여기에 소스를 포함하고
# 프로젝트 특정 논리를 정의합니다.
#
cmake_minimum_required (VERSION 3.8)
project(EasyTimer)


SET(CMAKE_EXE_LINKER_FLAGS "-static")

message("Boost_LIBRARY_DIRS" ${Boost_LIBRARY_DIRS} )


message("MSVC_VERSION : " ${MSVC_VERSION})
if (MSVC_VERSION GREATER_EQUAL "1900")
    include(CheckCXXCompilerFlag)
    CHECK_CXX_COMPILER_FLAG("/std:c++latest" _cpp_latest_flag_supported)
    if (_cpp_latest_flag_supported)
        add_compile_options("/std:c++latest")
        message("CMAKE_CXX_COMPILER_VERSION :" ${CMAKE_CXX_COMPILER_VERSION} )
    endif()
endif()


if (WIN32)
	set(BOOST_LIBRARIES ${Boost_LIBRARY_DIRS}/boost_system-vc140-mt.lib)
	if (CMAKE_BUILD_TYPE MATCHES "Debug")
		set(BOOST_LIBRARIES ${Boost_LIBRARY_DIRS}/../debug/lib/boost_system-vc140-mt-gd.lib)
        set(BOOST_LIBRARIES ${Boost_LIBRARY_DIRS}/../debug/lib/boost_date_time-vc140-mt-gd.lib)
	endif()
endif()

find_package(Boost 1.17.0)
find_path(BOOST_INCLUDE_DIR boost)

include_directories(
${BOOST_INCLUDE_DIR}
		)


# 이 프로젝트의 실행 파일에 소스를 추가합니다.
add_executable (EasyTimer 
                EasyTimer.cpp 
                Countdown.h
                Date.h
                ElapsedTimer.h
                Scheduling.h
                ScopeTimer.h
                Stopwatch.h
                Times.h
                )

# TODO: 필요한 경우 테스트를 추가하고 대상을 설치합니다.
