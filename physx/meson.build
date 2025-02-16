include = include_directories('include')

#add_project_arguments('-DRENDER_SNIPPET', language: 'cpp')

inc = run_command('src_include_grabber.sh', check: true)
sdkIncludes = inc.stdout().strip().split('\n')

src = run_command('src_grabber.sh', check: true)
sources = src.stdout().strip().split('\n')
message('sources: ', sources)

physxsdk = static_library('physx', 
  sources : sources, 
  include_directories: [include, sdkIncludes])

physxDep = declare_dependency(
  include_directories: [include, sdkIncludes],
  link_with: physxsdk
)

install_subdir('include/physx', install_dir : get_option('includedir'), install_tag : 'devel')

pkg_mod = import('pkgconfig')
pkg_mod.generate(
    name : 'physx',
    filebase : 'physx',
    description: 'NVIDIA PhysX SDK',
    subdirs : 'physx'
)

snippetInc = run_command('snippet_include_grabber.sh', check: true)
snippetIncludes = inc.stdout().strip().split('\n')

snippetSrc = run_command('snippet_grabber.sh', check: true)
snippetSources = src.stdout().strip().split('\n')

glewDep = dependency('glew', required: true)

helloWorld = static_library('physx_hello_world', 
  sources: [
    #'snippets/snippetdeformablevolume/SnippetDeformableVolume.cpp', 
    #'snippets/snippetdeformablevolume/SnippetDeformableVolumeRender.cpp',
    'snippets/snippethelloworld/SnippetHelloWorld.cpp', 
    'snippets/snippethelloworld/SnippetHelloWorldRender.cpp', 
    #'snippets/snippetrender/SnippetRender.cpp',
    #'snippets/snippetrender/SnippetFontRenderer.cpp',
    #'snippets/snippetrender/SnippetCamera.cpp',
    'snippets/snippetutils/SnippetImmUtils.cpp',
    'snippets/snippetutils/SnippetUtils.cpp'
    ], 
  include_directories: [include, sdkIncludes, snippetIncludes],
  link_with: [physxsdk])

executable('snippet',
  sources: ['snippets/snippetcommon/ClassicMain.cpp'],
  include_directories: [include, sdkIncludes, snippetIncludes],
  dependencies: [glewDep],
  link_with: [physxsdk, helloWorld])
