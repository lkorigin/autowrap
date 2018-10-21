project('Autowrap', 'd',
    meson_version: '>=0.46',
    license: 'BSD-3-Clause',
    version: '0.1.4'
)
add_languages('c')

project_soversion = '0'

aw_reflect_src_dir = include_directories('reflection/source/')
aw_py_src_dir = include_directories('python/source/')

pkgc = import('pkgconfig')
pyd_dep = dependency('pyd')

aw_reflection_src = [
    'reflection/source/autowrap/reflection.d'
]

aw_py_src = [
    'python/source/autowrap/python/boilerplate.d',
    'python/source/autowrap/python/package.d',
    'python/source/autowrap/python/pyd/class_wrap.d',
    'python/source/autowrap/python/pyd/package.d',
    'python/source/autowrap/python/wrap.d',

    'python/source/autowrap/python/druntime.c'
]

install_subdir('reflection/source/autowrap/', install_dir: 'include/d/autowrap/')
install_subdir('python/source/autowrap/',     install_dir: 'include/d/autowrap/')

aw_py_lib = library('autowrap-python',
        [aw_py_src, aw_reflection_src],
        include_directories: [aw_reflect_src_dir, aw_py_src_dir],
        dependencies: [pyd_dep],
        install: true,
        version: meson.project_version(),
        soversion: project_soversion,
)
pkgc.generate(name: 'autowrap-python',
              libraries: aw_py_lib,
              subdirs: 'd/autowrap/',
              version: meson.project_version(),
              description: 'Wrap existing D code for use in Python.'
)
