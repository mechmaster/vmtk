set(VTK_VMTK_RENDERING_TARGET_LINK_LIBRARIES )

if( ${VTK_VERSION_MAJOR} GREATER 6 )
  set( VTK_VMTK_RENDERING_COMPONENTS
    vtkCommonCore
    vtkInteractionWidgets
    vtkRenderingOpenGL2
    )
  if (VTK_WRAP_PYTHON AND VTK_VMTK_WRAP_PYTHON)
    list(APPEND VTK_VMTK_RENDERING_COMPONENTS
      vtkWrappingPythonCore
      )
  endif(VTK_WRAP_PYTHON AND VTK_VMTK_WRAP_PYTHON)
  find_package( VTK ${VTK_VERSION_MAJOR}.${VTK_VERSION_MINOR} COMPONENTS ${VTK_VMTK_RENDERING_COMPONENTS} REQUIRED )
  include( ${VTK_USE_FILE} )
  list( APPEND VTK_VMTK_RENDERING_TARGET_LINK_LIBRARIES ${VTK_LIBRARIES} )
elseif( ${VTK_VERSION_MAJOR} GREATER 5 )
  set( VTK_VMTK_RENDERING_COMPONENTS
    vtkCommonCore
    vtkInteractionWidgets
    vtkRenderingOpenGL
    )
  if (VTK_WRAP_PYTHON AND VTK_VMTK_WRAP_PYTHON)
    list(APPEND VTK_VMTK_RENDERING_COMPONENTS
      vtkWrappingPythonCore
      )
  endif(VTK_WRAP_PYTHON AND VTK_VMTK_WRAP_PYTHON)
  find_package( VTK ${VTK_VERSION_MAJOR}.${VTK_VERSION_MINOR} COMPONENTS ${VTK_VMTK_RENDERING_COMPONENTS} REQUIRED )
  include( ${VTK_USE_FILE} )
  list( APPEND VTK_VMTK_RENDERING_TARGET_LINK_LIBRARIES ${VTK_LIBRARIES} )
else( ${VTK_VERSION_MAJOR} GREATER 6 )
  list( APPEND VTK_VMTK_RENDERING_TARGET_LINK_LIBRARIES
    vtkCommon
    vtkFiltering
    vtkGraphics
    vtkHybrid
    vtkRendering
    vtkWidgets
    )
endif( ${VTK_VERSION_MAJOR} GREATER 6 )

SET (VTK_VMTK_RENDERING_SRCS
  vtkvmtkImagePlaneWidget.cxx
  vtkvmtkInteractorStyleTrackballCamera.cxx
  )

vmtk_build_library(
  NAME Rendering
  SRCS ${VTK_VMTK_RENDERING_SRCS}
  TARGET_LINK_LIBRARIES ${VTK_VMTK_RENDERING_TARGET_LINK_LIBRARIES}
  )
