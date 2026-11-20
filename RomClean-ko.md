# RomClean

[English](RomClean.md) | **한국어**

MAME 롬을 관리하고 롬셋을 만드는 데스크톱 앱입니다 (Linux · macOS · Windows).

**[⬇ 최신 버전 내려받기](https://github.com/airplanez/AppsRepo/releases/tag/RomClean)**

> RomClean 은 롬을 제공하지 않습니다. 사용자가 보유한 파일만 관리합니다.

## 목차

- [기능](#기능)
- [내려받기 · 설치](#내려받기--설치)
- [빠른 시작](#빠른-시작)
- [RomClean 에서 게임 실행](#romclean-에서-게임-실행)
- [MAME 실행 파일 위치](#mame-실행-파일-위치)
- [MAME Software List](#mame-software-list)
- [장르 파일 (catver.ini · mature.ini)](#장르-파일-catverini--matureini)
- [데이터 저장 위치](#데이터-저장-위치)
- [초기화](#초기화)
- [삭제](#삭제)
- [버전 기록](#버전-기록)

## 기능

- 롬 폴더(zip · 7z · CHD · 샘플)를 **변경하지 않고** 스캔해 보유 현황을 기록합니다.
- MAME Dat(`mame -listxml`, 또는 MAME 실행 파일 선택)를 등록하면 머신별 완전 · 일부 누락 · 전체 누락을 보여 줍니다.
- `split` · `merged` · `non-merged` 형식의 zip 또는 7z 롬셋으로 내보냅니다 — 항상 TorrentZip / Torrent7z 규격이며, 지난 내보내기 뒤 바뀐 파일만 다시 씁니다. CHD 는 가능하면 하드링크로 만들어 디스크 공간을 더 쓰지 않습니다.
- 내보낸 게임을 목록에서 바로 MAME 로 실행합니다.
- MAME Software List (콘솔 · 컴퓨터) — `.nes` 처럼 다른 에뮬레이터용으로 만든 롬도 인식합니다.
- 장르(catver.ini · mature.ini) · 연도 · 제조사 · 화면 · 플레이어 수 필터와 "아케이드 게임만".
- 정리 기능: **중복 제거**(남는 사본 삭제)와 **안 맞는 파일 이동**(어느 타깃세트에도 필요 없는 파일을 옮김 — 삭제하지 않음).
- 영어 · 한국어, Light · Dark 테마.
- RomClean 은 어떤 정보도 수집 · 전송하지 않습니다.

## 내려받기 · 설치

**[RomClean 릴리스 페이지](https://github.com/airplanez/AppsRepo/releases/tag/RomClean)** 에서 사용하는 OS 의 파일을 내려받습니다.

설치 프로그램이 없습니다. 압축을 풀어 바로 실행합니다. `0.5.3` 은 내려받은 버전으로 바꿔 읽어 주세요.

### Linux (x64) — `romclean_v0.5.3_linux.tar.gz`

```bash
tar -xzf romclean_v0.5.3_linux.tar.gz
./romclean_v0.5.3_linux/romclean
```

- GTK 3 런타임이 필요합니다 (대부분의 데스크톱 배포판에 기본 설치되어 있습니다).
- 앱 목록에 아이콘과 함께 등록하려면 (선택):
  `./romclean_v0.5.3_linux/install-desktop-entry.sh` (제거는 `--uninstall`).
  폴더를 옮긴 뒤에는 다시 실행합니다.

### macOS (12 이상, Apple Silicon · Intel) — `romclean_v0.5.3_macos.zip`

1. zip 을 더블클릭해 `romclean.app` 을 꺼냅니다.
2. `응용 프로그램` 폴더로 옮긴 뒤(선택) 실행합니다.

Apple 의 서명과 공증을 받은 앱입니다.

### Windows (x64) — `romclean_v0.5.3_windows.zip`

1. zip 을 마우스 오른쪽 버튼으로 눌러 **압축 풀기**를 합니다.
2. `romclean_v0.5.3_windows` 폴더의 `romclean.exe` 를 실행합니다.

- 폴더 안의 파일을 모두 함께 두어야 합니다. `romclean.exe` 만 따로 옮기면 실행되지 않습니다.
- 코드 서명이 없는 앱입니다. "Windows의 PC 보호" 창이 나오면 **추가 정보 → 실행**을 누릅니다.

## 빠른 시작

1. **원본세트** → **디렉토리 추가** → 롬 폴더 선택 → **스캔**.
2. **타깃세트** → **타깃세트 추가** → MAME Dat 파일이나 MAME 실행 파일 선택.
3. 타깃세트를 열어 머신별 상태를 보고 **내보내기** 로 새 폴더에 롬셋을 만듭니다.
4. 완전한 머신의 ▶ 상태를 누르면 MAME 로 실행합니다 (아래 참고).

## RomClean 에서 게임 실행

타깃세트를 내보내고 RomClean 에 MAME 실행 파일이 등록되어 있으면 RomClean 에서 바로 게임을 실행할 수 있습니다.

1. **MAME 실행 파일 등록** — MAME 실행 파일로 만든 타깃세트는 자동으로 등록됩니다. 그 밖에는 타깃세트 메뉴(⋮) → **MAME 선택…** 으로 고르거나, 처음 실행할 때 고릅니다. RomClean 은 `mame -version` 으로 MAME 인지 확인합니다.
2. 타깃세트를 **내보내기** 합니다. 실제로 내보낸 완전한 머신은 상태 칩이 누를 수 있는 ▶ 버튼이 됩니다. 머신 상세 화면에도 **MAME 로 실행** 버튼이 생깁니다.
3. 누르고 확인하면 RomClean 이 다음처럼 실행합니다.

   ```
   mame -rompath <내보낸 폴더> [-samplepath <내보낸 폴더>/samples] <머신>
   ```

   Software List 항목은 `mame <본체> <목록>:<소프트웨어> -rompath <내보낸 폴더> -hashpath <hash 폴더>` 로 실행하며, 본체 머신(예: `nes`)은 실행 창에서 고릅니다.

- 게임은 원본 폴더가 아니라 **마지막으로 내보낸 폴더**에서 실행됩니다.
- MAME 가 오류로 멈추면(필요한 파일 없음 등) MAME 의 오류 출력 전체를 보여 줍니다.
- 타깃세트 카드에 마지막 내보낸 위치와 MAME 실행 파일이 표시됩니다. 메뉴의 **내보낸 폴더 열기** 로 파일 관리자에서 열 수 있습니다.

## MAME 실행 파일 위치

| OS | 설치 방법 | MAME 실행 파일 | Software List `hash` 폴더 |
| --- | --- | --- | --- |
| Linux (Debian · Ubuntu) | `sudo apt install mame` | `/usr/games/mame` | `/usr/share/games/mame/hash` (`mame-data` 패키지) |
| Linux (그 밖의 배포판) | 배포판 패키지 | 보통 `/usr/bin/mame` | 보통 `/usr/share/mame/hash` |
| Linux | `sudo snap install mame` | `/snap/bin/mame` | 패키지에 없음 (아래 참고) |
| macOS (Apple Silicon) | `brew install mame` | `/opt/homebrew/bin/mame` | `/opt/homebrew/share/mame/hash` |
| macOS (Intel) | `brew install mame` | `/usr/local/bin/mame` | `/usr/local/share/mame/hash` |
| Windows | [mamedev.org](https://www.mamedev.org/release.html) 의 공식 배포물을 원하는 폴더에 압축 해제 | `<그 폴더>\mame.exe` (예: `C:\mame\mame.exe`) | `<그 폴더>\hash` |

- 잘 모르겠으면 터미널에서 `command -v mame` (Linux · macOS) 를 실행해 확인합니다.
- RomClean 은 `hash` 폴더를 MAME 실행 파일 옆 → MAME 의 `hashpath` 설정(`mame -showconfig`) → 위 표의 위치 순서로 찾습니다. 찾지 못하면 직접 고릅니다.
- **Snap 으로 설치한 MAME**: 패키지에 `hash` 폴더가 없고, snap 은 허용된 폴더(보통 홈 폴더)만 읽을 수 있습니다. Software List 실행이 안 될 수 있으니 Software List 를 쓰려면 apt 패키지를 쓰고, 내보내기 폴더는 홈 폴더 안에 두세요.

## MAME Software List

**무엇인가.** MAME 는 아케이드 기판 외에도 콘솔 · 컴퓨터(NES, 슈퍼패미컴, 메가드라이브, PC 엔진 …)를 에뮬레이션합니다. 그 게임들은 **Software List** 로 정의됩니다 — MAME 의 `hash` 폴더에 있는 시스템별 XML 파일(`hash/nes.xml`, `hash/snes.xml` …)이며, 각 항목은 카트리지 · 디스크 하나와 그에 필요한 정확한 롬 덤프(이름 · 크기 · CRC · SHA-1)를 적어 둡니다. 아케이드 게임의 Dat 파일과 비슷합니다. MAME 는 이 롬을 `roms/<목록>/<소프트웨어>.zip` 으로 찾고, `mame nes smb`(본체 + 소프트웨어)처럼 실행합니다.

**전용 에뮬레이터와 무엇이 다른가.** 전용 에뮬레이터(예: NES 의 Mesen · Nestopia)는 `Super Mario Bros.nes` 같은 파일 하나를 읽습니다. 이 파일 앞에는 카트리지 구성을 알려 주는 작은 **헤더**(iNES 는 16바이트)가 붙어 있습니다. MAME 는 헤더를 쓰지 않습니다 — 기판 정보는 Software List 에서 가져오고, 롬은 **헤더 없는 칩 데이터 그대로**, 보통 칩별로 나눠서 요구합니다. NES 카트리지라면 `nes/smb.zip` 안에 PRG 롬과 CHR 롬이 따로 들어갑니다. 그래서 같은 게임이라도 저장 형태가 다르고, `.nes` 파일을 그대로 두면 MAME 와 맞지 않습니다.

**RomClean 이 하는 일.**

- 원하는 목록을 가져옵니다: 타깃세트 메뉴(⋮) → **Software List…** (또는 타깃세트를 추가할 때 **Software List 포함**). 타깃세트 화면 위쪽의 **머신 | Software List** 로 전환합니다.
- 헤더가 붙은 파일 — `.nes`(NES), `.fds`(패미컴 디스크 시스템), `.a78`(Atari 7800), `.lnx`(Lynx), `.smc` · `.sfc` · `.swc` · `.fig`(슈퍼패미컴), `.pce`(PC 엔진) — 은 스캔할 때 **헤더를 뗀 부분**도 함께 기록합니다. 그래서 Software List 와 맞고, **내보내기**(**Software List 포함**)가 MAME 용 구조로 변환해 씁니다: `.nes` 파일 하나가 PRG · CHR 롬이 든 `nes/<소프트웨어>.zip` 이 됩니다. 원본 파일은 바꾸지 않습니다.
- 지원하지 않는 것: PRG / CHR 외의 여러 칩으로 나눠야 하는 카트리지(예: ColecoVision, 일부 슈퍼패미컴 · 다중 PRG NES 카트리지)와 바이트 순서가 다른 형식(메가드라이브 `.smd`, N64 `.v64`). 이런 파일은 맞지 않는 파일로 남습니다.
- Software List 지원 이전 버전에서 만든 타깃세트에는 Software List 를 추가할 수 없습니다 — 타깃세트를 다시 만드세요.

## 장르 파일 (catver.ini · mature.ini)

장르 필터 · 장르 열 · "성인물 제외" · "아케이드 게임만" 에는 이 파일이 필요합니다. MAME 나 RomClean 에 들어 있지 않으니 직접 내려받습니다.

1. **[Progetto-SNAPS CatVer](https://www.progettosnaps.net/catver/)** 에서 최신 패키지를 내려받습니다 (예: MAME 0.289 용 `pS_CatVer_289.zip`). 사용하는 MAME 와 가장 가까운 버전을 고르세요.
2. 압축을 풉니다. `catver.ini` 는 맨 위 폴더에, `mature.ini` 는 `UI_files/` 폴더에 있습니다.
3. RomClean: 타깃세트 메뉴(⋮) → **장르 파일…** → 각 파일의 **선택…**.

- 내용을 RomClean 의 DB 로 복사하므로, 연결한 뒤에는 파일을 지우거나 옮겨도 됩니다.
- 파일에 없는 clone 은 parent 의 장르를 따릅니다.
- 머신 속성(연도 · 제조사 · 화면 · 플레이어 수)은 Dat 에서 읽습니다. v0.5.3 이전에 만든 타깃세트는 타깃세트 메뉴 → **Dat 다시 읽기…** 로 채웁니다.

## 데이터 저장 위치

| OS | DB · 데이터 폴더 | 설정 (언어 · 테마) |
| --- | --- | --- |
| Linux | `~/.local/share/net.airplanez.flutter.romclean/` | 같은 폴더의 `shared_preferences.json` |
| macOS | `~/Library/Application Support/net.airplanez.flutter.romclean/` | `~/Library/Preferences/net.airplanez.flutter.romclean.plist` |
| Windows | `%APPDATA%\net.airplanez.flutter\romclean\` | 같은 폴더의 `shared_preferences.json` |

- `romclean2.sqlite` — DB: 원본 폴더와 스캔 결과, 타깃세트, 필터, 내보내기 설정, MAME 실행 파일, 장르 데이터.
- `romclean.sqlite` — v0.5.0 의 DB. 이후 버전은 쓰지 않으니 지워도 됩니다.
- Linux 에서 `install-desktop-entry.sh` 를 실행했다면: `~/.local/share/applications/net.airplanez.flutter.romclean.desktop`, `~/.local/share/icons/hicolor/256x256/apps/net.airplanez.flutter.romclean.png`.
- Windows 는 파일 탐색기 주소창에 `%APPDATA%\net.airplanez.flutter` 를 붙여 넣으면 폴더가 열립니다.

## 초기화

**먼저 RomClean 을 종료합니다.** 초기화해도 롬 폴더 · 내보낸 롬셋 · 옮긴 파일은 건드리지 않습니다.

- **빈 DB 로 다시 시작** — 위 데이터 폴더의 `romclean2.sqlite` 를 지웁니다. 원본 폴더 추가 · 스캔 · 타깃세트 추가를 다시 해야 합니다. 언어 · 테마는 유지됩니다.
- **설정 초기화** (언어 · 테마 · 필터 펼침 상태) — 위의 설정 파일을 지웁니다. macOS 는 파일을 지우는 대신 다음을 실행합니다.

  ```bash
  defaults delete net.airplanez.flutter.romclean
  ```

- **전부 초기화** — 둘 다 지웁니다.

  ```bash
  # Linux
  rm -rf ~/.local/share/net.airplanez.flutter.romclean
  # macOS
  rm -rf ~/Library/Application\ Support/net.airplanez.flutter.romclean
  defaults delete net.airplanez.flutter.romclean
  ```

  Windows: `%APPDATA%\net.airplanez.flutter\romclean` 폴더를 지웁니다.

## 삭제

RomClean 을 종료한 뒤:

- **Linux** — 앱 목록에 등록했다면 먼저 `./romclean_v<버전>_linux/install-desktop-entry.sh --uninstall` 을 실행합니다. `romclean_v<버전>_linux` 폴더와 `~/.local/share/net.airplanez.flutter.romclean` 을 지웁니다.
- **macOS** — `romclean.app` 을 휴지통으로 옮기고, `~/Library/Application Support/net.airplanez.flutter.romclean` 을 지운 뒤 `defaults delete net.airplanez.flutter.romclean` 을 실행합니다.
- **Windows** — `romclean_v<버전>_windows` 폴더와 `%APPDATA%\net.airplanez.flutter\romclean` 을 지웁니다 (`%APPDATA%\net.airplanez.flutter` 가 비었으면 그것도).

RomClean 은 이 밖에 시스템에 아무것도 쓰지 않습니다. 롬 · 내보낸 롬셋 · 옮긴 안 맞는 파일은 그대로 남습니다.

## 버전 기록

### v0.5.3
- MAME Software List 지원 (가져오기 · 보유 판정 · 내보내기 · 실행), 헤더가 붙은 롬(`.nes` · `.smc` 등) 인식
- 머신 필터 개선 (기본 줄 + 상세 필터), 장르 필터 (`catver.ini` · `mature.ini`), 연도 · 제조사 · 화면 · 플레이어 수 필터
- 어느 타깃세트에도 맞지 않는 파일을 다른 폴더로 이동 (삭제 없음), 중복 · 안 맞는 파일 용량 표시
- CHD 내보내기를 하드링크로 (디스크 공간 절약), 등록 삭제 확인 창 · 입력칸 지우기 버튼

### v0.5.2
- 7z 읽기 · 쓰기 지원, 내보내기를 항상 TorrentZip · Torrent7z 규격으로
- 내보낸 머신을 목록에서 바로 MAME 로 실행, 내보낸 폴더 열기
- 증분 스캔 · 증분 내보내기, 내보내기 폴더 자동 정리, 원본 변경 감지
- 언어 "System" 기본값, clone 판정을 MAME 와 같게, 새 DB 로 시작 (v0.5.1 변경 포함)

### v0.5.0
- 첫 공개 릴리스 (Linux · macOS · Windows)
- 원본세트 스캔 · 중복 제거, Dat · MAME 실행 파일로 타깃세트 등록 · 보유 상태 판정
- 머신 목록 · 상세 · 필터, split / merged / non-merged 롬셋 내보내기
- Light / Dark 테마, 영어 · 한국어, 정보 탭
