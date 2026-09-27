# 진 여신전생 IV FINAL 한국어 추가 패치 v1.0.0

이 문서는 GitHub 배포 파일 세 가지의 **적용 대상, 한글화 범위, 설치 순서**를 설명합니다. 먼저 아래 표에서 본인의 게임 구동 방식을 고르세요.

| 배포 ZIP | 용도 | 결과 |
| --- | --- | --- |
| `SMT4F_KO_FOR_REPACK_v1.0.0.zip` | 본편 게임을 직접 추출하여 다시 빌드할 때 | 재빌드에 넣을 본편 변경 파일 623개 |
| `SMT4F_KO_LayeredFS_Luma_v1.0.0.zip` | Luma3DS의 게임 패칭으로 본편을 실행할 때 | SD 카드에 복사할 본편 변경 파일 623개 |
| `SMT4F_KO_ExtractedDLC_PythonPatch_v1.0.0.zip` | 별도로 보유한 DLC를 추출해 패치할 때 | 패치된 DLC 추출 폴더. 설치용 CIA는 별도로 빌드해야 함 |

**본편은 앞의 두 ZIP 중 하나만 선택**합니다. 둘은 같은 본편 변경분을 재빌드용과 Luma3DS용으로 포장한 것입니다. DLC를 사용하고 한글화하려면 세 번째 ZIP을 추가로 사용합니다. 본편 패치가 DLC를 자동으로 수정하지는 않습니다.

## 이 패치가 한글화하는 곳

본편 ZIP 두 종류는 기존 **Team Frost 2.0 한국어 패치가 적용된 북미판 UNDUB**을 기준으로 만든 *추가·수정 패치*입니다. 따라서 이 ZIP만 순정 게임에 넣어 전체 한국어판을 만드는 방식이 아닙니다. 기존 번역을 바탕으로 다음 영역의 문구, 표시, 동작을 보강합니다.

- **이야기와 전투:** 이벤트·퀘스트 대사, 악마 대사와 교섭, 전투 이벤트, 동료 관련 메시지.
- **메뉴와 안내:** 야영지, 퀘스트 센터, 상점, 아이템, 상태, 저장·불러오기, 합체, 타이틀 등의 텍스트와 용어.
- **화면 그래픽:** 지도, 전투 메뉴, 상태창, 레벨업, 크레딧 등 이미지 안에 들어 있는 글자와 표시. 일부 영상 파일도 변경 대상에 포함됩니다.
- **실행 코드와 글꼴:** 한글 이름 입력 및 일부 화면 문구·표시에 필요한 `code.bin`, `DecryptedExHeader.bin`/`exheader.bin`, 한글 글꼴 `ko.bcfnt` 등을 포함합니다. 코드와 헤더는 반드시 한 세트로 적용하세요.

본편 배포물의 파일 기준 변경량은 **기존 파일 수정 622개 + 새 파일 1개 = 623개**입니다. 파일 수는 번역된 문장 수나 한글화율을 뜻하지 않습니다. 모든 게임 화면과 모든 미사용 문자열이 한국어라고 보장하는 수치도 아닙니다.

DLC ZIP은 **DLC 추출본의 37개 파일**을 수정합니다. DLC 콘텐츠의 대사·퀘스트·아이템 관련 텍스트와 오역·용어를 보강하며, 변경 대상에는 `DecryptedApp.*`, 매뉴얼·다운로드 플레이용 파일과 그 추출 테이블이 포함됩니다. DLC의 모든 파일을 바꾸는 패치는 아니며, **본편용 ZIP만 설치하면 DLC 변경분은 적용되지 않습니다.**

## 시작 전 준비

1. 본인이 보유한 게임과 DLC에서 직접 준비한 파일을 사용하세요. 세 ZIP은 완성된 본편 `.3ds`나 DLC `.cia`가 아닙니다.
2. 기존 Team Frost 2.0 패치와 자신의 추출 폴더 또는 SD 카드 내용을 **별도 위치에 백업**하세요. 재빌드 방식이라면 원본 추출 폴더도 보존하세요.
3. 세 ZIP을 각각 압축 해제하세요. Windows 탐색기의 **모두 압축 풀기**를 사용해도 됩니다. 압축을 풀면 ZIP 내부의 최상위 폴더 이름을 아래 예시와 비교하세요.
4. 본편 게임의 지역·UNDUB 구성·Team Frost 2.0 버전이 기준과 다르면 화면이 달라지거나 실행되지 않을 수 있습니다. 특히 다른 지역판에 같은 파일을 무작정 덮어쓰지 마세요.

### 본편 기준에 관하여

제작 기준은 **북미판(USA) UNDUB 본편에 Team Frost `SMT4Final 2.0`의 RomFS 한국어 패치를 적용한 상태**입니다. 프로젝트 문서에 기록된 원본 본편 파일의 예시 SHA-256은 다음과 같습니다.

```text
Shin_Megami_Tensei_IV_Apocalypse(decrypted).3ds
afeaae1b41880dd91b9f2e8a4ce58741707f500f5e8e658e57e419d9d56d9b79
```

이 해시는 *제작에 쓰인 원본 파일 예시*입니다. 기존 패치를 입힌 후 재빌드한 파일의 해시와 혼동하지 마세요. `FOR_REPACK` ZIP은 적용 전 파일을 자동 검사하지 않으므로 특히 기준을 직접 확인해야 합니다.

## 사전 준비 1: 본편 `.3ds`와 DLC `.cia` 복호화·추출

**복호화**는 암호화된 게임 이미지가 추출 도구에서 읽히도록 만드는 단계이고, **추출**은 복호화된 이미지 안의 `RomFS`·`ExeFS` 등을 폴더로 푸는 단계입니다. 이미 본인이 준비한 파일이 복호화되어 있고 아래 해시까지 일치한다면 복호화를 다시 할 필요가 없습니다. 복호화한 파일도 본인이 보유한 게임에서 준비한 것만 사용하세요.

### 1-1. Batch CIA 3DS Decryptor로 복호화

1. [Batch CIA 3DS Decryptor 제작자의 배포 글](https://gbatemp.net/threads/batch-cia-3ds-decryptor-a-simple-batch-file-to-decrypt-cia-3ds.512385/)에서 **완전한 배포 폴더**를 받아 압축 해제합니다. `.bat` 파일만 떼어 쓰지 말고 함께 제공된 실행 파일을 같은 폴더에 둡니다. [원본 스크립트](https://github.com/matiffeder/3DS-stuff/blob/master/Batch%20CIA%203DS%20Decryptor.bat)는 `.3ds`와 `.cia`를 처리하고, 별도 [Batch CIA CCI Decryptor](https://github.com/rcyggdra/decryptor)는 이름과 출력 방식이 다른 후속 구현입니다. 이 문서의 파일명 예시는 **원본 Batch CIA 3DS Decryptor** 기준입니다.
2. 본편 `.3ds`와 DLC `.cia`의 **복사본**을 Decryptor의 `.bat`가 있는 폴더에 넣습니다. 원본은 다른 곳에 보관합니다. 혼동을 줄이려면 본편과 DLC를 **한 번에 하나씩** 처리하세요.
3. `Batch CIA 3DS Decryptor.bat`를 실행하고 `Finished`가 표시될 때까지 기다립니다. 큰 본편 파일은 시간이 걸릴 수 있습니다. 창에 오류가 나거나 결과가 보이지 않으면 같은 폴더의 `log.txt`를 확인합니다.
4. 결과 파일을 확인합니다. 원본 스크립트는 본편에 `원래이름-decrypted.3ds`, DLC에 `원래이름 (DLC)-decrypted.cia` 형태의 파일을 만듭니다. 이미 복호화한 파일은 건너뛰거나 결과 이름이 다를 수 있습니다. **이름만 바꿔도 암호화가 풀리는 것은 아닙니다.**
5. 이 패치의 기준과 맞는지 PowerShell에서 SHA-256을 확인합니다. 파일 경로는 본인의 결과 파일로 바꾸세요.

   ```powershell
   Get-FileHash -Algorithm SHA256 "D:\Games\base-decrypted.3ds"
   Get-FileHash -Algorithm SHA256 "D:\Games\dlc-decrypted.cia"
   ```

   제작에 사용한 복호화된 본편 예시 해시는 `afeaae1b41880dd91b9f2e8a4ce58741707f500f5e8e658e57e419d9d56d9b79`, DLC 기준 해시는 `ee53472150a3bb58a43673ff85fc5d1658ccae9430d949f22673bf7d5dbdd201`입니다. 해시가 다르면 지역·UNDUB·DLC 구성 또는 도구 출력이 다른 것이므로 다음 단계에 억지로 적용하지 마세요.

### 1-2. HackingToolkit3DS V9로 본편 추출·재빌드

[HackingToolkit3DS V9](https://github.com/Cyanol/HackingToolkit3DS)는 **복호화 도구가 아니라 복호화된 이미지를 추출·재빌드하는 도구**입니다. 도구와 설정 파일이 들어 있는 작업 폴더를 준비하고, 복호화한 본편 `.3ds`의 복사본을 그 폴더에 넣습니다. 도구 설명에 따라 게임 파일 이름은 영문·숫자 위주로 짧게 만들고 공백·특수문자를 피하세요. 파일 이름을 바꾸어도 내용의 SHA-256은 달라지지 않습니다.

1. `HackingToolkit3DS.exe`를 실행합니다. 메뉴의 **`D`는 `.3ds` 추출**, **`R`은 `.3ds` 재빌드**입니다.
2. `D`를 누르고, `Enter the name of your decrypted .3DS file (Without extension)`에는 **확장자 `.3ds`를 뺀 파일명**만 입력합니다. 예: `smt4f_base.3ds`라면 `smt4f_base`.
3. `Decompress the code.bin file (n/y)?`가 나오면 선택한 값을 메모해 두고, Team Frost 적용본을 다시 추출할 때도 같은 설정을 사용합니다. 이 프로젝트의 기준 `code.bin`과 일치하는지 아래 사전 준비 2의 해시로 최종 확인하세요.
4. `Extraction done!`이 표시되면 `ExtractedRomFS/`, `ExtractedExeFS/code.bin`, `DecryptedExHeader.bin`이 생성되었는지 확인합니다. 이 파일들은 **도구 작업 폴더의 추출 결과**입니다. 다른 게임을 같은 폴더에서 연속 추출하면 이전 산출물이 섞일 수 있으므로 게임마다 깨끗한 작업 폴더를 쓰세요.
5. 추출본의 `ExtractedRomFS/`에 파일을 병합한 뒤 재빌드할 때는 `R`을 누르고, 결과 파일의 **확장자 없는 새 이름**을 입력합니다. V9는 보통 `<입력한 이름>_Edited.3ds`를 만듭니다. 재빌드가 끝난 뒤 새 파일이 생성되었는지 확인하세요. 이 절차를 Team Frost 2.0을 만들 때 한 번, 아래 방법 A의 추가 패치를 넣은 뒤 한 번 사용합니다.

V9가 추출한 `DecryptedRomFS.bin`과 새로 생성되는 `CustomRomFS.bin`은 역할이 다릅니다. `ExtractedRomFS/`를 바꾼 뒤에는 반드시 **새 RomFS를 빌드**해야 수정 내용이 이미지에 들어갑니다. [V9 메뉴·재빌드 코드](https://github.com/Cyanol/HackingToolkit3DS/blob/master/PackEnglishV9/HackingToolkit3DS.bat)를 참고하세요.

### 1-3. DLC CIA 추출

1. 앞의 Decryptor로 만든 DLC `.cia`의 해시가 위 DLC 기준과 일치하는지 먼저 확인합니다.
2. DLC CIA의 **복사본**을 별도의 HackingToolkit3DS 작업 폴더에 두고, `HackingToolkit3DS.exe`의 **`CE` (`.cia` 추출)**를 선택합니다. 파일명 입력에는 `.cia` 확장자를 뺀 이름만 입력합니다. `code.bin` 압축 해제 질문이 나오면 앞서 선택한 값을 기록합니다.
3. 추출 후 `DecryptedApp.0003.00000003` 같은 콘텐츠 파일들, `DecryptedManual.bin`, `DecryptedDownloadPlay.bin`, `ExtractedManual/`, `ExtractedDownloadPlay/`가 생성되었는지 확인하고 작업 폴더 전체를 `ExtractedDLC_Base/`로 보존합니다. 그런 다음 아래 방법 C의 `--check`로 실제 패치 기준과 일치하는지 검사합니다.

**이 프로젝트에서 확인한 DLC 흐름:** 복호화된 기준 DLC CIA는 HackingToolkit3DS의 `CE`로 실제 추출할 수 있습니다. 추출 결과에서 위 파일들과 `HeaderNCCH1.bin`, `HeaderNCCH2.bin`을 확인하세요. CIA 재빌드는 HackingToolkit3DS의 `CR` 대신 별도 `SMT4F_KO_DLC_Patch_v1.0.0.zip`에 든 `tools/`와 `BUILD_DLC_CIA.bat`를 사용합니다. HackingToolkit3DS V9의 일반 설명에는 DLC 지원 제한이 적혀 있지만, 여기서는 **`CE` 추출 가능 여부와 `CR` 재빌드 지원 여부를 구분**해야 합니다. DLC Python 패치의 `--check`가 실패하면 기준 파일 차이도 함께 확인하세요.

## 사전 준비 2: Team Frost 2.0 본편 기준 만들기

Team Frost 2.0은 진 여신전생 마이너 갤러리의 [진여신전생 4F 한글패치 경로 안내](https://gall.dcinside.com/mgallery/board/view/?id=megaten&no=47112)를 통해 준비합니다. 이 글은 갤러리의 [정보·공략 모음](https://gall.dcinside.com/mgallery/board/view/?id=megaten&no=6135)에도 연결되어 있습니다. 글과 배포 링크는 바뀔 수 있으므로 **`SMT4Final 2.0` 버전인지** 확인하세요. Team Frost 배포 파일의 구체적인 최상위 폴더 이름은 압축본마다 다를 수 있으므로, 아래의 `RomFS` 상대 경로를 기준으로 적용합니다.

**본편 재빌드 방식의 전체 순서:** 복호화된 북미판 UNDUB `.3ds` → HackingToolkit3DS `D`로 추출 → Team Frost 2.0의 RomFS 변경분 병합 → `R`로 재빌드 → 그 결과를 다시 `D`로 추출해 `Extracted_Base/` 보존 → 아래 방법 A의 `FOR_REPACK` 변경분 병합 → 다시 `R`로 최종 재빌드.

1. 사전 준비 1-2에서 추출한 **순정 UNDUB 본편 추출 폴더**를 백업합니다.
2. Team Frost 2.0 ZIP을 압축 해제하고 그 안에서 게임 `RomFS`용 파일들이 들어 있는 폴더를 찾습니다. 배포본 설명에서 `romfs/`, `RomFS/` 또는 `ExtractedRomFS/`로 표시될 수 있습니다. **그 폴더 안의 파일과 하위 폴더**를 HackingToolkit3DS 작업 폴더의 `ExtractedRomFS/`에 병합합니다. 같은 경로의 파일은 교체하고, 기존 `ExtractedRomFS/` 폴더 자체를 통째로 삭제하지 않습니다. ZIP에 별도 적용 안내가 있으면 그 안내의 파일 구성도 확인하세요.
3. 한글 패치 파일이 실제로 `ExtractedRomFS/` 아래에 들어갔는지 확인하고, HackingToolkit3DS 메뉴 `R`로 Team Frost 2.0 적용본 `.3ds`를 새 이름으로 빌드합니다.
4. **새 작업 폴더**에서 방금 빌드한 Team Frost 적용본을 `D`로 다시 추출합니다. 추출 결과 폴더를 `Extracted_Base/`로 보존하세요. 이것이 아래 방법 A에서 623개 변경 파일을 받을 **기준 폴더**입니다.
5. 기준이 맞는지 다음 두 파일의 SHA-256을 확인할 수 있습니다. 단, 이 두 해시만 맞는다고 전체 RomFS가 동일하다는 뜻은 아닙니다.

   ```text
   Extracted_Base/ExtractedExeFS/code.bin
   b54c3a31c5a59f7c9f82318dbdde0d1796414d3b33eafb04468c5f10581e7b42

   Extracted_Base/DecryptedExHeader.bin
   3515e53615b48591cd6625237df370b6dc48c11e9fc46bb7303b0cf2bed552d0
   ```

   두 파일은 PowerShell에서 `Get-FileHash -Algorithm SHA256 "파일경로"`로 확인할 수 있습니다. 전체 기준과의 호환성을 자동 확인하려면 이 문서의 세 ZIP과는 별도인 `SMT4F_KO_Extracted_PythonPatch_v1.0.0.zip`의 `--check` 기능을 사용할 수 있습니다.

**Luma3DS 방식**을 선택한 사용자는 Team Frost 2.0을 본편에 재빌드할 필요가 없습니다. Team Frost의 LayeredFS 파일을 먼저 `SD:/luma/titles/000400000019A200/`에 설치한 뒤, 아래 방법 B의 추가 ZIP을 같은 경로에 병합하세요.

## 방법 A: 본편을 직접 재빌드하기 — `FOR_REPACK`

**대상:** 본편을 HackingToolkit3DS 등으로 추출하고 재빌드하는 사용자. Luma3DS용 ZIP은 이 절차에 필요하지 않습니다.

압축 해제 후 구조는 다음과 같습니다.

```text
SMT4F_KO_FOR_REPACK_v1.0.0/
├─ patch/
│  ├─ DecryptedExHeader.bin
│  ├─ ExtractedExeFS/code.bin
│  └─ ExtractedRomFS/...
├─ manifest.csv
└─ SUMMARY.txt
```

`patch` 폴더는 **추출 폴더의 루트에 합쳐 넣는 변경분**입니다. `manifest.csv`는 파일 목록과 해시를 기록한 참고 자료이며 설치 프로그램이 아닙니다.

1. 위 **사전 준비 2**까지 진행해 Team Frost 2.0 적용본을 재추출한 `Extracted_Base/`를 준비합니다. `DecryptedExHeader.bin`, `ExtractedExeFS/code.bin`, `ExtractedRomFS/`가 있는지 확인합니다.
2. 추출 결과를 다른 폴더로 **통째로 복사**해 작업본을 만듭니다. 예: 원본 `Extracted_Base/`, 작업본 `Extracted_KO/`. 이후 작업은 `Extracted_KO/`에서만 합니다.
3. ZIP 안의 **`patch` 폴더를 열고**, 그 안의 `DecryptedExHeader.bin`, `ExtractedExeFS`, `ExtractedRomFS`를 `Extracted_KO/` 안으로 복사합니다. 같은 이름의 파일을 **덮어쓰고 폴더는 병합**합니다. `ExtractedRomFS` 전체를 지우고 `patch/ExtractedRomFS`로 바꾸면 기존 게임 파일이 빠지므로 그렇게 하지 마세요.
4. 완료 후 최소한 아래 구조인지 확인합니다.

   ```text
   Extracted_KO/
   ├─ DecryptedExHeader.bin        ← 이번 패치로 교체
   ├─ ExtractedExeFS/code.bin      ← 이번 패치로 교체
   └─ ExtractedRomFS/
      ├─ font/ko.bcfnt             ← 이번 패치로 추가
      └─ ...                       ← 기존 파일과 변경 파일이 함께 존재
   ```

5. **패치한 작업본에서 RomFS·ExeFS를 새로 생성**해 본편을 재빌드합니다. 예전에 만든 `CustomRomFS.bin`, `CustomExeFS.bin`, `CustomPartition*.bin`이나 이전 `.3ds`를 재사용하면 이번 수정이 빠질 수 있습니다. 사용 중인 추출·재빌드 도구의 절차에 따라 새 결과물을 만드세요.
6. 새로 빌드한 게임을 실행해 타이틀, 대사, 메뉴, 이름 입력 등을 확인합니다. 기존 실행 상태를 담은 에뮬레이터 세이브스테이트 대신 게임을 새로 시작하여 코드 변경을 확인하세요.

**되돌리기:** 백업한 추출 폴더에서 다시 빌드합니다. 작업본에 파일만 역으로 복사하는 것보다 백업에서 새로 시작하는 편이 추가 파일까지 확실하게 정리됩니다.

## 방법 B: Luma3DS에서 본편 실행하기 — `LayeredFS_Luma`

**대상:** Luma3DS 게임 패칭을 사용하는 3DS. 본편을 다시 빌드할 필요는 없습니다. 이 ZIP은 기존 Team Frost 2.0 LayeredFS 설치 위에 **추가로 병합**하는 파일입니다.

1. SD 카드의 `luma/titles/000400000019A200/` 아래에 기존 Team Frost 2.0 패치의 `romfs/`와 `code.bin`이 있는지 확인합니다. 그 폴더를 PC에 백업합니다.
2. `SMT4F_KO_LayeredFS_Luma_v1.0.0.zip`을 압축 해제합니다. 안쪽에는 `luma/` 폴더와 설명·매니페스트 파일이 있습니다.
3. ZIP 안의 **`luma` 폴더 전체를 SD 카드의 최상위 위치**에 복사합니다. Windows가 묻는 같은 이름의 폴더는 **병합**, 같은 이름의 파일은 **교체**합니다. 기존 `luma/titles/000400000019A200/romfs/`를 먼저 삭제하면 Team Frost 2.0의 나머지 파일이 사라지므로 삭제하지 마세요.
4. 복사 후 아래 경로를 확인합니다. SD 카드 드라이브 문자는 PC마다 다릅니다.

   ```text
   SD:/luma/titles/000400000019A200/
   ├─ code.bin
   ├─ exheader.bin
   └─ romfs/
      ├─ font/ko.bcfnt
      └─ ...
   ```

5. 3DS를 끈 다음 **SELECT를 누른 채 전원을 켜서** Luma 설정 화면을 엽니다. `Enable game patching`을 켜고 **START**로 저장합니다.
6. 본편을 실행해 표시를 확인합니다. 게임의 실제 타이틀 ID가 `000400000019A200`이 아닌 경우 해당 폴더가 적용되지 않습니다. 다른 지역판은 단순히 폴더 이름만 바꿔 호환된다고 보장할 수 없습니다.

**되돌리기:** 백업한 Team Frost 2.0 폴더를 복원하고 이 추가 패치의 `exheader.bin`을 제거합니다. 기존 Team Frost 파일을 다시 덮어쓰는 것만으로 새로 추가된 파일이 자동 삭제되지는 않습니다.

## 방법 C: DLC 추출본 패치하기 — `ExtractedDLC_PythonPatch`

**대상:** 별도로 보유한 북미판 DLC를 HackingToolkit3DS로 추출한 사용자. 본편을 A 또는 B 방식으로 설치한 뒤 필요한 경우 진행합니다. 이 ZIP에는 완성 DLC CIA가 들어 있지 않습니다.

### DLC 기준 파일

제작 기준은 아래 DLC 파일을 추출한 `ExtractedDLC_Base/`입니다. **본편과 달리 DLC에는 Team Frost 2.0 RomFS를 미리 적용하지 않습니다.**

```text
Shin Megami Tensei IV - Apocalypse (USA) (DLC) decrypted.cia
SHA-256: ee53472150a3bb58a43673ff85fc5d1658ccae9430d949f22673bf7d5dbdd201
```

ZIP 내부에는 `APPLY_PATCH.bat`, `apply_patch.py`, `patch_data.zip`, `README_KO.txt`가 있습니다. 네 파일을 **같은 폴더에 둔 채** 사용하세요. Windows에서는 Python 3 설치가 필요합니다. 설치 후 명령 프롬프트에서 `py -3 --version`으로 확인할 수 있습니다. 별도 Python 패키지나 xdelta 실행 파일은 필요하지 않습니다.

### 적용 순서

1. 위 **사전 준비 1-3**에 따라 DLC CIA를 추출해 `ExtractedDLC_Base/` 폴더를 준비합니다. 예를 들어 그 안에 `DecryptedApp.0003.00000003`, `DecryptedManual.bin`, `ExtractedManual/` 등이 있어야 합니다. 기준 폴더는 백업하고 수정하지 않습니다.
2. 압축 해제한 DLC 패치 폴더에서 `APPLY_PATCH.bat`를 실행합니다.
3. `Baseline folder:`에는 **기준 추출 폴더**의 전체 경로를 입력합니다. 예: `D:\Games\ExtractedDLC_Base`.
4. `Output folder:`에는 **새로 만들 결과 폴더**의 전체 경로를 입력합니다. 예: `D:\Games\ExtractedDLC`. 같은 드라이브에 두고, 아직 존재하지 않는 경로를 쓰는 것이 편합니다. 그냥 Enter를 누르면 기준 폴더 옆의 `ExtractedDLC`를 제안합니다.
5. 패처가 37개 대상의 크기·SHA-256을 검사하고, 기준 폴더 전체를 결과 폴더로 복사한 뒤 델타를 적용합니다. 마지막에 다음 문구가 나와야 성공입니다.

   ```text
   Applied and verified 37/37 files
   Patch complete: <결과 폴더 경로>
   ```

6. 결과 `ExtractedDLC/`는 **패치된 추출 파일 폴더**입니다. 이것만으로 DLC 설치가 끝나지 않습니다. DLC CIA까지 만들려면 아래의 별도 `SMT4F_KO_DLC_Patch_v1.0.0.zip` 절차를 따르세요.

### DLC CIA 재빌드 — 별도 `SMT4F_KO_DLC_Patch_v1.0.0.zip`

`dist`에 있는 이 ZIP은 위 세 가지 주요 배포 ZIP과 **별도 파일**입니다. 이 ZIP에는 DLC용 변경 파일 `patch/`, 재빌드 데이터 `rebuild/`, `tools/3dstool.exe`, `tools/makerom.exe`, `BUILD_DLC_CIA.bat`, `build_dlc_cia.ps1`, `MANIFEST_DLC.json`이 들어 있습니다. 필요한 경우 GitHub 배포에 이 ZIP도 함께 올려야 아래 CIA 생성 절차를 사용할 수 있습니다.

1. `SMT4F_KO_DLC_Patch_v1.0.0.zip`을 압축 해제하고 내부 폴더 구성을 그대로 둡니다.
2. `BUILD_DLC_CIA.bat`를 실행합니다. **기준 폴더** 질문에는 `HeaderNCCH1.bin`이 들어 있는, 수정하지 않은 `ExtractedDLC_Base/`의 전체 경로를 입력합니다.
3. **출력 폴더** 질문에는 CIA를 저장할 폴더를 입력합니다. Enter만 누르면 배포 폴더의 `out/`을 사용합니다. 정상 완료 시 그 폴더에 `smt4a_dlc_ko.cia`가 만들어집니다. 이미 같은 이름의 CIA가 있으면 중단하므로 기존 파일을 먼저 별도 위치에 보관하세요.
4. 생성된 CIA를 본인의 3DS 또는 에뮬레이터 환경에 설치한 뒤 DLC 장면을 확인합니다.

**입력 폴더를 구분하세요.** 이 `BUILD_DLC_CIA.bat`는 Python 패치 결과인 `ExtractedDLC/`를 입력받아 다시 묶는 프로그램이 아닙니다. **원본 `ExtractedDLC_Base/`와 자기 ZIP 안의 `patch/`**를 읽고 해시를 검사한 뒤 CIA를 만듭니다. 따라서 DLC Python 패치는 패치된 추출 폴더가 필요할 때 쓰고, `SMT4F_KO_DLC_Patch_v1.0.0.zip`은 설치용 CIA가 필요할 때 **같은 원본 기준 폴더에서 별도로** 실행하면 됩니다. 두 방식을 순서대로 중복 적용할 필요는 없습니다.

명령행을 선호한다면 패치 폴더에서 다음과 같이 실행할 수 있습니다. 경로는 본인 PC에 맞게 바꾸세요.

```powershell
py -3 apply_patch.py "D:\Games\ExtractedDLC_Base" "D:\Games\ExtractedDLC" --check
py -3 apply_patch.py "D:\Games\ExtractedDLC_Base" "D:\Games\ExtractedDLC"
```

첫 줄의 `--check`는 기준 파일 호환성만 검사하고 결과 폴더를 만들지 않습니다. 둘째 줄은 실제 적용입니다. 결과 폴더가 이미 있으면 기본값으로 중단합니다. `--force`는 **지정한 결과 폴더를 통째로 삭제**하므로, 이름이 겹치면 다른 새 출력 경로를 사용하는 편이 안전합니다.

### 오류가 나면

| 메시지 | 뜻과 조치 |
| --- | --- |
| `Missing baseline file` | 기준 추출 폴더에 필요한 파일이 없습니다. DLC 추출을 다시 확인하세요. |
| `Baseline size mismatch` / `Baseline SHA-256 mismatch` | 지역판·버전·기존 수정 상태가 제작 기준과 다릅니다. 위 DLC 기준과 원본 추출 상태를 확인하세요. |
| `Missing patch data` | `patch_data.zip`이 `apply_patch.py` 옆에 없습니다. ZIP을 다시 온전히 압축 해제하세요. |
| `Output already exists` | 새 결과 폴더 이름을 선택하거나 기존 결과를 안전하게 백업한 후 다시 시도하세요. |
| `Python 3 was not found` | Python 3을 설치하고 `py -3 --version` 또는 `python --version`을 확인하세요. |

`ERROR:`가 나오면 적용 완료로 취급하지 마세요. 기준 폴더는 패처가 수정하지 않으므로 원인을 바로잡은 뒤 새 결과 경로로 재시도할 수 있습니다.

## 마지막 확인

- [ ] 본편에서 **재빌드(A) 또는 Luma3DS(B) 중 한 방법**을 선택했다.
- [ ] 필요한 경우 본편 `.3ds`와 DLC `.cia`를 복호화한 뒤 SHA-256을 확인했다.
- [ ] 본편의 기준이 북미판 UNDUB + Team Frost 2.0인지 확인했다.
- [ ] `code.bin`과 `DecryptedExHeader.bin` 또는 `exheader.bin`을 함께 적용했다.
- [ ] DLC가 필요하면 별도 DLC 패치의 `37/37` 완료 문구를 확인했다.
- [ ] 재빌드 또는 SD 카드 복사 후 실제 게임에서 이야기·전투·메뉴·이름 입력과 사용하는 DLC 장면을 확인했다.

배포 ZIP의 파일 구성과 정적 검증만으로 모든 게임 장면의 실제 표시를 보증할 수는 없습니다. 문제가 생기면 사용한 방식, 본편·DLC 기준 버전, 오류 문구, 화면 위치를 함께 기록하면 원인을 찾기 쉽습니다.

## 글꼴 출처·저작권 및 라이선스 안내

- 이 추가 패치의 **일부 한국어 그래픽을 제작할 때 나눔명조 계열 글꼴**을 사용했습니다. 나눔명조 글꼴의 권리는 해당 저작권자에게 있으며, 글꼴 소프트웨어는 [SIL Open Font License 1.1](https://github.com/google/fonts/blob/main/ofl/nanummyeongjo/OFL.txt)에 따라 제공됩니다. 글꼴 파일 자체를 별도로 재배포한다면 저작권 고지와 라이선스 전문 등 해당 조건을 함께 확인하고 준수해야 합니다. 그래픽 이미지에 글꼴을 사용했다는 사실만으로 게임 자료나 이 패치 전체가 OFL 1.1로 배포되는 것은 아닙니다.
- **진 여신전생 IV FINAL의 게임 자료·이름·상표, Team Frost 2.0의 기존 번역·패치, 이 추가 패치의 독자적 작업물은 각각 권리 관계가 다릅니다.** 이 문서는 게임 원저작권자나 Team Frost의 승인·후원을 주장하지 않으며, 그들의 권리 또는 이용 허락을 대신 부여하지 않습니다.
- 이 README는 패치의 적용 방법을 설명합니다. **이 추가 패치 전체에 대한 독립적인 오픈소스 라이선스나 재배포 허락은 이 문서만으로 선언하지 않습니다.** GitHub에 ZIP을 공개하기 전에는 각 ZIP에 들어 있는 게임 유래 파일, 기존 패치 자료, 글꼴 파일, 재빌드 도구의 권리와 배포 조건을 각각 확인해야 합니다. 출처 표기나 면책 문구만으로 필요한 허락이 생기지는 않습니다.
- 패치는 사용자의 기준 파일과 실행 환경에 따라 동작이 달라질 수 있습니다. 적용 전에 원본 게임·DLC·세이브를 백업하세요. 배포자는 모든 환경에서의 정상 작동이나 데이터 손실 방지를 보증하지 않습니다. 관련 법령과 원본 게임·각 도구의 이용 조건을 지키는 책임은 각 이용자에게 있습니다.
