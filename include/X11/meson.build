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

include_path = join_paths(get_option('includedir'), 'X11')

configure_file(
  input : 'Xfuncproto.h.meson',
  output : '@BASENAME@',
  configuration : config,
  install : true,
  install_dir : include_path
)

configure_file(
  input : 'Xpoll.h.in',
  output : '@BASENAME@',
  configuration : config,
  install : true,
  install_dir : include_path
)

install_headers(
  'ap_keysym.h', 'DECkeysym.h', 'HPkeysym.h', 'keysymdef.h', 'keysym.h',
  'Sunkeysym.h', 'Xalloca.h', 'Xarch.h', 'Xatom.h', 'Xdefs.h', 'XF86keysym.h',
  'Xfuncs.h', 'X.h', 'Xmd.h', 'Xosdefs.h', 'Xos.h', 'Xos_r.h', 'Xproto.h',
  'Xprotostr.h', 'Xthreads.h', 'Xw32defs.h', 'XWDFile.h', 'Xwindows.h',
  'Xwinsock.h',
  subdir : 'X11',
)
