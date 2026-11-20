# RomClean

A desktop app for managing MAME ROMs and building romsets (Linux · macOS · Windows).

> RomClean does not provide any ROMs. It only manages files you already own.

- Scans your ROM folders **without changing them** and records what you have.
- Register a MAME Dat (`mame -listxml`, or pick the MAME executable) to see which machines are complete, partial, or missing.
- Export zip romsets in `split`, `merged`, or `non-merged` format only when you need them.
- Supports ROMs, CHDs, samples, and `nodump` / `baddump`.
- Optional duplicate removal — the only feature that modifies your files.

## Download & install

No installer. Extract and run. Replace `0.5.0` with the version you downloaded.

### Linux (x64) — `romclean_v0.5.0_linux.tar.gz`

```bash
tar -xzf romclean_v0.5.0_linux.tar.gz
./romclean_v0.5.0_linux/romclean
```

- Requires the GTK 3 runtime (installed by default on most desktop distributions).
- To add RomClean to the app list with its icon (optional):
  `./romclean_v0.5.0_linux/install-desktop-entry.sh` (remove with `--uninstall`).
  Run it again if you move the folder.

### macOS (12 or later, Apple Silicon · Intel) — `romclean_v0.5.0_macos.zip`

1. Double-click the zip to extract `romclean.app`.
2. Move it to `Applications` (optional) and open it.

The app is signed and notarized by Apple.

### Windows (x64) — `romclean_v0.5.0_windows.zip`

1. Right-click the zip → **Extract All**.
2. Open the `romclean_v0.5.0_windows` folder and run `romclean.exe`.

- Keep all files in the folder together — `romclean.exe` does not run on its own.
- The app is not code-signed. If Windows shows "Windows protected your PC", click **More info → Run anyway**.

---

# RomClean (한국어)

MAME 롬을 관리하고 롬셋을 만드는 데스크톱 앱입니다 (Linux · macOS · Windows).

> RomClean 은 롬을 제공하지 않습니다. 사용자가 보유한 파일만 관리합니다.

- 롬 폴더를 **변경하지 않고** 스캔해 보유 현황을 기록합니다.
- MAME Dat(`mame -listxml`, 또는 MAME 실행 파일 선택)를 등록하면 머신별 완전 · 일부 누락 · 전체 누락을 보여 줍니다.
- 필요할 때만 `split` · `merged` · `non-merged` 형식의 zip 롬셋으로 내보냅니다.
- 롬 · CHD · 샘플 · `nodump` / `baddump` 를 지원합니다.
- 중복 제거(선택 기능) — 파일을 변경하는 유일한 기능입니다.

## 내려받기 · 설치

설치 프로그램이 없습니다. 압축을 풀어 바로 실행합니다. `0.5.0` 은 내려받은 버전으로 바꿔 읽어 주세요.

### Linux (x64) — `romclean_v0.5.0_linux.tar.gz`

```bash
tar -xzf romclean_v0.5.0_linux.tar.gz
./romclean_v0.5.0_linux/romclean
```

- GTK 3 런타임이 필요합니다 (대부분의 데스크톱 배포판에 기본 설치되어 있습니다).
- 앱 목록에 아이콘과 함께 등록하려면 (선택):
  `./romclean_v0.5.0_linux/install-desktop-entry.sh` (제거는 `--uninstall`).
  폴더를 옮긴 뒤에는 다시 실행합니다.

### macOS (12 이상, Apple Silicon · Intel) — `romclean_v0.5.0_macos.zip`

1. zip 을 더블클릭해 `romclean.app` 을 꺼냅니다.
2. `응용 프로그램` 폴더로 옮긴 뒤(선택) 실행합니다.

Apple 의 서명과 공증을 받은 앱입니다.

### Windows (x64) — `romclean_v0.5.0_windows.zip`

1. zip 을 마우스 오른쪽 버튼으로 눌러 **압축 풀기**를 합니다.
2. `romclean_v0.5.0_windows` 폴더의 `romclean.exe` 를 실행합니다.

- 폴더 안의 파일을 모두 함께 두어야 합니다. `romclean.exe` 만 따로 옮기면 실행되지 않습니다.
- 코드 서명이 없는 앱입니다. "Windows의 PC 보호" 창이 나오면 **추가 정보 → 실행**을 누릅니다.
