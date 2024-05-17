Vagrant.configure("2") do |config|
  
  config.vm.box = "debian/bullseye64"
  config.vm.network "private_network", ip: "192.168.33.23"  
  config.vm.provision "shell", inline: <<-SHELL
    sudo apt-get update
    sudo apt-get install -y nginx openssl ufw

    sudo ufw enable
    sudo ufw allow ssh
    sudo ufw allow 'Nginx Full'
    sudo ufw delete allow 'Nginx HTTP'
    sudo ufw --force enable

    sudo rm -r /etc/nginx/sites-enabled/default

    sudo mkdir -p /var/www/example/html

    cp -vr /vagrant/example.com /etc/nginx/sites-available/
    # Usuario - > santi | vilches passwd -> password1 | password2
    sudo cp /vagrant/.htpasswd /etc/nginx/
    sudo cp -r /vagrant/html/* /var/www/example/html
  
    sudo chown -R www-data:www-data /var/www/example/html
    sudo chmod -R 755 /var/www/example/html

    if [ ! -f "/etc/nginx/sites-enabled/www.example.com" ]; then
      sudo ln -s /etc/nginx/sites-available/www.example.com /etc/nginx/sites-enabled/
    fi

    sudo systemctl restart nginx
  SHELL
end