# NillionBecomeVerifier
> herhangi bir sunucuda çalıştırılabilir.
```console
# gerekli güncellemeler ve docker kurulumu
sudo apt update -y && sudo apt install -y apt-transport-https ca-certificates curl software-properties-common && sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg && echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null && sudo apt update -y && apt-cache policy docker-ce && sudo apt install -y docker-ce && sudo usermod -aG docker ${USER} && su - ${USER} -c "groups" && docker --version
```
```console
docker pull nillion/retailtoken-accuser:v1.0.0
```
```console
# dizin oluşturup accuser başlatalım
mkdir -p nillion/accuser && docker run -v ./nillion/accuser:/var/tmp nillion/retailtoken-accuser:v1.0.0 initialise
```
> yukarıdaki komut çalıştıktan sonra `account_id` ve `public_key` çıktılarını alacaksınız saklayın.
> [bu siteye](https://verifier.nillion.com/verifier) aldığımız `account_id` ve `public_key` girip doğruluyoruz.
> çıktıda aldığımız nillion adresimize [faucet](https://faucet.testnet.nillion.com/) token alıyoruz.
```console
# bu kodu çalıştırıp private key alıyoruz keplr import edip az önce girdiğimiz siteye bağlıyoruz. ! private key saklayın yoksa kaybedersiniz!
cat ~/nillion/accuser/credentials.json
```
> BU KISIMA 30-60DK SONRA DEVAM EDİN..
```console
sudo apt update && sudo apt install -y screen jq
```
```console
current_block=$(curl -s https://testnet-nillion-rpc.lavenderfive.com/abci_info | jq -r '.result.response.last_block_height'); block_start=$((current_block - 5)); docker run -v $(pwd)/nillion/accuser:/var/tmp nillion/retailtoken-accuser:v1.0.0 accuse --rpc-endpoint "https://testnet-nillion-rpc.lavenderfive.com" --block-start $block_start
```
>Done ✅, beni takip edin : [j4rdeux](https://x.com/j4rdeux)
