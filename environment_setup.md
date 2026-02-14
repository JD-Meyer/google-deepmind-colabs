### Set up the virtual environment
- open terminal
- for information only

sudo apt update

sudo apt install python3

sudo apt install python3-venv

cd /path-to-project/

python3 -m venv .venv

source .venv/bin/activate

cd .venv/bin

pip install "git+https://github.com/google-deepmind/ai-foundations.git@main"