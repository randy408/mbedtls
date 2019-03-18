project('mbedtls', 'c', license : 'apache', version : '2.14.0')

mbed_inc = include_directories('include', 'configs')

add_project_arguments('-DMBEDTLS_CONFIG_FILE="config-ccm-psk-tls1_2.h"', language : 'c')

cc = meson.get_compiler('c')

mbed_deps = []

if host_machine.system() == 'windows'
    add_project_arguments('-DMBEDTLS_PLATFORM_C', language : 'c')

    mbed_deps += cc.find_library('ws2_32')
endif

#custom_conf get_option('custom')

#if(custom_conf)
#    cdata = configuration_data()

#    cdata.set('

#endif

subdir('library')

mbedcrypto_lib = library('mbedcrypto', mbedcrypto_src,
                         include_directories : mbed_inc,

                         install : true)

mbedx509_lib = library('mbedx509', mbedx509_src,
                       link_with : mbedcrypto_lib,
                       include_directories : mbed_inc,
                       install : true)

mbedtls_lib = library('mbedtls', mbedtls_src,
                      link_with : [ mbedcrypto_lib, mbedx509_lib ],
                      include_directories : mbed_inc,
                      dependencies : mbed_deps,
                      install : true)

mbed_dep = declare_dependency(link_with : [ mbedcrypto_lib, mbedx509_lib, mbedtls_lib ],
                               include_directories : mbed_inc)

subdir('programs')
