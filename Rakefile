require "readline"

cache_file = ".fluent-plugin"

task :default => ["fluent:init"]

namespace :fluent do
  desc "build of fluent plugin template."
  task :init do |t, args|
    begin
      line = Readline.readline("fluent plugin name? > ", true)
      name = "fluent-plugin-#{line}"
      Dir.mkdir "dist"
      Dir.chdir "dist"
      system "bundle gem #{name}"
      Dir.chdir name
      Dir.mkdir "lib/fluent/#{name}"
      FileUtils.move "lib/#{name}.rb", "lib/fluent/plugin/out_#{line}"
      File.delete "lib/#{name}/version.rb"
      Dir.rmdir "lib/#{name}"
      Dir.mkdir "test/plugin"
      system "touch test/plugin/test_out_#{line}"
      Dir.chdir File.dirname(__FILE__)
      open(cache_file, "w").write(name)
    rescue
      puts "ERROR!"
    end
  end
end
