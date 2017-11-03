# Copyright © 2017 Dylan Baker
# Copyright © 2017 Intel Corporation

# Permission is hereby granted, free of charge, to any person obtaining a copy
# of this software and associated documentation files (the "Software"), to deal
# in the Software without restriction, including without limitation the rights
# to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
# copies of the Software, and to permit persons to whom the Software is
# furnished to do so, subject to the following conditions:

# The above copyright notice and this permission notice shall be included in
# all copies or substantial portions of the Software.

# THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
# IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
# FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
# AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
# LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
# OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
# SOFTWARE.

project('xproto', 'c', license : 'MIT', version : '7.0.32-devel')

config = configuration_data()

cc = meson.get_compiler('c')

# XXX: is this the right way to detect mingw? what about cygwin?
if host_machine.system() == 'windows' and cc.get_id() != 'msvc'
  config.set('USE_FDS_BITS', true)
else
  fds_test_args = []
  if cc.has_header('sys/select.h')
    fds_test_args += '-DHAVE_SYS_SELECT_H'
  endif
  if cc.has_header('sys/param.h')
    fds_test_args += '-DHAVE_SYS_PARAM_H'
  endif
  if cc.has_header('sys/types.h')
    fds_test_args += '-DHAVE_SYS_TYPES_H'
  endif
  if cc.has_header('sys/time.h')
    fds_test_args += '-DHAVE_SYS_TIME_H'
  endif

  code = '''
  #ifdef HAVE_SYS_PARAM_H
  #include <sys/param.h>
  #endif
  #ifdef HAVE_SYS_TYPES_H
  #include <sys/types.h>
  #endif
  #ifdef HAVE_SYS_TIME_H
  #include <sys/time.h>
  #endif
  #ifdef HAVE_SYS_SELECT_H
  #include <sys/select.h>
  #endif
  '''

  if cc.has_member('fd_set', 'fds_bits', prefix : code, args : fds_test_args)
    config.set('USE_FDS_BITS', 'fds_bits')
  elif cc.has_member('fd_set', '__fds_bits', prefix : code, args : fds_test_args)
    config.set('USE_FDS_BITS', '__fds_bits')
  else
    error('''
      Could not determine how to access the fds_bits or equivalent'
      structure in fd_set on your platoform
    ''')
  endif
endif

_varproto = get_option('varargs-prototypes')
if _varproto == 'true'
  with_varproto = true
elif _varproto == 'false'
  with_varproto = false
else
  with_varproto = not ['darwin', 'windows'].contains(host_machine.system())
endif

_nestedproto = get_option('nested-prototypes')
if _nestedproto == 'true'
  with_nestedproto = true
elif _nestedproto == 'false'
  with_nestedproto = false
else
  with_nestedproto = not ['darwin', 'windows'].contains(host_machine.system())
endif

_constproto = get_option('const-prototypes')
if _constproto == 'true'
  with_constproto = true
elif _constproto == 'false'
  with_constproto = false
else
  with_constproto = not ['darwin', 'windows'].contains(host_machine.system())
endif

_funcproto = get_option('function-prototypes')
if _funcproto == 'true'
  with_funcproto = true
elif _funcproto == 'false'
  with_funcproto = false
else
  if ['bsd', 'linux'].contains(host_machine.system())
    with_funcproto = true
  else
    with_funcproto = with_varproto and with_nestedproto
  endif
endif

if with_varproto and with_funcproto and with_nestedproto and with_constproto
  config.set('FUNCPROTO', 15)
elif with_funcproto and with_varproto and with_nestedproto
  config.set('FUNCPROTO', 11)
elif with_funcproto and with_nestedproto
  config.set('FUNCPROTO', 9)
elif with_funcproto and with_varproto and with_constproto
  config.set('FUNCPROTO', 7)
elif with_funcproto and with_nestedproto
  config.set('FUNCPROTO', 5)
elif with_funcproto and with_varproto
  config.set('FUNCPROTO', 3)
elif with_funcproto
  config.set('FUNCPROTO', false)  # XXX: is this correct?
endif

_wideproto = get_option('wide-prototypes')
if _wideproto == 'true'
  config.set('NARROWPROTO', true)
elif _wideproto == 'false'
  config.set('NARROWPROTO', false)
else
  config.set('NARROWPROTO', ['linux', 'bsd'].contains(host_machine.system()))
endif

pkg = import('pkgconfig')
pkg.generate(
  name : 'Xproto',
  filebase : 'xproto',
  description : 'Xproto headers',
  version : meson.project_version(),
)

subdir('include/X11')

ext_xproto = declare_dependency(
  include_directories : include_directories('include'),
)
