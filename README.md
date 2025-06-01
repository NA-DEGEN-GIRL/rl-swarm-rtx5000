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

## ⚡ Quick start

```bash
git clone https://github.com/NA-DEGEN-GIRL/rl-swarm-rtx5000
cd rl-swarm-rtx5000

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
rm -rf rl-swarm gensyn-testnet .nvm .npm .ngrok*
```
install node22.x
```bash
sudo apt-get update
curl -fsSL https://deb.nodesource.com/setup_22.x | sudo -E bash -
sudo apt-get install -y nodejs
```

```bash
cd modal-login
cp .env.example .env        # create .env then edit:
# RPC / contract details
NEXT_PUBLIC_ALCHEMY_API_KEY=<your-alchemy-key>
NEXT_PUBLIC_PAYMASTER_POLICY_ID=<policy-id>
SMART_CONTRACT_ADDRESS=0x6947c6E196a48B77eFa9331EC1E3e45f3Ee5Fd58

npm install
npm run dev        # localhost:3000
```

Leave this terminal running, return to the main repo and start the swarm:
```bash
./run_rl_swarm.sh
```
