require "rake/clean"

JRUBY_COMPLETE = "jruby-complete-1.4.0.jar"
JRUBY = "java -Xmx500m -Xss1024k -jar #{JRUBY_COMPLETE}"

desc "Run the application"
task :run do
  sh "#{JRUBY} lib/application_bootstrap.rb"
end

namespace :jruby do
  desc "Run JRuby help"
  task :help do
    sh %+#{JRUBY} --help+
  end

  desc "Run any command with JRuby"
  task :run do
    sh %+#{JRUBY} -e '#{ENV["cmd"]}'+
  end

  output_directory = "classes"
  directory output_directory
  CLEAN.include output_directory

  desc "Compile Ruby files in lib"
  task :compile => output_directory do
    sh %+#{JRUBY} -S jrubyc -p com/atomicobject -t #{output_directory} lib+
  end
end

namespace :spec do
  desc "Run RSpec against a specific file"
  task :run do
    raise "You need to specify a spec with spec=" if not ENV["spec"]
    sh %+#{JRUBY} -S spec -f specdoc #{ENV["spec"]}+
  end
end

task :default => :run
