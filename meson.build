project('proxysql', ['c', 'cpp'],
    version: '2.0.10',
    license: 'GPL-3.0',
    meson_version: '>= 0.53.0',
    default_options : ['cpp_std=gnu++17', 'c_std=c11'],
)
git_version_define = '-DGITVERSION="' + meson.project_version() + '"'

add_project_arguments(git_version_define, language: 'c')
add_project_arguments(git_version_define, language: 'cpp')

if get_option('clickhouse')
    clickhouse_define  = '-DPROXYSQLCLICKHOUSE'
    add_project_arguments(clickhouse_define,  language: 'c')
    add_project_arguments(clickhouse_define,  language: 'cpp')
endif

subdir('src')
