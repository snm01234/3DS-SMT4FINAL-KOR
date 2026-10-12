# 진 여신전생 IV FINAL 한국어 추가 패치 v1.1.1

**Team Frost 2.0 한국어 패치를 기반으로 미번역 요소를 보완하고, 한글 입력 및 각종 UI를 개선한 추가 패치입니다.**

- **지원 게임:** Shin Megami Tensei IV: Apocalypse (북미판 UNDUB)
- **필수 선행 패치:** Team Frost `SMT4Final 2.0`
- **지원 방식:** 3DS/CIA 재빌드, Luma3DS LayeredFS, DLC CIA 생성
- **현재 버전:** v1.1.1

> **중요:** 이 패치는 독립적인 완전 한국어 패치가 아닙니다. 본편에는 반드시 Team Frost 2.0을 먼저 적용해야 합니다. DLC는 별도로 패치해야 합니다.
>
> 이전 v1.0.0 또는 v1.1.0 추가 패치를 먼저 설치할 필요는 없습니다. v1.1.1은 추가 패치와 배포 도구의 버전이며 게임 내부 버전을 변경하지 않습니다.

---

## 1. 주요 한글화 내용

| 구분 | 개선 내용 |
|---|---|
| 스토리·전투 | 이벤트, 퀘스트, 악마 대화·교섭, 동료 메시지 등의 번역 보완 |
| 메뉴·시스템 | 상점, 아이템, 저장·불러오기, 합체, 상태창 등의 미번역 및 오역 수정 |
| 그래픽·UI | 지도, 전투 화면, 레벨업, 타이틀, 크레딧, 엇갈림 통신 등의 한글화 |
| 한글 입력 | 주인공 이름 한글 입력 및 관련 코드 개선 |
| DLC | DLC 대사, 퀘스트, 아이템, 스킬명 및 설명 교정 |

그 외 영문 UI, 지도 INFO, 전투 알림, 각종 용어와 선택지 표시를 개선하고 일부 영상 및 실행 코드도 수정했습니다.

기존 번역을 기반으로 추가·수정한 패치이므로 모든 게임 화면과 미사용 문자열의 완전한 한국어화를 보장하지는 않습니다.

## 2. 어떤 파일을 받아야 하나요?

| 배포 파일 | 용도 |
|---|---|
| `SMT4F_KO_FOR_REPACK_v1.1.1.zip` | 본편을 직접 추출하고 다시 빌드할 때 |
| `SMT4F_KO_LayeredFS_Luma_v1.1.1.zip` | Luma3DS 게임 패칭으로 실행할 때 |
| `SMT4F_KO_DLC_Patch_v1.1.1.zip` | 한국어 DLC CIA를 생성할 때 |
| `SMT4F_KO_Main_DLC_Builder_v1.1.1.zip` | 패치 완료된 본편·DLC를 3DS/CIA로 재빌드할 때 |

**실행 환경에 따라 선택하세요.**

- **3DS 실기 + Luma3DS:** `LayeredFS_Luma`
- **에뮬레이터 또는 직접 ROM 재빌드:** `FOR_REPACK`
- **DLC도 한글화할 경우:** `DLC_Patch` 추가
- **통합 재빌드 도구가 필요할 경우:** `Main_DLC_Builder` 추가

본편용 `FOR_REPACK`과 `LayeredFS_Luma`는 동일한 변경 사항을 서로 다른 방식으로 적용하므로 **둘 중 하나만 선택**하면 됩니다.

통합 빌더는 한글패치를 자동 적용하는 프로그램이 아니라 패치 완료된 추출본을 재빌드하는 도구입니다.

## 3. 사전 준비

### 3-1. 게임 파일 복호화

게임 파일을 추출하거나 재빌드하려면 먼저 본편 `.3ds`와 DLC `.cia`를 **복호화(Decrypt)** 해야 합니다.

이미 복호화된 파일을 가지고 있고 아래 기준 SHA-256과 일치한다면 이 과정은 건너뛰어도 됩니다.

**① 복호화 프로그램 다운로드**

1. [Batch CIA 3DS Decryptor 다운로드](https://gbatemp.net/threads/batch-cia-3ds-decryptor-a-simple-batch-file-to-decrypt-cia-3ds.512385/) 페이지에서 프로그램을 받습니다.
2. ZIP 파일을 원하는 작업 폴더에 압축 해제합니다.
3. `Batch CIA 3DS Decryptor.bat`와 함께 제공된 실행 파일들이 같은 폴더에 있는지 확인합니다.

> `.bat` 파일만 별도로 다운로드하면 정상 작동하지 않을 수 있으므로 전체 배포 폴더를 사용하세요.

**② 게임 파일 복사**

1. 본인이 보유한 본편 `.3ds` 또는 DLC `.cia` 파일을 준비합니다.
2. 원본 보존을 위해 **복사본**을 만듭니다.
3. 복사한 게임 파일을 `Batch CIA 3DS Decryptor.bat`가 있는 폴더에 넣습니다.

본편과 DLC는 혼동을 피하도록 각각 따로 처리하는 것을 권장합니다.

**③ 복호화 실행**

1. `Batch CIA 3DS Decryptor.bat`를 더블클릭합니다.
2. 명령 프롬프트 창에서 복호화가 진행됩니다.
3. `Finished`가 표시되면 결과 파일을 확인합니다.

| 복호화 전 | 복호화 후 예시 |
|---|---|
| `smt4f.3ds` | `smt4f-decrypted.3ds` |
| `smt4f (DLC).cia` | `smt4f (DLC)-decrypted.cia` |

결과 파일명은 원본 이름과 도구 버전에 따라 다를 수 있습니다. 오류가 발생하거나 파일이 생성되지 않았다면 같은 폴더의 `log.txt`를 확인하세요.

**④ SHA-256 해시 확인**

복호화된 게임 파일이 한국어 패치 제작 기준과 일치하는지 확인합니다.

Windows PowerShell에서 다음 명령어를 실행합니다. 경로는 본인의 파일 위치로 변경하세요.

`Get-FileHash -Algorithm SHA256 "D:\Games\smt4f-decrypted.3ds"`

`Get-FileHash -Algorithm SHA256 "D:\Games\smt4f (DLC)-decrypted.cia"`

**제작 기준 SHA-256**

**본편 — 북미판 UNDUB (Team Frost 적용 전)**

`afeaae1b41880dd91b9f2e8a4ce58741707f500f5e8e658e57e419d9d56d9b79`

**DLC — 북미판**

`ee53472150a3bb58a43673ff85fc5d1658ccae9430d949f22673bf7d5dbdd201`

해시가 다르면 지역판·UNDUB 구성·파일 상태가 다를 수 있으므로 제작 기준을 확인하세요.

> 파일 이름에 `-decrypted`를 붙이는 것만으로 복호화되지는 않습니다. 반드시 복호화 프로그램을 통해 처리해야 합니다.

### 3-2. HackingToolkit3DS로 게임 추출

복호화가 완료되었다면 [HackingToolkit3DS V9](https://github.com/Cyanol/HackingToolkit3DS)를 사용해 게임 데이터를 추출합니다.

**① 프로그램 준비**

1. HackingToolkit3DS V9를 설치하고 작업 폴더를 준비합니다.
2. 복호화된 게임 파일의 복사본을 해당 폴더에 넣습니다.
3. 게임 파일명은 가급적 영문·숫자 위주로 짧게 지정합니다.
4. `HackingToolkit3DS.exe`를 실행합니다.

**② 게임 파일 추출**

| 메뉴 명령 | 기능 |
|---|---|
| `D` | 본편 `.3ds` 추출 |
| `R` | 본편 `.3ds` 재빌드 |
| `CE` | DLC `.cia` 추출 |

- **본편:** `D` 선택 → 확장자 없는 파일명 입력
- **DLC:** `CE` 선택 → 확장자 없는 파일명 입력

예를 들어 `smt4f-decrypted.3ds`의 경우 `smt4f-decrypted`만 입력합니다.

`Decompress the code.bin file (n/y)?` 질문이 표시되면 선택한 설정을 기록하고, 이후 동일한 추출 기준을 유지하세요.

**③ 추출 결과 확인**

본편은 다음 파일과 폴더가 생성되었는지 확인합니다.

- `ExtractedRomFS/`
- `ExtractedExeFS/code.bin`
- `DecryptedExHeader.bin`

DLC는 `DecryptedApp.*`, `DecryptedManual.bin`, `DecryptedDownloadPlay.bin`, `HeaderNCCH1.bin`, `HeaderNCCH2.bin` 등의 생성 여부를 확인합니다.

**본편과 DLC는 서로 다른 작업 폴더에서 추출하세요.** 이전 추출 결과가 섞이면 빌드 오류가 발생할 수 있습니다.

### 3-3. Team Frost 2.0 선행 패치 적용

본 추가 패치를 적용하기 전에 기존 한국어 패치인 **Team Frost `SMT4Final 2.0`**이 필요합니다.

- [Team Frost 2.0 한글패치 안내](https://gall.dcinside.com/mgallery/board/view/?id=megaten&no=47112)

**직접 재빌드하는 경우**

1. 복호화된 북미판 UNDUB 본편을 HackingToolkit3DS의 `D`로 추출합니다.
2. Team Frost 2.0 패치의 **RomFS 변경 파일**을 `ExtractedRomFS/`에 병합합니다.
3. `R`로 Team Frost 2.0 적용본을 재빌드합니다.
4. 완성된 게임을 새로운 작업 폴더에서 다시 `D`로 추출합니다.
5. 이 추출 결과를 `Extracted_Base/`로 백업합니다.

이 `Extracted_Base/`가 다음 단계에서 추가 패치를 적용할 기준 폴더입니다.

**Team Frost 적용본의 확인용 SHA-256**

- `ExtractedExeFS/code.bin`

  `b54c3a31c5a59f7c9f82318dbdde0d1796414d3b33eafb04468c5f10581e7b42`

- `DecryptedExHeader.bin`

  `3515e53615b48591cd6625237df370b6dc48c11e9fc46bb7303b0cf2bed552d0`

두 파일이 일치하더라도 전체 RomFS의 동일성까지 보장하지는 않습니다.

**Luma3DS를 사용하는 경우**

Team Frost 2.0의 LayeredFS 파일을 먼저 SD 카드의 `luma/titles/000400000019A200/` 경로에 설치합니다.

이 방식은 본편을 재빌드할 필요가 없습니다.

---

## 4. 한국어 추가 패치 적용

### 방법 A. 본편 ROM 직접 재빌드

**대상:** `.3ds` 게임 파일에 한국어 추가 패치를 직접 반영하려는 사용자

**사용 파일:** `SMT4F_KO_FOR_REPACK_v1.1.1.zip`

1. 앞서 준비한 Team Frost 2.0 적용 추출본 `Extracted_Base/`를 복사하여 `Extracted_KO/` 폴더를 만듭니다.
2. `FOR_REPACK` ZIP을 압축 해제합니다.
3. ZIP의 **`patch/` 폴더 안에 있는 파일과 폴더**를 `Extracted_KO/`에 복사하여 병합·덮어씁니다.
4. 아래 주요 파일이 올바르게 적용되었는지 확인합니다.

   - `Extracted_KO/DecryptedExHeader.bin`
   - `Extracted_KO/ExtractedExeFS/code.bin`
   - `Extracted_KO/ExtractedRomFS/font/ko.bcfnt`

5. HackingToolkit3DS의 `R` 또는 아래 통합 빌더를 사용하여 새 `.3ds` 파일을 생성합니다.
6. 생성된 게임을 실행해 한글 표시와 이름 입력 기능을 확인합니다.

**주의사항**

- `ExtractedRomFS/` 전체를 삭제하거나 교체하지 말고 **파일을 병합**하세요.
- `code.bin`과 `DecryptedExHeader.bin`은 반드시 함께 적용해야 합니다.
- 기존 `CustomRomFS.bin` 등의 재빌드 산출물을 재사용하지 말고 새로 빌드하세요.

### 방법 B. Luma3DS 설치

**대상:** Luma3DS 게임 패칭 기능을 사용하는 3DS

**사용 파일:** `SMT4F_KO_LayeredFS_Luma_v1.1.1.zip`

1. 기존 **Team Frost 2.0 LayeredFS 패치**가 설치되어 있는지 확인합니다.
2. SD 카드의 `luma/titles/000400000019A200/` 폴더를 백업합니다.
3. 추가 패치 ZIP을 압축 해제합니다.
4. ZIP 안의 **`luma/` 폴더를 SD 카드 최상위 경로에 복사**하고 기존 파일과 병합·덮어씁니다.
5. 다음 파일들이 있는지 확인합니다.

   - `luma/titles/000400000019A200/code.bin`
   - `luma/titles/000400000019A200/exheader.bin`
   - `luma/titles/000400000019A200/romfs/font/ko.bcfnt`

6. 3DS 전원을 끈 상태에서 **SELECT 버튼을 누른 채 전원을 켭니다.**
7. Luma 설정 화면에서 `Enable game patching`을 활성화하고 **START로 저장**합니다.
8. 본편 게임을 실행하여 한국어 표시를 확인합니다.

**주의사항**

- 기존 Team Frost의 `romfs/` 폴더를 삭제하지 마세요.
- 기준 게임 타이틀 ID는 `000400000019A200`입니다.
- 다른 지역판은 단순히 폴더 이름을 변경한다고 호환되는 것은 아닙니다.

이 방법은 본편 ROM을 다시 빌드하지 않아도 됩니다.

### 방법 C. DLC 한글화 및 CIA 생성

**대상:** 별도로 보유한 북미판 DLC에 한국어 패치를 적용하려는 사용자

**사용 파일:** `SMT4F_KO_DLC_Patch_v1.1.1.zip`

1. DLC `.cia`를 복호화하고 HackingToolkit3DS의 `CE`로 추출합니다.
2. 추출 결과 전체를 `ExtractedDLC_Base/`로 보존합니다.
3. DLC 패치 ZIP을 압축 해제합니다.
4. `BUILD_DLC_CIA.bat`를 실행합니다.
5. 프로그램 안내에 따라 다음 경로를 입력합니다.

   - **원본 DLC 폴더:** `ExtractedDLC_Base/`의 전체 경로
   - **출력 경로:** 결과 CIA 저장 폴더 (Enter 시 기본 `out/` 사용)

6. 스크립트가 원본 및 패치 파일의 SHA-256을 검사한 후 CIA를 생성합니다.
7. 완료 메시지와 결과 파일이 생성되었는지 확인합니다.

**완성 파일:** `SMT4F_KO_DLC_v1.1.1.cia`

생성된 CIA를 본인의 3DS 또는 에뮬레이터 환경에 설치하면 됩니다.

**주의사항**

- DLC에는 Team Frost 2.0을 사전에 적용할 필요가 없습니다.
- `ExtractedDLC_Base/`는 수정하지 않은 원본 추출 상태로 유지하세요.
- 이 빌더는 패치 파일을 자동으로 조합하므로 `patch/` 내용을 원본 폴더에 미리 덮어쓰지 마세요.
- ZIP의 `tools/`, `patch/`, `rebuild/` 및 스크립트의 상대 위치를 변경하지 마세요.
- Windows PowerShell 환경에서 실행하며 Python은 필요하지 않습니다.

---

## 5. 통합 빌더 사용 (선택)

**사용 파일:** `SMT4F_KO_Main_DLC_Builder_v1.1.1.zip`

한글패치가 적용된 추출 폴더를 이용하여 본편 `.3ds`·`.cia` 또는 DLC `.cia`를 생성하는 통합 도구입니다.

별도로 HackingToolkit3DS의 `R`을 사용하는 대신 본편 재빌드에 사용할 수 있습니다.

### 사용 방법

1. 통합 빌더 ZIP을 압축 해제합니다.
2. `BUILD_ROM.bat`를 실행합니다.
3. **본편 또는 DLC**를 선택합니다.
4. 본편은 `.3ds` 또는 `.cia` 출력 형식을 선택합니다.
5. 패치가 완료된 추출 폴더와 결과 저장 경로를 입력합니다.

**지원 출력 형식**

| 출력 형식 | 기본 결과 파일 |
|---|---|
| 본편 3DS | `SMT4F_KO_v1.1.1_not-pad.3ds` |
| 본편 CIA | `SMT4F_KO_v1.1.1.cia` |
| DLC CIA | `SMT4F_KO_DLC_v1.1.1.cia` |

출력 경로를 지정하지 않으면 `output/` 폴더에 생성됩니다.

본편 `.3ds`는 `--not-pad` 옵션을 사용하여 불필요한 용량 패딩을 생략합니다.

### 입력 폴더 주의사항

- **본편:** 방법 A에서 `FOR_REPACK` 패치를 병합한 `Extracted_KO/` 폴더
- **DLC:** `ExtractedDLC_Base/`를 복사한 뒤 DLC 패치의 `patch/` 내용까지 병합한 작업 폴더

DLC 전용 `BUILD_DLC_CIA.bat`는 **수정하지 않은 원본 추출 폴더**를 입력받지만, 통합 빌더의 `BUILD_ROM.bat`는 **패치가 완료된 작업 폴더**를 입력받습니다.

두 빌더의 차이에 주의하세요.

**기타 사항**

- Windows PowerShell 3.0 이상 필요
- Python 설치 불필요
- 한국어 안내 및 진행률 표시 지원
- 원본 입력 폴더는 수정하지 않음
- 동일한 이름의 출력 파일이 이미 있으면 중단
- `tools/`, `rebuild/` 및 스크립트 위치 유지 필요

## 6. 문제 해결

| 증상 | 확인 사항 |
|---|---|
| 게임이 실행되지 않음 | 북미판 UNDUB, Team Frost 2.0 적용 여부 및 `code.bin`·ExHeader 조합 확인 |
| 일부 영문·일본어가 표시됨 | 패치 파일 병합 상태와 새 RomFS 재빌드 여부 확인 |
| Luma 패치가 적용되지 않음 | 타이틀 ID, SD 카드 경로, `Enable game patching` 확인 |
| DLC 기준 파일 오류 | DLC SHA-256 및 `CE` 추출 결과 확인 |
| DLC 패치 파일 손상 | ZIP 재압축 해제 및 `patch/`, `rebuild/` 구성 확인 |
| `3dstool`·`makerom` 오류 | `tools/` 위치, 파일 누락 및 디스크 여유 공간 확인 |
| 출력 파일이 이미 존재함 | 다른 출력 경로 지정 또는 기존 결과 파일 별도 보관 |

패치 후에는 기존 에뮬레이터 세이브스테이트 대신 게임을 새로 실행하여 정상 작동 여부를 확인하는 것이 좋습니다.

**패치 제거 방법**

- **재빌드 방식:** 백업한 원본 추출 폴더에서 다시 빌드합니다.
- **Luma3DS 방식:** 백업한 Team Frost 2.0 폴더를 복원하고 추가 패치에서 새로 생성한 `exheader.bin` 등을 제거합니다.

문제가 발생하면 사용한 패치 방식, 기준 ROM·DLC 버전, 오류 메시지 및 문제가 발생한 게임 화면을 함께 기록해 주세요.

## 7. 출처·라이선스 및 주의사항

- **Team Frost 2.0:** 기존 한국어 패치의 번역과 자료에 관한 권리는 해당 제작자에게 있습니다.
- **나눔명조:** 일부 한국어 그래픽 제작에 사용했으며, 글꼴은 [SIL Open Font License 1.1](https://github.com/google/fonts/blob/main/ofl/nanummyeongjo/OFL.txt)을 따릅니다.
- **게임 저작권:** 진 여신전생 IV FINAL의 게임 자료, 이름 및 상표에 관한 권리는 각 원저작권자에게 있습니다.
- **외부 빌드 도구:** 각 도구의 출처와 라이선스 조건을 별도로 확인해야 합니다.

본 추가 패치 전체에 대한 독립적인 오픈소스 라이선스나 자유 재배포 허락이 선언된 것은 아닙니다. GitHub 공개 시 포함된 게임 유래 파일, 기존 패치 자료, 글꼴 및 외부 도구의 배포 허용 여부를 개별적으로 확인해야 합니다.

이 패치는 게임 원저작권자나 Team Frost의 공식 승인 또는 후원을 받았음을 의미하지 않습니다.

패치는 모든 실행 환경에서 정상 작동을 보증하지 않으며, 데이터 손실에 대비해 원본 게임·DLC·세이브를 반드시 백업하세요.

---

**파일 무결성 확인**

배포 ZIP의 SHA-256은 `SHA256SUMS_v1.1.1.txt`에서 확인할 수 있습니다.

각 ZIP 내부에도 파일 검증용 `SHA256SUMS.txt`와 패키지별 상세 안내문이 포함되어 있습니다.
