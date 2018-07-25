project('benchmark', 'cpp', default_options : ['cpp_std=c++11'], version : '1.4.1')


cc = meson.get_compiler('cpp')

public_deps = [dependency('threads', required : true)]

if host_machine.system() == 'linux'
  public_deps += cc.find_library('rt', required : true)
elif host_machine.system() == 'windows'
  public_deps += cc.find_library('Shlwapi', required : true)
endif

src = [
  'src/commandlineflags.cc',
  'src/reporter.cc',
  'src/console_reporter.cc',
  'src/benchmark.cc',
  'src/complexity.cc',
  'src/csv_reporter.cc',
  'src/sysinfo.cc',
  'src/string_util.cc',
  'src/benchmark_register.cc',
  'src/sleep.cc',
  'src/counter.cc',
  'src/json_reporter.cc',
  'src/timers.cc',
  'src/colorprint.cc',
  'src/statistics.cc',
]

private_defs = ['-DHAVE_STD_REGEX', '-DHAVE_STEADY_CLOCK']

# benchmark target name is reserved by meson

private_inc = include_directories('include', 'src')

benchmark_lib = static_library('libbenchmark',
  name_prefix : '',
  sources : src,
  dependencies : public_deps,
  include_directories : private_inc,
  cpp_args : private_defs,
)

benchmark_main_lib = static_library('libbenchmark_main',
  name_prefix : '',
  sources : 'src/benchmark_main.cc',
  dependencies : public_deps,
  include_directories : private_inc,
  cpp_args : private_defs,
  link_with : benchmark_lib,
)

public_inc = include_directories('include', is_system : true)

benchmark_dep = declare_dependency(
  link_with : benchmark_lib,
  include_directories : public_inc,
  dependencies : public_deps,
)

benchmark_main_dep = declare_dependency(
  link_with : benchmark_main_lib,
  include_directories : public_inc,
  dependencies : public_deps,
)
