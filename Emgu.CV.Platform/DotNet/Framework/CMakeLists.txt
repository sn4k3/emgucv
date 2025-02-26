# --------------------------------------------------------
#  Copyright (C) 2004-2022 by EMGU Corporation. All rights reserved.
# --------------------------------------------------------

IF((EMGU_CV_BUILD OR EMGU_CV_EXAMPLE_BUILD) AND NOT ANDROID AND NOT NETFX_CORE AND NOT APPLE)
  
  IF(WIN32)
    PROJECT(Emgu.CV.Platform.NetFramework)
    
    SET(EXTRA_BUILD_FLAGS "/p:Platform=\"Any CPU\"")

    MSBUILD_CSPROJ_IN_SOLUTION(${PROJECT_NAME} "${CMAKE_CURRENT_SOURCE_DIR}/../../../Solution/Windows.Desktop/Emgu.CV.Example.sln" "Emgu.CV.Platform.NetFramework" "${EXTRA_BUILD_FLAGS}" ALL)	

    IF (EMGU_SIGN_FOUND)
      EMGU_SIGN_BINARY(${PROJECT_NAME} ${LIBRARY_OUTPUT_PATH}/${PROJECT_NAME}.dll)
    ENDIF()

    INSTALL(
      FILES 
      ${LIBRARY_OUTPUT_PATH}/${PROJECT_NAME}.xml
      ${LIBRARY_OUTPUT_PATH}/${PROJECT_NAME}.dll 
      DESTINATION ${CPACK_PACKAGE_CLI_FOLDER}
      COMPONENT emgucv_binary)
    
    if(ENABLE_SOLUTION_FOLDERS)
      set_target_properties(${PROJECT_NAME} PROPERTIES FOLDER "emgu")
    endif()
    
    ADD_DEPENDENCIES(${PROJECT_NAME} cvextern Emgu.CV.Bitmap)

  ENDIF()
  
ENDIF()
