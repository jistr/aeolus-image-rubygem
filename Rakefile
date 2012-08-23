#   Copyright 2011 Red Hat, Inc.
#
#   Licensed under the Apache License, Version 2.0 (the "License");
#   you may not use this file except in compliance with the License.
#   You may obtain a copy of the License at
#
#       http://www.apache.org/licenses/LICENSE-2.0
#
#   Unless required by applicable law or agreed to in writing, software
#   distributed under the License is distributed on an "AS IS" BASIS,
#   WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
#   See the License for the specific language governing permissions and
#   limitations under the License.

require 'rubygems'
require 'rake'
require 'rake/clean'
require 'rubygems/package_task'
require 'rdoc/task'
require 'rake/testtask'
require 'rspec/core/rake_task'
require './rake/rpmtask'

RPMBUILD_DIR = "#{File.expand_path('~')}/rpmbuild"
RPM_SPEC = "rubygem-aeolus-image.spec"
RPM_SPEC_IN = "rubygem-aeolus-image.spec.in"
PKG_VERSION = "0.6.0"

spec = eval(File.read('aeolus-image.gemspec'))

Gem::PackageTask.new(spec) do |p|
  p.gem_spec = spec
  p.need_tar = true
  p.need_zip = true
end

Rake::RDocTask.new do |rdoc|
  files =['README', 'COPYING', 'lib/**/*.rb']
  rdoc.rdoc_files.add(files)
  rdoc.main = "README" # page to start on
  rdoc.title = "aeolus-image Docs"
  rdoc.rdoc_dir = 'doc/rdoc' # rdoc output folder
  rdoc.options << '--line-numbers'
end

Rake::TestTask.new do |t|
  t.test_files = FileList['test/**/*.rb']
end

RSpec::Core::RakeTask.new do |t|
  t.pattern = FileList['spec/**/*.rb']
end

Rake::RpmTask.new(RPM_SPEC, {:suffix => '.in', :pkg_version => PKG_VERSION}) do |rpm|
  rpm.need_tar = true
  rpm.package_files.include("lib/*")
  rpm.topdir = "#{RPMBUILD_DIR}"
end
