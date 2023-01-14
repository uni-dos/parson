project('parson', 'c',
    version : '1.5.0',
    license : 'MIT',
    meson_version : '>=0.47.0',
    default_options : [
        'c_std=c89', 'optimization=2', 
        'warning_level=2'
        ]
)

parson_inc = include_directories('.')

# defaults to a shared lib; 
# pass default_library=static for a static build
lib_parson = library(
    meson.project_name(),
    sources: 'parson.c',
    include_directories: [parson_inc],
    install: not meson.is_subproject()
)

header = files('parson.h')
if not meson.is_subproject()
    install_headers(header, subdir : 'parson')
endif

# https://github.com/mesonbuild/meson/issues/2546
# needed to have parson/parson.h when used as a subproject
# it is just preference
# but if not interested, remove
# subdir(s) in pkgconfig, install_headers and below
if meson.is_subproject()
    subdir('parson')
endif

parson = declare_dependency(
    include_directories : parson_inc,
    link_with : lib_parson
)

if not meson.is_subproject()
    pkgconfig = import('pkgconfig')
    pkgconfig.generate(
        libraries: lib_parson,
        version: meson.project_version(),
        name: meson.project_name(),
        subdirs: 'parson',
        description: 'Lightweight JSON library written in C.')
endif

