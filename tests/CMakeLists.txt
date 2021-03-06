#   Copyright 2017 Comcast Cable Communications Management, LLC
#
#   Licensed under the Apache License, Version 2.0 (the "License");
#   you may not use this file except in compliance with the License.
#   You may obtain a copy of the License at
#
#       http://www.apache.org/licenses/LICENSE-2.0
#
#   Unless required by applicable law or agreed to in writing, software
#   distributed under the License is distributed on an "AS IS" BASIS,
#   WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
#   See the License for the specific language governing permissions and
#   limitations under the License.

add_test(NAME Simple COMMAND simple)

set (CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -Wall -Wno-error=missing-field-initializers -W -g -fprofile-arcs -ftest-coverage -O0")
set (CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall -W  -g -fprofile-arcs -ftest-coverage -O0")
set (CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS} -fprofile-arcs -ftest-coverage -O0")

#file(GLOB snmpadapter_SRC "../src/*.c" "../src/*.h")
#add_executable(simple simple.c ${snmpadapter_SRC})
add_executable(simple simple.c ../src/snmpadapter_main.c ../src/snmpadapter_parser.c ../src/snmpadapter_get.c ../src/snmpadapter_set.c)
set_property(TARGET simple PROPERTY C_STANDARD 99)
  
target_link_libraries (simple -llibparodus -lwrp-c -lwdmp-c -lmsgpackc -lnanomsg -luuid -lnetsnmp -lcimplog -ltrower-base64 -lrt -lcrypto -lm -lcjson -lpthread)
target_link_libraries (simple gcov)
target_link_libraries (simple cunit)
target_link_libraries (simple rt)
