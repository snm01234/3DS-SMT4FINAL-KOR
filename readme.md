# 진 여신전생 IV FINAL 한국어 패치 적용 가이드

이 문서는 `D:\SMT4FINAL\dist`에 있는 **추출 파일 기반 Python 패치**를 적용하기 위한 통합 안내서입니다.

본 배포 방식은 완성된 ROM, CIA, `code.bin`, RomFS 파일을 그대로 배포하지 않고, 사용자가 직접 준비한 기준 추출 파일에 바이너리 델타를 적용해 한국어 패치 상태의 추출 폴더를 생성합니다.

> 중요: 반드시 본인이 적법하게 보유한 게임에서 직접 추출한 파일을 사용하세요. 이 배포본은 게임 본편이나 DLC 원본 파일을 제공하지 않습니다.

## 1. 배포 구성

현재 기준으로 사용하는 패치 폴더는 다음 두 개입니다.

```text
SMT4F_KO_Extracted_PythonPatch_v1.0.0/
SMT4F_KO_ExtractedDLC_PythonPatch_v1.0.0/
```

첫 번째는 **본편**, 두 번째는 **DLC**용입니다.

각 폴더에는 다음 파일이 있습니다.

```text
apply_patch.py
APPLY_PATCH.bat
patch_data.zip
README_KO.txt
```
`patch_data.zip`은 완성 게임 파일 모음이 아니라 기준 파일과 수정 파일의 차이를 저장한 XOR 델타와 매니페스트입니다. `apply_patch.py`가 기준 파일의 SHA-256을 확인한 뒤 새 출력 폴더를 만들고 델타를 적용합니다.

외부 `xdelta`, `bsdiff` 실행 파일은 필요하지 않습니다.

## 2. 필요한 프로그램

### 필수

- Windows 10/11 권장
- Python 3.9 이상
- HackingToolkit3DS로 준비한 기준 추출 폴더
- 패치 적용 및 재빌드에 필요한 충분한 디스크 여유 공간

Python 설치 확인:

```powershell
py -3 --version
```

또는:

```powershell
python --version
```

버전 정보가 표시되면 사용할 수 있습니다.

### 별도 Python 패키지

필요하지 않습니다. 패처는 Python 표준 라이브러리만 사용합니다.
## 3. 기준 파일에 대한 중요 사항

이 패치는 아무 SMT IV FINAL 추출본에 적용되는 범용 패치가 아닙니다. **제작 시 사용한 `Extracted_Base` / `ExtractedDLC_Base`와 동일한 기준 파일**이 필요합니다.

### 본편 기준 롬

본편 패치는 **북미판(USA) UNDUB 원본 ROM에 기존 팀프로스트 제작 한글패치 2.0 버전 `SMT4Final 2.0`의 RomFS 패치 파일을 적용한 ROM**을 기준으로 제작되었습니다. 이후 HackingToolkit3DS로 해당 기준 ROM을 추출한 결과가 `Extracted_Base`의 기준 파일이 됩니다.

기준 ROM 파일 예시는 다음과 같습니다.

```text
Shin_Megami_Tensei_IV_Apocalypse(decrypted).3ds
SHA-256: afeaae1b41880dd91b9f2e8a4ce58741707f500f5e8e658e57e419d9d56d9b79
```

즉, **순정 북미판 ROM을 그대로 추출한 파일이 기준이 아니며**, 북미판 UNDUB 원본 ROM에 먼저 `SMT4Final 2.0` RomFS 패치를 적용한 뒤 그 결과물을 HackingToolkit3DS로 추출해야 합니다.

기준 추출 폴더는 다음 형태입니다.

```text
Extracted_Base/
├─ DecryptedExHeader.bin
├─ ExtractedExeFS/
│  └─ code.bin
├─ ExtractedRomFS/
├─ ExtractedBanner/
├─ ExtractedManual/
└─ 기타 HackingToolkit3DS 추출 파일
```

> **DLC에는 위 본편 기준 ROM SHA-256 및 `SMT4Final 2.0` RomFS 적용 조건이 해당되지 않습니다.** DLC는 별도의 `ExtractedDLC_Base` 기준 파일을 사용합니다.

### DLC 기준

DLC 패치는 다음 **북미판(USA) DLC decrypted CIA**를 기준으로 제작되었습니다. 이 CIA를 HackingToolkit3DS로 추출한 결과가 `ExtractedDLC_Base`의 기준 파일입니다.

```text
Shin Megami Tensei IV - Apocalypse (USA) (DLC) decrypted.cia
SHA-256: ee53472150a3bb58a43673ff85fc5d1658ccae9430d949f22673bf7d5dbdd201
```

즉, DLC는 본편과 달리 `SMT4Final 2.0` RomFS 패치를 먼저 적용하는 과정이 없습니다. 위 SHA-256과 일치하는 DLC CIA를 그대로 HackingToolkit3DS로 추출한 파일을 기준으로 사용합니다.

기준 추출 폴더는 다음 형태입니다.

```text
ExtractedDLC_Base/
├─ DecryptedApp.0003.00000003
├─ DecryptedApp.0004.00000004
├─ ...
├─ DecryptedManual.bin
├─ DecryptedDownloadPlay.bin
├─ ExtractedManual/
└─ ExtractedDownloadPlay/
```

파일명만 같다고 호환되는 것은 아닙니다. 패처가 변경 대상 파일의 **크기와 SHA-256을 모두 검사**하므로 다른 지역판, 다른 UNDUB, 다른 한글패치 버전, 임의 수정본은 적용 전에 중단될 수 있습니다.
## 4. 본편 패치 적용

본편 패치 폴더:

```text
SMT4F_KO_Extracted_PythonPatch_v1.0.0
```

### 가장 쉬운 방법

1. 위 폴더 안의 `APPLY_PATCH.bat`를 실행합니다.
2. `Baseline folder`에 기준 추출 폴더 경로를 입력합니다.
3. `Output folder`에 새로 생성할 폴더 경로를 입력합니다.
4. SHA-256 검사가 끝나면 기준 폴더 전체를 새 출력 폴더로 복사합니다.
5. 623개 패치 작업을 적용하고 각 결과 파일을 다시 SHA-256으로 검증합니다.

예시:

```text
Baseline folder: D:\SMT4FINAL\Extracted_Base
Output folder:   D:\SMT4FINAL\Extracted
```

정상 완료 시 마지막에 다음과 비슷한 문구가 표시됩니다.

```text
Applied and verified 623/623 files
Patch complete: D:\SMT4FINAL\Extracted
```

`Extracted_Base`는 직접 수정하지 않습니다.
### 명령행으로 적용

PowerShell 또는 명령 프롬프트에서 패치 폴더로 이동한 뒤 실행합니다.

```powershell
py -3 apply_patch.py "D:\SMT4FINAL\Extracted_Base" "D:\SMT4FINAL\Extracted"
```

기준 파일 호환성만 검사하고 실제 파일은 만들지 않으려면:

```powershell
py -3 apply_patch.py "D:\SMT4FINAL\Extracted_Base" "D:\SMT4FINAL\Extracted" --check
```

기존 출력 폴더를 삭제하고 새로 만들려면:

```powershell
py -3 apply_patch.py "D:\SMT4FINAL\Extracted_Base" "D:\SMT4FINAL\Extracted" --force
```

> `--force`는 지정한 출력 폴더를 삭제합니다. 기준 폴더와 출력 폴더 경로를 혼동하지 마세요.

## 5. DLC 패치 적용

DLC 패치 폴더:

```text
SMT4F_KO_ExtractedDLC_PythonPatch_v1.0.0
```

DLC를 사용하지 않는 경우 이 단계는 생략할 수 있습니다.
### DLC 적용 순서

1. `SMT4F_KO_ExtractedDLC_PythonPatch_v1.0.0\APPLY_PATCH.bat`를 실행합니다.
2. `Baseline folder`에 `ExtractedDLC_Base` 경로를 입력합니다.
3. `Output folder`에 새 `ExtractedDLC` 경로를 입력합니다.
4. 37개 변경 대상의 기준 SHA-256을 검사합니다.
5. 기준 폴더를 복제한 뒤 37개 델타를 적용하고 결과 SHA-256을 검증합니다.

예시:

```text
Baseline folder: D:\SMT4FINAL\ExtractedDLC_Base
Output folder:   D:\SMT4FINAL\ExtractedDLC
```

정상 완료 예시:

```text
Applied and verified 37/37 files
Patch complete: D:\SMT4FINAL\ExtractedDLC
```

명령행으로 실행할 경우:

```powershell
py -3 apply_patch.py "D:\SMT4FINAL\ExtractedDLC_Base" "D:\SMT4FINAL\ExtractedDLC"
```

호환성만 확인하려면:

```powershell
py -3 apply_patch.py "D:\SMT4FINAL\ExtractedDLC_Base" "D:\SMT4FINAL\ExtractedDLC" --check
```
## 6. 필요한 디스크 공간

현재 기준 폴더의 실제 크기는 대략 다음과 같습니다.

- 본편 `Extracted_Base`: 약 4.14 GB
- DLC `ExtractedDLC_Base`: 약 43 MB

패처는 기준 폴더를 새 출력 폴더로 **통째로 복사한 뒤** 변경 파일을 적용합니다. 따라서 본편은 최소 5 GB 이상의 여유 공간을 확보하는 것을 권장합니다. 재빌드 결과물까지 같은 드라이브에 만들 경우 더 많은 여유 공간이 필요합니다.

## 7. 패치가 실제로 하는 일

본편 패치는 현재 다음 작업을 수행합니다.

- XOR 델타 적용: 622개 파일
- 기준 폰트에서 복사/이름 변경: 1개 파일
- 총 검증 작업: 623개

추가되는 `ExtractedRomFS/font/ko.bcfnt`는 기준 폴더의 기존 한글 폰트 `cbf_ko-Hang-KR.bcfnt`를 복사해 생성하므로, 동일한 폰트 본문을 패치 데이터에 다시 포함하지 않습니다.

DLC 패치는 현재 다음 작업을 수행합니다.

- XOR 델타 적용: 37개 파일
- 출력 결과 각각 SHA-256 검증

패치 중 하나라도 예상 결과와 다르면 정상 완료로 처리하지 않습니다.
## 8. 본편 재빌드

Python 패처의 최종 결과는 `.3ds`가 아니라 **패치가 적용된 HackingToolkit3DS 추출 폴더**입니다.

예시:

```text
D:\SMT4FINAL\Extracted
```

이 폴더의 `ExtractedRomFS`, `ExtractedExeFS`, `DecryptedExHeader.bin` 등이 패치된 상태이므로, HackingToolkit3DS의 일반적인 Rebuild 절차를 사용해 게임 이미지를 다시 생성합니다.

재빌드할 때는 이전 작업에서 만들어 둔 다음 파일을 그대로 재사용하지 않는 것을 권장합니다.

```text
CustomRomFS.bin
CustomExeFS.bin
CustomPartition*.bin
이전 재빌드 완료 .3ds
```

이전 빌드 산출물을 재사용하면 최신 `ExtractedRomFS` / `ExtractedExeFS` 변경이 반영되지 않을 수 있습니다. 가능하면 패치 적용 후 새로 빌드하세요.

> `DecryptedRomFS.bin` 같은 추출 당시의 대형 컨테이너 파일은 Python 패처가 개별 `ExtractedRomFS` 변경 내용을 다시 합쳐 쓰는 용도가 아닙니다. 재빌드는 갱신된 추출 디렉터리를 기준으로 새로 수행해야 합니다.
## 9. DLC 재빌드

DLC Python 패처 역시 최종 CIA를 만들지 않고 다음과 같은 **패치 완료 추출 폴더**를 생성합니다.

```text
D:\SMT4FINAL\ExtractedDLC
```

이 폴더에는 패치된 `DecryptedApp.*`, `DecryptedManual.bin`, `DecryptedDownloadPlay.bin` 및 관련 추출 파일이 들어 있습니다.

CIA로 다시 묶으려면 DLC를 처음 추출할 때 사용한 것과 호환되는 재빌드 절차를 사용하세요. 일반적으로 `makerom`/`3dstool` 계열 도구 또는 기존 DLC 재빌드 스크립트를 사용할 수 있습니다.

이 Python 패치 자체를 적용하는 데에는 별도 EXE 도구가 필요하지 않습니다. 외부 도구가 필요한 시점은 **패치 적용 후 CIA 재빌드 단계**입니다.

완성된 CIA는 사용자 개인 환경에서만 생성하는 것을 전제로 하며, 배포 패키지에는 포함하지 않는 것을 권장합니다.

## 10. 패치 완료 확인

패처는 각 변경 파일을 생성한 직후 다음 두 항목을 확인합니다.

1. 결과 파일 크기
2. 결과 파일 SHA-256

따라서 다음 메시지가 나오면 패처가 관리하는 변경 대상은 검증을 통과한 것입니다.

```text
Patch complete: <출력 폴더>
```

중간에 `ERROR:`가 표시되었다면 완료된 것으로 보지 마세요.
## 11. 자주 발생하는 오류

### `Baseline SHA-256 mismatch`

기준 파일 내용이 제작 기준과 다릅니다.

가능한 원인:

- 다른 지역판 사용
- 다른 UNDUB 버전 사용
- 다른 한글패치 버전 사용
- 기준 폴더에 이미 다른 수정이 들어감
- 추출 과정에서 일부 파일이 달라짐

이 경우 해당 파일을 억지로 덮어쓰지 말고, 정확한 기준 파일을 다시 준비하세요.

### `Baseline size mismatch`

파일명은 같지만 파일 크기가 다릅니다. 다른 버전의 파일일 가능성이 높습니다.

### `Missing baseline file`

필요한 추출 파일이 없습니다. 추출이 완전하게 끝났는지 확인하세요.

### `Missing patch data`

`patch_data.zip`이 `apply_patch.py`와 같은 폴더에 있어야 합니다. 파일명을 변경하거나 다른 위치로 옮기지 마세요.
### `Output already exists`

기본 설정에서는 기존 출력 폴더를 덮어쓰지 않습니다.

기존 출력 폴더를 직접 삭제하거나, 내용을 모두 버려도 되는 경우에만 `--force`를 사용하세요.

```powershell
py -3 apply_patch.py "D:\SMT4FINAL\Extracted_Base" "D:\SMT4FINAL\Extracted" --force
```

### Python 명령을 찾을 수 없음

`py -3 --version`이 실패하면 `python --version`도 확인하세요. 둘 다 실패하면 Python 3을 설치하고 PATH 설정을 확인해야 합니다.

### 경로에 공백이 있음

경로 전체를 큰따옴표로 감싸면 됩니다.

```powershell
py -3 apply_patch.py "D:\My Games\Extracted_Base" "D:\My Games\Extracted"
```

## 12. 권장 작업 폴더 예시

```text
SMT4FINAL/
├─ Extracted_Base/             # 본편 기준 추출본, 보존
├─ Extracted/                  # 본편 패치 결과
├─ ExtractedDLC_Base/          # DLC 기준 추출본, 보존
├─ ExtractedDLC/               # DLC 패치 결과
└─ dist/
   ├─ readme.md
   ├─ SMT4F_KO_Extracted_PythonPatch_v1.0.0/
   └─ SMT4F_KO_ExtractedDLC_PythonPatch_v1.0.0/
```
## 13. 현재 제작 기준

현재 메인 패처는 작업 프로젝트에서 사용한 **영문판 UNDUB + Team Frost 2.0 기반 추출 파일**을 기준으로 생성되어 있습니다.

같은 이름의 게임이라도 원본 지역, UNDUB 구성, 기존 패치 상태가 다르면 SHA-256 검사가 실패할 수 있습니다. 배포 시에는 사용자가 정확히 같은 기준을 준비할 수 있도록 기준 버전을 함께 명시하는 것을 권장합니다.

## 14. GitHub 배포 시 포함 권장 파일

Python 패치 방식만 배포한다면 다음 구성만으로 충분합니다.

```text
readme.md
SMT4F_KO_Extracted_PythonPatch_v1.0.0/
├─ apply_patch.py
├─ APPLY_PATCH.bat
├─ patch_data.zip
└─ README_KO.txt
SMT4F_KO_ExtractedDLC_PythonPatch_v1.0.0/
├─ apply_patch.py
├─ APPLY_PATCH.bat
├─ patch_data.zip
└─ README_KO.txt
```

패치 적용 자체에는 `xdelta3.exe`, `makerom.exe`, `3dstool.exe`가 필요하지 않습니다.

DLC CIA 재빌드용 도구를 별도 제공할 경우에는 해당 도구의 라이선스 및 재배포 조건을 별도로 확인하세요.
## 15. GitHub 배포에서 제외 권장

다음 항목은 Python 델타 패치 배포에는 필요하지 않습니다.

```text
Extracted/
Extracted_Base/
ExtractedDLC/
ExtractedDLC_Base/
완성 .3ds
완성 .cia
완성 code.bin
완성 RomFS/ExeFS 파일 모음
_verify_* 검증 폴더
```

현재 `dist`에 남아 있는 이전 테스트/배포 산출물 중 완성 CIA, 완성 LayeredFS 리소스, 구형 xdelta 패키지는 새 Python 방식과 별개입니다. 공개 저장소를 만들 때는 필요한 Python 패치 폴더만 선별해 업로드하는 것을 권장합니다.

## 16. 빠른 적용 체크리스트

- [ ] Python 3 설치 확인
- [ ] 정확한 `Extracted_Base` 준비
- [ ] 필요하면 `--check`로 본편 호환성 확인
- [ ] 본편 `APPLY_PATCH.bat` 실행
- [ ] `Applied and verified 623/623 files` 확인
- [ ] DLC 사용 시 정확한 `ExtractedDLC_Base` 준비
- [ ] DLC `APPLY_PATCH.bat` 실행
- [ ] `Applied and verified 37/37 files` 확인
- [ ] 이전 `Custom*.bin` 및 이전 빌드 결과를 재사용하지 않고 새로 재빌드
- [ ] 실제 게임에서 신규/기존 세이브와 주요 UI를 확인

---

패치 버전: **v1.0.0**  
문서 기준일: **2026-09-26**
