# Bu rehberde, Covalent Network refiner node'unu Docker Compose kullanarak nasıl kuracağınızı öğreneceksiniz. Adımları takip ederek Covalent Network refiner node'unu başarıyla çalıştırabilirsiniz.

# Adım 1: Docker Kurulumu
````
Öncelikle, Docker'ı sisteminize yüklemeniz gerekiyor. Platformunuz ve mimariniz için Docker kurulum talimatlarını takip edin.
````

# Adım 2: direnv Kurulumu.
````
Direnv, refiner node kurulumunda kullanacağımız bir araçtır. Ubuntu 22.04 LTS x86_64 / amd64 platformunda çalıştıracağız.
````
````
sudo apt update
sudo apt get direnv

# bash kullanıcıları - ~/.bashrc dosyanıza aşağıdaki satırı ekleyin
eval "$(direnv hook bash)"
source ~/.bashrc

# zsh kullanıcıları - ~/.zshrc dosyanıza aşağıdaki satırı ekleyin
eval "$(direnv hook zsh)"
source ~/.zshrc
````

# Adım 3: Covalent Network Refiner Repo'sunu Klonlayın ve Çevre Değişkenlerini Ayarlayın
````
git clone https://github.com/covalenthq/rudder
cd rudder
cat docker-compose-mbase.yml
````
# Adım 4: Global Çevre Değişkenlerini Kontrol Edin
````
cat .envrc
````
# Adım 5: Yerel Çevre Değişkenlerini Ayarlayın
````
touch .envrc.local

export BLOCK_RESULT_OPERATOR_PRIVATE_KEY="BRP-OPERATOR-PK-WITHOUT-0x-PREFIX"
export NODE_ETHEREUM_MAINNET="<<ASK-ON-DISCORD>>"
export IPFS_PINNER_URL="http://ipfs-pinner:3001"
export EVM_SERVER_URL="http://evm-server:3002"
export WEB3_JWT="<<WEB3.STORAGE-API-TOKEN>>"
````
# Not: Yukarıdaki gibi özel anahtarı çevre değişkenlerine eklerken, 0x önekini kaldırdığınızdan emin olun.
````
1 - BLOCK_RESULT_OPERATOR_PRIVATE_KEY: Kişisel Block Result Producer (BRP) operator özel anahtarınız
2 - WEB3_JWT: ipfs-pinner servisi tarafından kullanılan kişisel web3.storage API token'ınız
3 - IPFS_PINNER_URL: rudder'ın Block Specimens gibi IPFS varlıklarına erişmek için kullandığı servis (ipfs-pinner)
4 - EVM_SERVER_URL: rudder'ın sorgulanabilir (indexable) Block Result için Block Specimens'ları durumsuz bir şekilde çalıştırdığı servis (evm-server)
````
# Adım 6: Servisleri Başlatın Çevre değişkenlerini kabuğa yükleyin:
````
direnv allow .
````
# Daha sonra, Moonbase alpha için 3 hizmeti arka planda çalıştırın:
````
docker compose -f "docker-compose-mbase.yml" up -d --remove-orphans
````
# Adım 7: Block Result Gönderimleri için Kayıtları İzleyin
````
docker compose -f "docker-compose-mbase.yml" logs -f --tail 2
````

# Bu adımları izleyerek Covalent Network refiner node'unu Docker Compose kullanarak başarıyla çalıştırabilirsiniz.

