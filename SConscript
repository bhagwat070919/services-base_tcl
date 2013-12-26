# Copyright (c) 2013, AllSeen Alliance. All rights reserved.
#
#    Permission to use, copy, modify, and/or distribute this software for any
#    purpose with or without fee is hereby granted, provided that the above
#    copyright notice and this permission notice appear in all copies.
#
#    THE SOFTWARE IS PROVIDED "AS IS" AND THE AUTHOR DISCLAIMS ALL WARRANTIES
#    WITH REGARD TO THIS SOFTWARE INCLUDING ALL IMPLIED WARRANTIES OF
#    MERCHANTABILITY AND FITNESS. IN NO EVENT SHALL THE AUTHOR BE LIABLE FOR
#    ANY SPECIAL, DIRECT, INDIRECT, OR CONSEQUENTIAL DAMAGES OR ANY DAMAGES
#    WHATSOEVER RESULTING FROM LOSS OF USE, DATA OR PROFITS, WHETHER IN AN
#    ACTION OF CONTRACT, NEGLIGENCE OR OTHER TORTIOUS ACTION, ARISING OUT OF
#    OR IN CONNECTION WITH THE USE OR PERFORMANCE OF THIS SOFTWARE.

import os

Import('env')

env['_ALLJOYN_SERVER_SAMPLE_'] = True

build_all = ARGUMENTS.get('ALL', 0)
if 'java' in env['bindings'] :
    build_all = 1

if int(build_all):
    build_config       = 1
    build_notification = 1
    build_cps          = 1
    build_onboarding   = 1
else:
    build_config       = int(ARGUMENTS.get('CONFIG',       0))
    build_notification = int(ARGUMENTS.get('NOTIFICATION', 0))
    build_cps          = int(ARGUMENTS.get('CPS',          0))
    build_onboarding   = int(ARGUMENTS.get('ONBOARDING',   0))

if not env.has_key('_ALLJOYN_ABOUT_') and os.path.exists('../../core/alljoyn/services/about/SConscript'):
    env.SConscript('../../core/alljoyn/services/about/SConscript')

if not env.has_key('_ALLJOYN_SERVICES_COMMON_') and os.path.exists('../../services/services_common/SConscript'):
    env.SConscript('../../services/services_common/SConscript')

if build_config:
    env.Append(CPPDEFINES = '_CONFIG_')
    if not env.has_key('_ALLJOYN_CONFIG_') and os.path.exists('../../services/config/SConscript'):
        env.SConscript('../../services/config/SConscript')

if build_notification:
    env.Append(CPPDEFINES = '_NOTIFICATION_')
    if not env.has_key('_ALLJOYN_NOTIFICATION_') and os.path.exists('../../services/notification/SConscript'):
        env.SConscript('../../services/notification/SConscript')

if build_cps:
    env.Append(CPPDEFINES = '_CONTROLPANEL_')
    if not env.has_key('_ALLJOYN_CONTROLPANEL_') and os.path.exists('../../services/controlpanel/SConscript'):
        env.SConscript('../../services/controlpanel/SConscript')

if build_onboarding:
    env.Append(CPPDEFINES = '_ONBOARDING_')
    if not env.has_key('_ALLJOYN_ONBOARDING_') and os.path.exists('../../services/onboarding/SConscript'):
        env.SConscript('../../services/onboarding/SConscript')

if 'cpp' in env['bindings'] and not env.has_key('_ALLJOYNCORE_') and os.path.exists('../../core/alljoyn/alljoyn_core/SConscript'):
    env.SConscript('../../core/alljoyn/alljoyn_core/SConscript')

if 'java' in env['bindings'] and not env.has_key('_ALLJOYN_JAVA_') and os.path.exists('../../core/alljoyn/alljoyn_java/SConscript'):
    env.SConscript('../../core/alljoyn/alljoyn_java/SConscript')

server_sample_env = env.Clone()

for b in server_sample_env['bindings']:
    if os.path.exists('%s/SConscript' % b):
        server_sample_env.VariantDir('$OBJDIR/%s' % b, b, duplicate = 0)

server_sample_env.SConscript(['$OBJDIR/%s/SConscript' % b for b in env['bindings'] if os.path.exists('%s/SConscript' % b) ],
                   exports = ['server_sample_env'])