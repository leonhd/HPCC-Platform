################################################################################
#    HPCC SYSTEMS software Copyright (C) 2012 HPCC Systems®.
#
#    Licensed under the Apache License, Version 2.0 (the "License");
#    you may not use this file except in compliance with the License.
#    You may obtain a copy of the License at
#
#       http://www.apache.org/licenses/LICENSE-2.0
#
#    Unless required by applicable law or agreed to in writing, software
#    distributed under the License is distributed on an "AS IS" BASIS,
#    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
#    See the License for the specific language governing permissions and
#    limitations under the License.
################################################################################

# Component: zcrypt 

#####################################################
# Description:
# ------------
#    Cmake Input File for zcrypt
#####################################################


project( zcrypt ) 

SET(CMAKE_UNITY_BUILD FALSE)

set ( SRCS
      aes.cpp
      base64.cpp
      mutex.cpp
      ioapi.c
      zip.c
      unzip.c
      zcrypt.cpp
    )

IF (WIN32)
  set ( SRCS ${SRCS} iowin32.c )
ENDIF()

include_directories ( 
         ${ZLIB_INCLUDE_DIR}
         ${OPENSSL_INCLUDE_DIR}
         ./../../include 
         ./../../jlib
    )

ADD_DEFINITIONS ( -D_USRDLL -DZCRYPT_EXPORTS )

HPCC_ADD_LIBRARY( zcrypt SHARED ${SRCS} )
install ( TARGETS zcrypt RUNTIME DESTINATION ${EXEC_DIR} LIBRARY DESTINATION ${LIB_DIR} )
target_link_libraries ( zcrypt
         jlib
         ${ZLIB_LIBRARIES} 
         ${OPENSSL_LIBRARIES} 
    )


