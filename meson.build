project('cxxplot', 'cpp', version: '0.3.1', default_options: ['cpp_std=c++20'])

cxxplot_not_subproject = meson.is_subproject()

if get_option('def_library') == 'both'
  error('Cxxplot can only be built as a shared or a static library, not both at the same time. Choose shared or static with the default_library meson option.')
endif

cxxplot_compile_with_opengl = get_option('opengl')

if cxxplot_compile_with_opengl
  qt_modules = ['Core', 'Widgets', 'Gui', 'PrintSupport', 'OpenGL']
  opengl_dep = dependency('gl')
else
  qt_modules = ['Core', 'Widgets', 'Gui', 'PrintSupport']
endif

qt_dep = dependency('qt6', modules: qt_modules, required: false)
if not qt_dep.found()
  qt_dep = dependency('qt5', modules: qt_modules)
endif

dependencies = [qt_dep, dependency('threads')]

cxxplot_dir_with_version = 'cxxplot-@0@'.format(meson.project_version())

cxxplot_sources = files(
  'src/align.cpp',
  'src/color.cpp',
  'src/execution.cpp',
  'src/figure.cpp',
  'src/graph.cpp',
  'src/image.cpp',
  'src/qcustomplot.cpp',
  'src/range.cpp',
  'src/styles.cpp',
  'src/utils.cpp',
  'src/widget.cpp',
  'src/window.cpp',
  'src/version.cpp'
)

cxxplot_headers = files(
  'src/execution_p.hpp',
  'src/qcustomplot.h',
  'src/styles_p.hpp',
  'src/widget.hpp',
  'include/cxxplot/align.hpp',
  'include/cxxplot/color.hpp',
  'include/cxxplot/concepts.hpp',
  'include/cxxplot/cxxplot',
  'include/cxxplot/execution.hpp',
  'include/cxxplot/figure.hpp',
  'include/cxxplot/image.hpp',
  'include/cxxplot/gettersetter.hpp',
  'include/cxxplot/graph.hpp',
  'include/cxxplot/named_parameter.hpp',
  'include/cxxplot/point2d.hpp',
  'include/cxxplot/range.hpp',
  'include/cxxplot/styles.hpp',
  'include/cxxplot/typetraits.hpp',
  'include/cxxplot/utils.hpp',
  'include/cxxplot/window.hpp'
)

cxxplot = library(
  'cxxplot',
  sources: [cxxplot_sources, cxxplot_headers],
  dependencies: dependencies,
  install: true)

# Installation
install_headers(cxxplot_headers, subdir: cxxplot_dir_with_version + '/cxxplot')

# tests/examples
# if not cxxplot_not_subproject
#   subdir('tests')
#   subdir('examples')
# endif
