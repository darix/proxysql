project('proxysql', ['c', 'cpp'],
    version: '2.20.0',
    license: 'GPL-2.0',
    meson_version: '>= 0.53.0',
)
git_version_define = '-DGITVERSION="5b31997"'

add_project_arguments(git_version_define, language: 'c')
add_project_arguments(git_version_define, language: 'cpp')

subdir('src')
