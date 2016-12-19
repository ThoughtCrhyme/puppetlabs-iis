require 'puppetlabs_spec_helper/rake_tasks'
require 'puppet-lint/tasks/puppet-lint'
require 'puppet_blacksmith/rake_tasks' if Bundler.rubygems.find_name('puppet-blacksmith').any?
require 'rototiller'

PuppetLint.configuration.fail_on_warnings = true
PuppetLint.configuration.send('relative')
PuppetLint.configuration.send('disable_80chars')
PuppetLint.configuration.send('disable_class_inherits_from_params_class')
PuppetLint.configuration.send('disable_documentation')
PuppetLint.configuration.send('disable_single_quote_string_with_variables')
PuppetLint.configuration.ignore_paths = ["spec/**/*.pp", "pkg/**/*.pp"]

module_pe_dir = {:name => 'BEAKER_PE_DIR', :default => 'http://enterprise.delivery.puppetlabs.net/archives/releases/2016.5.1/'}

desc 'Executes acceptance tests'
rototiller_task :acceptance do |t|
  t.add_command(name: 'rspec spec/acceptance')

  t.add_env do |env|
    env.name = 'PLATFORM'
    env.default = 'default.yml'
    env.message = "#{env.name} set to #{env.default}"
  end

  t.add_env do |env|
    env.name = 'BEAKER_keyfile'
    env.default = '~/.ssh/id_rsa-acceptance'
    env.message = "#{env.name} set to #{env.default}"
  end

  t.add_env(module_pe_dir)
end
