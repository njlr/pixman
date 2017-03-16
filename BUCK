def merge_dicts(x, y):
  z = x.copy()
  z.update(y)
  return z

PIXMAN_VERSION_H = """
#ifndef PIXMAN_VERSION_H__
#define PIXMAN_VERSION_H__

//#ifndef PIXMAN_H__
//#  error pixman-version.h should only be included by pixman.h
//#endif

#define PIXMAN_VERSION_MAJOR 0
#define PIXMAN_VERSION_MINOR 34
#define PIXMAN_VERSION_MICRO 0

#define PIXMAN_VERSION_STRING \\"0.34.0\\"

#define PIXMAN_VERSION_ENCODE(major, minor, micro) (	\
	  ((major) * 10000)				\
	+ ((minor) *   100)				\
	+ ((micro) *     1))

#define PIXMAN_VERSION PIXMAN_VERSION_ENCODE(	\
	PIXMAN_VERSION_MAJOR,			\
	PIXMAN_VERSION_MINOR,			\
	PIXMAN_VERSION_MICRO)

#endif /* PIXMAN_VERSION_H__ */
"""

genrule(
  name = 'pixman-version.h',
  out = 'pixman-version.h',
  cmd = 'echo "' + PIXMAN_VERSION_H + '" > $OUT',
)

macos_flags = [
  '-DHAVE_PTHREADS',
  '-DTLS=__thread',
]

linux_flags = [
  '-DHAVE_PTHREADS',
  '-DTLS=__thread',
]

cxx_library(
  name = 'pixman',
  header_namespace = '',
  exported_headers = merge_dicts(subdir_glob([
    ('pixman', 'pixman.h'),
    ('pixman', 'pixman-private.h'),
    ('pixman', 'pixman-compiler.h'),
  ]), {
    'pixman-version.h': ':pixman-version.h',
  }),
  srcs = [
    'pixman/pixman-access-accessors.c',
    'pixman/pixman-access.c',
    'pixman/pixman-combine-float.c',
    'pixman/pixman-combine32.c',
    'pixman/pixman-edge-accessors.c',
    'pixman/pixman-edge.c',
    'pixman/pixman-fast-path.c',
    'pixman/pixman-filter.c',
    'pixman/pixman-general.c',
    'pixman/pixman-glyph.c',
    'pixman/pixman-gradient-walker.c',
    'pixman/pixman-image.c',
    'pixman/pixman-implementation.c',
    'pixman/pixman-linear-gradient.c',
    'pixman/pixman-matrix.c',
    'pixman/pixman-mmx.c',
    'pixman/pixman-noop.c',
    'pixman/pixman-ppc.c',
    'pixman/pixman-region16.c',
    'pixman/pixman-region32.c',
    'pixman/pixman-solid-fill.c',
    'pixman/pixman-timer.c',
    'pixman/pixman-trap.c',
    'pixman/pixman-utils.c',
    'pixman/pixman-x86.c',
  ],
  compiler_flags = [
    '-std=c11',
    '-DPACKAGE=pixman',
  ],
  platform_compiler_flags = [
    ('default', macos_flags),
    ('^macos.*', macos_flags),
    ('^linux.*', linux_flags),
  ],
  visibility = [
    'PUBLIC',
  ],
)
