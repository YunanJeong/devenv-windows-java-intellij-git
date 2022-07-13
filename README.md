# devenv-Windows-Java-InteliiJ-git
- Tips for building InteliiJ and Java development environment on Windows
- In addition, Records of trial and error
- keywords: `WSL2, Windows, git, InteliiJ, Java, jdk`

## Quick Setup (가장 무난한 방법)
- Windows에 git 설치
- IntelliJ의 다음 메뉴에서 지정된 git 실행파일위치가 맞는지 확인한다.
  - `File-Settings-Version Control-Git-Path to Git excutable`
- 프로젝트 생성시 기존 설치된 jdk 선택 or 새로운 jdk 설치 가능
- git 관리는 git bash로 관리한다.
  - InteliiJ 자체에서도 별도 git bash 설치 없이 git 관리가능하지만, branch가 의도치 않게 분기될 수 있다.
  - git 사용법 검색시, InteliiJ의 git 기능보다 git command 찾는게 더 수월하다.
- 개발한다.


## Windows에 설치된 InteliiJ로 WSL2 환경에서 개발
- Windows InteliiJ를 쓰지만, 리눅스환경에서 개발하고 싶을 수 있다.
- InteliiJ에서 프로젝트 생성 및 오픈을 WSL2 경로에서 하면된다.
  - vscode의 `code`처럼 커맨드로 IntelliJ 실행은 불가하다.
  - 프로젝트 생성시,
    - jdk는 WSL2에 있는 것을 선택한다.
    - (주의)`WSL2+InteliiJ 조합에서 Gradle은 error발생. Maven만 가능하다.`
  - InteliiJ는 WSL2의 프로젝트 오픈시, 자동으로 WSL2의 글로벌 git설정을 참조한다.
    - 참고: https://www.jetbrains.com/help/idea/settings-version-control-git.html
    - `File-Settings-Version Control-Git-Path to Git excutable`에서 글로벌 git 정보 확인 및 변경가능


## Git 관련 참고
- global git이 설정되어있지 않은 상태에서, InteliiJ에서 commit을 시도하면 user.name과 user.email을 설정하라는 창이 뜬다.

- `If` "Set properties globally" is unchecked,
  - It is a local git configuration for that project only.
  - 프로젝트 "basepath의 config파일"에 git 정보가 등록된다.

- `Else` "Set properties globally" is checked(default),
  - It is a global git configuration for user's all projects.
	- `If` Git Bash is installed on Windows,
    - it is registered in the general Windows global git setting location.
	- `Else` Git Bash is not installed on Windows,
    - (중요!!!)User's information is added to the .gitconfig file of WSL2!!!
    - Moreover, conditional statement `IncludeIf` in .gitconfig of WSL2 is ignored by IntelliJ.
    - If you use only one git account, you can unify all git management on your PC with wsl2.
    - But, if you use multiple git accounts(e.g. private or business), you need to install git for Windows separately.