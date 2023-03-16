# Compile flow 

sudo bash kitware-archive.sh

west init ./zephyrproject

cd ./zephyrproject

west update

west zephyr-export

pip3 install -r ./zephyr/scripts/requirements.txt

cd ..

## download SDK

wget https://github.com/zephyrproject-rtos/sdk-ng/releases/download/v0.15.2/zephyr-sdk-0.15.2_linux-x86_64.tar.gz

wget -O - https://github.com/zephyrproject-rtos/sdk-ng/releases/download/v0.15.2/sha256.sum | shasum --check --ignore-missing

tar xvf zephyr-sdk-0.15.2_linux-x86_64.tar.gz

cd zephyr-sdk-0.15.2

./setup.sh

cd zephyrproject/zephyr/
