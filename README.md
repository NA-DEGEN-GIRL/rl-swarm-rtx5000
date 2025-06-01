# 🚀 Gensyn RL-Swarm — RTX 5000 Series (5090 / 5080 / 5070)

Fork of Gensyn’s RL-Swarm, pre-patched and validated for NVIDIA Blackwell GPUs (sm_120).

---

## ✅ Key changes
| Feature | Status |
|---------|--------|
| RTX 5000-series kernels & flags | **Patched** |
| Working dependency lockfile    | **Included** |
| vLLM / Flash-Attn (sm 120 clash) | **Disabled** |
| DHT bootstrap race fix         | **Applied** |
| Soak test                      | **15 h on RTX 5090** |

---

## Install python 3.12 first (recommend to use pyenv)
how to install pyenv (Linux need curl)
```bash
sudo apt update
sudo apt install -y curl build-essential clang make \
  libssl-dev zlib1g-dev libbz2-dev libreadline-dev libsqlite3-dev \
  libffi-dev libncursesw5-dev liblzma-dev tk-dev uuid-dev
curl -fsSL https://pyenv.run | bash
pyenv install 3.12.10
```

## ⚡ Quick start
```bash
git clone https://github.com/NA-DEGEN-GIRL/rl-swarm-rtx5000
cd rl-swarm-rtx5000
pyenv local 3.12.10 # you can skip if you don't use pyenv
python -m venv gensyn_env && source gensyn_env/bin/activate
pip install -r requirements-rtx5000.txt
# 👉 Do **not** run ./run_rl_swarm.sh yet
```

## 🔧 Extra steps for my custom workflow
```bash
pip install -r requirements-rtx5000_add01.txt
pip install -r requirements-rtx5000_add02.txt
pip install --pre torch torchvision torchaudio \
  --index-url https://download.pytorch.org/whl/nightly/cu128
pip install "git+https://github.com/learning-at-home/hivemind@53533289edfeb1f9b2f5917cbae66fe50cfa2548#egg=hivemind"
```
Edit run_rl_swarm.sh:
```bash
python /home/<user>/rl-swarm-rtx5000/full_patch.py
python /home/<user>/rl-swarm-rtx5000/fix_flash_attn.py
```

## 🌐 Modal Login UI
remove previous node installation if any
```bash
cd ~
sudo apt update
sudo apt remove --purge nodejs npm -y 2>/dev/null
sudo apt autoremove -y
rm -rf .nvm .npm .ngrok*
```
install node22.x
```bash
sudo apt-get update
curl -fsSL https://deb.nodesource.com/setup_22.x | sudo -E bash -
sudo apt-get install -y nodejs
```
build login server using npm (not yarn)
```bash
cd modal-login
cp .env.example .env        # create .env then edit:
mkdir temp-data
```
# RPC / contract details
```bash
NEXT_PUBLIC_ALCHEMY_API_KEY=RL2EtY6LXx2XCLPV3JZriJAB9mnELa2U
NEXT_PUBLIC_PAYMASTER_POLICY_ID=4c37387c-2a55-4edd-b188-b5c44eb71e96
SMART_CONTRACT_ADDRESS=0x6947c6E196a48B77eFa9331EC1E3e45f3Ee5Fd58
```
continue
```bash
sudo npm install -g npm@10.9.2
npm install typescript@latest @types/react@latest @types/node@latest eslint-config-next@latest
npm run dev        # localhost:3000
```
remove cuda12.0 (you can skip)
```bash
sudo apt purge nvidia-cuda-toolkit nvidia-cuda-dev libcudart12 nvidia-cuda-gdb
sudo apt autoremove
```
cuda 12.8 install, refer to the following website. choose your os
following is the example of WSL2.0 ubuntu
https://developer.nvidia.com/cuda-12-8-0-download-archive?target_os=Linux&target_arch=x86_64&Distribution=WSL-Ubuntu&target_version=2.0&target_type=deb_local
```bash
wget https://developer.download.nvidia.com/compute/cuda/repos/wsl-ubuntu/x86_64/cuda-wsl-ubuntu.pin
sudo mv cuda-wsl-ubuntu.pin /etc/apt/preferences.d/cuda-repository-pin-600
wget https://developer.download.nvidia.com/compute/cuda/12.8.0/local_installers/cuda-repo-wsl-ubuntu-12-8-local_12.8.0-1_amd64.deb
sudo dpkg -i cuda-repo-wsl-ubuntu-12-8-local_12.8.0-1_amd64.deb
sudo cp /var/cuda-repo-wsl-ubuntu-12-8-local/cuda-*-keyring.gpg /usr/share/keyrings/
sudo apt-get update
sudo apt-get -y install cuda-toolkit-12-8
```
set path
```bash
echo 'export PATH=/usr/local/cuda-12.8/bin:$PATH' >> ~/.bashrc && source ~/.bashrc
```
check whether cuda_12.8 is installed correctly
```bash
nvcc -V
```

Leave this terminal running, return to the main repo and start the swarm:
```bash
./run_rl_swarm.sh
```
