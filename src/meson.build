cpp_compiler = meson.get_compiler('cpp')

compiler_flags = cpp_compiler.get_supported_arguments(['-faligned-new', '-fno-strict-aliasing'])
add_project_arguments(compiler_flags, language: 'cpp')

stdcpp       = cpp_compiler.find_library('stdc++',    required: true)
dl           = cpp_compiler.find_library('dl',        required: true)
libinjection = cpp_compiler.find_library('injection', required: true)

cpp_compiler.has_header('libinjection.h',      required: true)
cpp_compiler.has_header('libinjection_sqli.h', required: true)

# TODO: use declare_dependency when we have a subproject for the patched mariadbclient
#libmariadbclient = cpp_compiler.find_library('libmariadbclient',
#    dirs: ['../deps/mariadb-client-library/mariadb_client/libmariadb/'],
#    required: true
#)

# TODO: add option for jemalloc
jemalloc      = dependency('jemalloc',      required: true)
libdaemon     = dependency('libdaemon',     required: true)
libconfig     = dependency('libconfig++',   required: true)
re2           = dependency('re2',           required: true)
pcre          = dependency('libpcrecpp',    required: true)
sqlite3       = dependency('sqlite3',       required: true)
libmicrohttpd = dependency('libmicrohttpd', required: true)
libhttpserver = dependency('libhttpserver', required: true)
libcurl       = dependency('libcurl',       required: true)
libev         = dependency('libev',         required: true)
libcrypto     = dependency('libcrypto',     required: true)
libssl        = dependency('libssl',        required: true)
zlib          = dependency('zlib',          required: true)

deps = [
        stdcpp,
        dl,
        libinjection,
        jemalloc,
        libdaemon,
        libconfig,
        re2,
        pcre,
        sqlite3,
        libmicrohttpd,
        libhttpserver,
        libcurl,
        libev,
        libcrypto,
        libssl,
        zlib,
]

sources = [
   '../lib/c_tokenizer.c',
   '../lib/Chart_bundle_js.cpp',
   '../lib/configfile.cpp',
   '../lib/debug.cpp',
   '../lib/font-awesome.min.css.cpp',
   '../lib/gen_utils.cpp',
   '../lib/main-bundle.min.css.cpp',
   '../lib/MySQL_Authentication.cpp',
   '../lib/mysql_backend.cpp',
   '../lib/mysql_connection.cpp',
   '../lib/mysql_data_stream.cpp',
   '../lib/MySQL_HostGroups_Manager.cpp',
   '../lib/MySQL_Logger.cpp',
   '../lib/MySQL_Monitor.cpp',
   '../lib/MySQL_PreparedStatement.cpp',
   '../lib/MySQL_Protocol.cpp',
   '../lib/MySQL_Session.cpp',
   '../lib/MySQL_Thread.cpp',
   '../lib/network.cpp',
   '../lib/ProxySQL_Admin.cpp',
   '../lib/ProxySQL_Cluster.cpp',
   '../lib/ProxySQL_Config.cpp',
   '../lib/ProxySQL_GloVars.cpp',
   '../lib/ProxySQL_HTTP_Server.cpp',
   '../lib/ProxySQL_Restapi.cpp',
   '../lib/ProxySQL_RESTAPI_Server.cpp',
   '../lib/ProxySQL_Statistics.cpp',
   '../lib/Query_Cache.cpp',
   '../lib/Query_Processor.cpp',
   '../lib/set_parser.cpp',
   '../lib/SpookyV2.cpp',
   '../lib/sqlite3db.cpp',
   '../lib/thread.cpp',
   'main.cpp',
   'proxysql_global.cpp',
   'SQLite3_Server.cpp'
]

includes = [
    '../include/',
    '../deps/mariadb-client-library/mariadb_client/include',
]

if get_option('clickhouse')
    deps   += [ cpp_compiler.find_library('clickhouse-cpp-lib-static', required: true) ]
    cpp_compiler.has_header('clickhouse/client.h', required: true)
    sources += [
       '../lib/ClickHouse_Authentication.cpp',
       '../lib/ClickHouse_Server.cpp',
    ]
endif

mod_mirrorbrain = executable('proxysql',
    sources,
    dependencies: deps,
    include_directories: includes,
    install: true,
    install_dir : get_option('sbindir'),
    pie: true,
    link_args: [
        '-L../deps/mariadb-client-library/mariadb_client/libmariadb', '-lmariadbclient',
    ],
)
