require "erb"
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
      File.delete "lib/fluent/plugin/#{line}/version.rb"
      Dir.chdir File.dirname(__FILE__)
      Dir.chdir "dist/#{name}" 
      FileUtils.mkdir_p "test/plugin"
      File.write("test/plugin/test_out_#{line}.rb", "")

      Dir.chdir File.dirname(__FILE__)
      open(cache_file, "w").write(name)

      # Create class skelton file
      template = open("template/fluent-plugin-class.erb", "r").read
      erb = ERB.new(template)
      class_name = line
      r = erb.result(binding)

      Dir.chdir "dist/#{name}"
      open("lib/fluent/plugin/out_#{name}.rb", "w").write(r)
    rescue => e
      puts "ERROR!"
      puts e
    end
  end
end
