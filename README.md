# 🚀 Gensyn RL-Swarm RTX 5000 Series Fork

Pre-patched and tested fork of Gensyn RL-Swarm for NVIDIA RTX 5090/5080/5070 (Blackwell sm_120).

## ✅ What's Included
- All RTX 5000 series patches pre-applied
- Working dependency versions locked
- vLLM disabled (incompatible with sm_120)
- Flash Attention disabled
- DHT bootstrap fixes
- Tested for 15 hours+ on RTX 5090

## 🎯 Quick Install
```bash
git clone https://github.com/nuxxor/rl-swarm-rtx5000
cd rl-swarm-rtx5000
python -m venv gensyn_env
source gensyn_env/bin/activate
pip install -r requirements-rtx5000.txt
#./run_rl_swarm.sh don't do this now!

📊 Tested Configuration

GPU: NVIDIA RTX 5090
CUDA: 12.8
Driver: 570.133.07
Ubuntu 22.04
Python 3.12

🤝 Credits
Original repo: https://github.com/gensyn-ai/rl-swarm
EOF
git add README.md
git commit -m "Add README for RTX 5000 series"
git push
```

## Modified for my own use
do belows
```bash
pip install -r requirements-rtx5000_add01.txt
pip install -r requirements-rtx5000_add02.txt
pip install --pre torch torchvision torchaudio --index-url https://download.pytorch.org/whl/nightly/cu128
pip install "git+https://github.com/learning-at-home/hivemind@53533289edfeb1f9b2f5917cbae66fe50cfa2548#egg=hivemind"
```
modify the following lines in `run_rl_swarm.sh`
```bash
python /home/your_folder/rl-swarm-rtx5000/full_patch.py
python /home/your_folder/rl-swarm-rtx5000/fix_flash_attn.py
python /home/your_folder/rl-swarm-rtx5000/fix_flash_attn.py
```
in new terminal
```bash
cd modal-login
```
make .env file with following
```bash
NEXT_PUBLIC_ALCHEMY_API_KEY=RL2EtY6LXx2XCLPV3JZriJAB9mnELa2U
NEXT_PUBLIC_PAYMASTER_POLICY_ID=4c37387c-2a55-4edd-b188-b5c44eb71e96
SMART_CONTRACT_ADDRESS=0x6947c6E196a48B77eFa9331EC1E3e45f3Ee5Fd58
```
then run follows
```bash
npm install next@latest react@latest react-dom@latest`
npm run dev
```
go to localhost:3000, login then comback to the original terminal
(dont turn off the new terminal which running localhost)
```bash
./run_rl_swarm.sh
```