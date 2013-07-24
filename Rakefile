require "readline"

cache_file = ".fluent-plugin"

task :default => ["fluent:init"]

namespace :fluent do
  desc "build of fluent plugin template."
  task :init do |t, args|
    begin
      line = Readline.readline("fluent plugin name? > ", true)
      name = "fluent-plugin-#{line}"
      system "mkdir dist"
      Dir.chdir "dist"
      system "bundle gem #{name}"
      Dir.chdir name
      system "mkdir -p lib/fluent/#{name}"
      system "mv lib/#{name}.rb lib/fluent/plugin/out_#{line}"
      system "rm lib/#{name}/version.rb"
      system "rmdir lib/#{name}"
      system "mkdir -p test/plugin"
      system "touch test/plugin/test_out_#{line}"
      Dir.chdir File.dirname(__FILE__)
      open(cache_file, "w").write(name)
    rescue
      puts "ERROR!"
    end
  end
end
