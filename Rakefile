# encoding: utf-8
require 'rubygems'
require 'bundler'
Bundler::GemHelper.install_tasks

$:.unshift(File.dirname(__FILE__) + '/lib')
Dir['gem_tasks/**/*.rake'].each { |rake| load rake }

require 'rubocop/rake_task'
RuboCop::RakeTask.new do |t|
  t.patterns = FileList[
    'cucumber.gemspec',
    'Gemfile',
    'Rakefile',
    'examples/**/*.rb',
    'features/**/*.rb',
    'gem_tasks/**/*.{rake,rb}',
    'lib/**/*.rb',
    'spec/**/*.rb',
  ]
end

require 'cucumber/rake/task'
Cucumber::Rake::Task.new

default_tasks = [:spec, :rubocop, :cucumber]

if ENV['TRAVIS'] && RUBY_VERSION < '2.4'
  ENV['SIMPLECOV']  = 'ci'
  ENV['JRUBY_OPTS'] = [ENV['JRUBY_OPTS'], '--debug'].compact.join(' ')

  require 'coveralls/rake/task'
  Coveralls::RakeTask.new

  default_tasks << 'coveralls:push'
end

task :default => default_tasks

require 'rake/clean'
CLEAN.include %w(**/*.{log,pyc,rbc,tgz} doc)
