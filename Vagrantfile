# load .env
Dotenv.load

# change default provider to digital_ocean
Vagrant.configure(2) do |config|
  machine_name  = [ 
    "nginx",
  ]
  machine_size   = 
  { 
    "nginx" => "nano_1_0", # "nano_1_0", "micro_1_0", "small_1_0", "medium_1_0", "large_1_0"
  }

  config.ssh.username         = "ubuntu"
  config.ssh.private_key_path = ENV['SSH_KEY']
  config.vm.box               = 'lightsail'
  config.vm.box_url           = 'https://github.com/thejandroman/vagrant-lightsail/raw/master/box/lightsail.box'

  machine_name.each do |machine|
    config.vm.define "#{machine}" do |config|
      config.vm.provider :lightsail do |provider, override|
        provider.bundle_id         = machine_size[machine]
        provider.blueprint_id      = "ubuntu_16_04"
        provider.region            = "ap-northeast-1"

        provider.access_key_id     = ENV['LS_ACCESS_KEY_ID']
        provider.secret_access_key = ENV['LS_SECRET_ACCESS_KEY']
        provider.key_pair_name     = ENV['LS_KEYPAIR']
        provider.port_info         = 
        [
          { from_port: 80,  to_port: 80,  protocol: 'tcp' },
          { from_port: 443, to_port: 443, protocol: 'tcp' }
        ]

        override.vm.synced_folder "./html", "/var/www/html", type: "rsync"


        if ARGV[0] == "up" || ARGV[0] == "provision" then
          config.vm.provision :shell do |shell|
            shell.inline = <<-SHELL
              sudo apt update && \
              sudo apt install -y \
                nginx && \
              sudo service nginx start && \
              echo "Node IP Address..." && \
              curl -sS httpbin.org/ip
            SHELL
            shell.privileged = false
          end
        end
      end
    end
  end
end

