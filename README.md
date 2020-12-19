# 지환이의 iTerm2 디자인을 훔쳐보자!
### **보충이 필요한 부분은 issue 주세요!**
******

**🏠 Homebrew 설치하기**
```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

**🛠 ZSH 설치하기**
```
# zsh 설치하기
brew install zsh

# zsh 설치경로 확인하기
which zsh

# 기본 shell 변경하기
chsh -s $(which zsh)
```

**만약 zsh 접근이 제대로 안된다면 기본 터미널 설정을 수정해 줍니다.**
> 터미널 환경설정 일반 -> 셀 열기를 “기본 로글인 셀”에서 “명령어(절대경로)“로 바꾸고 /usr/local/bin/zsh (zsh 설치경로) 를 입력합니다.  
>   
> 혹은,  
> /etc/shells 파일에 /usr/local/bin/zsh 를 추가합니다.

<br>

**😮 Oh-My-Zsh 설치**
```
# wget curl 설치
brew install curl

# oh-my-zsh 설치
sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
```

**🖊 zshrc파일 수정하기**
```
vi ~/.zshrc 또는 opne ~/.zshrc
```
> 위 명령어를 통해 설정파일에 진입합니다.   
> 위쪽에서 5~15번째줄쯤 **ZSH_THEME=”robyrussell”** 라고 되어있는 부분이 있습니다.  
> 이부분을 **agnoster** 로 수정합니다.
> <br>   
> agnoster는 기본테마이기때문에 추가적인 설치는 필요없습니다.   
> 그 다음 저장을해준 후 터미널을 나온다음 아래 명령어로 zshrc파일을 적용시켜줍니다.


**변경후 아래 코드로 꼭 적용을 시켜줘야해요!**
```
source ~/.zshrc
```

**📍 font install**
```
https://github.com/naver/d2codingfont에 들어가 
폰트를 다운받은 후 최신버전을 설치해줍니다.
```

**✅ 세부설정** 
> iTerm2에 들어가서  cmd + , 를눌러 환경설정에 들어간 후 상단 Profile -> Text로 진입한다음  
> change Font를 누른 후 D2Coding폰트를 선택합니다.   
> 폰트가 너무 작아보인다면 13pt를 해도 좋습니다.

<br>

**❌ 쓸대없는 경로지우기(MacBook Pro ~)**
> 조금전 ~/.zshrc파일로 다시들어가 하단에 아래와같이 추가해줍니다.

```
prompt_context() {
  if [[ "$USER" != "$DEFAULT_USER" || -n "$SSH_CLIENT" ]]; then
    prompt_segment black default "%(!.%{%F{yellow}%}.)$USER"
  fi
}
```
> 이렇게하면 사용자 이름만 변경되고  
> 아무것도 나오게하고싶지 않다면 중괄호안의 내용을 지우고 {}로만 놔둡니다.

<br>

**🙀 New Line 적용하기(옵션)**
>theme파일을 엽니다.
```
vi ~/.oh-my-zsh/themes/agnoster.zsh-theme
//or
open -a TextEdit ~/.oh-my-zsh/themes/agnoster.zsh-theme
```
> 하단 buld_prompt를 찾아 꼭 prompt_end 위에 prompt_newline을 추가합니다.
```
build_prompt() {
  RETVAL=$?
  prompt_status
  prompt_virtualenv
  prompt_context
  prompt_dir
  prompt_git
  prompt_bzr
  prompt_hg
  prompt_newline //이부분을 추가 꼭 순서 지켜서
  prompt_end
}
```

> 그다음 아래 코드를 추가합니다.

```
prompt_newline() {
  if [[ -n $CURRENT_BG ]]; then
    echo -n "%{%k%F{$CURRENT_BG}%}$SEGMENT_SEPARATOR
%{%k%F{blue}%}$SEGMENT_SEPARATOR"
  else
    echo -n "%{%k%}"
  fi

  echo -n "%{%f%}"
  CURRENT_BG=''
}
```

<br>

**😀 Syntax Hightlight 적용하기 (옵션)**
```
//brew를 통해 설치해줍니다.
brew install zsh-syntax-highlighting

//플러그인을 적용합니다.
source /usr/local/share/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh
```