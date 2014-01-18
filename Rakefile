task :install do
  require 'fileutils'
  unless File.exist? 'config.yml'
    FileUtils.copy 'config-sample.yml', 'config.yml'
  end
  `whenever -w`
end

task :uninstall do
  `whenever -c`
end

task :archive do
  require 'date'
  require 'yaml'
  require_relative 'lib/camopticon'

  CONFIG = YAML.load_file('config.yml')

  CONFIG['cameras'].each do |camera|
    camopticon = Camopticon.new
    camopticon.date = (Date.today - 1).to_s
    camopticon.storage_path = CONFIG['storage_path']
    camopticon.pushover = CONFIG['pushover']
    camopticon.camera = camera
    camopticon.frames_to_video
    camopticon.remove_frames_dir
  end
end
