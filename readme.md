git init --bare $HOME/.dotfiles
alias dotfiles='/usr/bin/git --git-dir=$HOME/.dotfiles --work-tree=$HOME'

echo "alias dotfiles='/usr/bin/git --git-dir=$HOME/.dotfiles --work-tree=$HOME'" >> ~/.bashrc
source ~/.bashrc

dotfiles config --local status.showUntrackedFiles no

dotfiles add .bashrc
dotfiles add .zshrc
dotfiles add .vimrc

dotfiles commit -m "Initial commit of dotfiles"

dotfiles remote add origin git@github.com:username/dotfiles.git



avoid overwriting::
mkdir -p .dotfiles-backup
/usr/bin/git --git-dir=$HOME/.dotfiles --work-tree=$HOME checkout 2>&1 | \
grep -E "\s+\." | awk '{print $1}' | \
xargs -I{} mv {} .dotfiles-backup/{}

