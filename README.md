aseom.dotfiles
================

> __Docs__  
> [Node.js](docs/nodejs.md)
> [Cheatsheet - Linux](docs/cheatsheet-linux.md)

## macbook-pro

> 잠자기 시 암호 요구 끔  
> 보안 설정에서 자동 로그인 활성화 (사용자 설정 아님!)  
> 공유 설정에서 컴퓨터 이름 지정

> Requires [XCode][] & [Homebrew][]  
> `brew install git vim zsh`

[XCode]: https://itunes.apple.com/kr/app/xcode/id497799835?mt=12
[Homebrew]: http://brew.sh

```Shell
cd ~
git clone https://github.com/aseom/dotfiles.git
ln -sf ~/dotfiles/.gitconfig
ln -sf ~/dotfiles/.gitignore_global
ln -sf ~/dotfiles/.vimrc
ln -sf ~/dotfiles/.zshrc
ln -sf ~/dotfiles/bin

# Create .ssh dir, Copy SSH keys, then
chmod 700 .ssh && chmod 600 .ssh/*.pem
ln -sf ~/dotfiles/.ssh/config .ssh

# Karabiner
cd "$HOME/Library/Application Support/Karabiner"
ln -sf ~/dotfiles/karabiner/private.xml
```

###### zsh를 기본 셸로 쓰기
```Shell
sudo cp -p /etc/shells /etc/shells.backup_
echo $(which zsh) | sudo tee -a /etc/shells
chpass -s $(which zsh)
```

###### Dotfiles 푸시할 때 SSH 쓰기
```Shell
cd ~/dotfiles && git remote set-url origin git@github.com:aseom/dotfiles.git
```

###### Firefox - `about:config`
```INI
gfx.color_management.mode = 1
gfx.color_management.enablev4 = true
mousewheel.default.delta_multiplier_y = 200
```

---

###### TODO: 여기 아래 있는 것들 정리해야함.

#### Generate SSH key
```Shell
$ ssh-keygen -t rsa -N "" -f whatever.pem
```

#### 이미 커밋된 파일을 .gitignore에 추가

무시되지만 여전히 무시되지 않는(?) 파일의 리스트를 확인하고,  
해당되는 파일들을 stage 영역에서 삭제 후 변경사항을 커밋.

	$ git ls-files --ignored --exclude-standard
	$ git rm --cached path/to/file
	$ git commit -m "Delete ignored files"
