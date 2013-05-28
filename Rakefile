require 'puppet-lint/tasks/puppet-lint'
PuppetLint.configuration.ignore_paths = [
  "vendor/**/*.pp",
  "spec/**/*.pp",
]
PuppetLint.configuration.log_format = 
  "%{path}:%{linenumber}:%{check}:%{KIND}:%{message}"

# Since we're performing linting from within the module directory, we don't
# want to check for correct autoloading layout
PuppetLint.configuration.send('disable_autoloader_layout')

require 'puppet/face'
desc "Perform Puppet parser's validation on manifests"
task :validate do
  Puppet::Face[:parser, '0.0.1'].validate(FileList['**/*.pp'].exclude('vendor/**/*.pp', 'spec/**/*.pp').join())
end

require 'rspec/core/rake_task'
RSpec::Core::RakeTask.new(:spec) do |t|
  t.rspec_opts = ['--color']
  t.pattern = 'spec/**/*_spec.rb'
end
