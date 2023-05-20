project(
  'cxxplot', 'cpp',
  version: '0.3.2',
  default_options: ['cpp_std=c++20']
)

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

qt = import('qt6', required: false)
qt_dep = dependency('qt6', modules: qt_modules, required: false)
if not qt_dep.found()
  qt = import('qt5')
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

cxxplot_qrcs = files(
  'src/images.qrc'
)

cxxplot_moc_headers = files(
  'src/execution_p.hpp',
  'src/qcustomplot.h',
  'src/widget.hpp',
  'include/cxxplot/graph.hpp',
  'include/cxxplot/window.hpp'
)

cxxplot_headers = files(
  'src/execution_p.hpp',
  'src/qcustomplot.h',
  'src/styles_p.hpp',
  'src/widget.hpp',
  'include/cxxplot/align.hpp',
  'include/cxxplot/color.hpp',
  'include/cxxplot/concepts.hpp',
  'include/cxxplot/cxxplot.hpp',
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

cxxplot_moc_sources = qt.compile_moc(
  headers : cxxplot_moc_headers,
  include_directories: include_directories('include', 'src'),
  dependencies: qt_dep
)

cxxplot_resources = qt.compile_resources(
  sources : cxxplot_qrcs
)

cxxplot = library(
  'cxxplot',
  sources: [cxxplot_sources, cxxplot_headers, cxxplot_moc_sources, cxxplot_resources],
  include_directories: include_directories('include', 'src'),
  dependencies: dependencies,
  install: true,
  cpp_args : ['-DCXXPLOT_VERSION="@0@"'.format(meson.project_version())]
)

cxxplot_dep = declare_dependency(
  link_with: cxxplot,
  include_directories: include_directories('include', is_system: get_option('is_system')),
  dependencies: dependencies
)

# Installation
install_headers(cxxplot_headers, subdir: cxxplot_dir_with_version + '/cxxplot')

message('Is system: @0@'.format(get_option('is_system')))
# tests/examples
# if not cxxplot_not_subproject
#   subdir('tests')
#   subdir('examples')
# endif
