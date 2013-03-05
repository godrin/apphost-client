require 'rake/clean'
begin
  require 'rubygems/package_task'
rescue LoadError
end

def spec
  require 'rubygems' unless defined? Gem::Specification
  @spec ||= eval(File.read('apphost-client.gemspec'))
end

def package(ext='')
  "pkg/apphost-client-#{spec.version}" + ext
end

desc 'Build packages'
task :package => %w[.gem].map {|e| package(e)}

desc 'Build and install as local gem'
task :install => package('.gem') do
  sh "gem install #{package('.gem')}"
end

directory 'pkg/'
CLOBBER.include('pkg')

file package('.gem') => %w[pkg/ apphost-client.gemspec] + spec.files do |f|
  sh "gem build apphost-client.gemspec"
  mv File.basename(f.name), f.name
end

