# 데이터와 개인정보 안내

BIMSASU가 무엇을 보내고, PC와 Revit 모델에 무엇을 남기는지 정리했습니다. BIMSASU 라이선스 계약(판 1) 제4조 제7항이 가리키는 안내입니다.

## 밖으로 보내는 것

BIMSASU가 스스로 하는 통신은 **업데이트 확인과 설치 파일 받기**뿐입니다.

| 항목 | 내용 |
|---|---|
| 보내는 곳 (업데이트 정보) | `https://raw.githubusercontent.com/kklidi/BIMSASU-release/main/feed.json` (저작권자가 전자 서명한 파일) |
| 보내는 곳 (설치 파일) | `https://github.com/kklidi/BIMSASU-release/releases/download/…` (GitHub가 내려받기 서버로 옮겨 줄 수 있음) |
| 보내는 것 | 이 파일들을 읽는 HTTPS 요청. BIMSASU가 따로 붙이는 정보(이름·이메일·PC 정보·사용 기록·모델·파일 경로)는 없습니다. 요청에는 BIMSASU 버전이 든 프로그램 이름(User-Agent)이 붙습니다. |
| 언제 | Revit을 켤 때와 켜 둔 동안 4시간마다, 그리고 [About BIMSASU]의 [지금 확인]을 누를 때. 새 버전이 있고 "자동으로 설치"이거나 [닫을 때 설치]를 고른 경우, 또는 버전 정책이 걸린 경우 설치 파일을 받습니다. |
| 끄는 법 | About BIMSASU의 "새 버전"에서 "알리지 않음"을 고르면 새 버전 알림과 자동 설치가 꺼집니다. 버전 정책(라이선스 제5조) 확인은 끌 수 없어서 업데이트 정보는 계속 읽습니다. |
| 동의 전 | 라이선스에 동의하기 전에도 확인하고 새 버전을 받습니다. 설치는 그 버전의 계약에 동의한 뒤에 합니다. |
| 회사 프록시 | 회사 네트워크의 프록시가 Windows 로그인 인증을 요구하면, Windows가 그 프록시에 지금 Windows 계정으로 인증합니다(브라우저와 같은 방식). 이 인증 정보는 회사 프록시까지만 가고 GitHub로는 가지 않습니다. |
| 상대 서버가 받는 것 | 인터넷 통신에 필요한 IP 주소·요청 시각 등은 GitHub에 전달되고, [GitHub 개인정보 처리방침](https://docs.github.com/site-policy/privacy-policies/github-general-privacy-statement)에 따라 처리됩니다. 저작권자는 GitHub가 주는 내려받기 횟수 같은 통계 말고는 받지 않습니다. |

0.0.54까지의 BIMSASU는 하루 한 번 `https://kklidi.github.io/BIMSASU-release/latest.json`을 읽었습니다(옛 버전을 위해 그 파일은 계속 둡니다).

함께 들어 있는 제3자 구성요소(Open XML SDK: `DocumentFormat.OpenXml`, `System.IO.Packaging`)는 엑셀 파일을 PC 안에서 읽고 쓰는 데만 쓰며 통신하지 않습니다.

### 웹 브라우저가 열리는 경우

BIMSASU가 직접 통신하지는 않지만, 다음 경우 웹 브라우저가 사이트를 엽니다. 이때는 브라우저와 그 사이트의 정책이 적용됩니다.

- 사용자가 누른 경우: 새 버전 알림의 [다운로드], About 창의 [다운로드 페이지 열기]·링크·배너 등
- 설치 완료 화면에서 "nosasu.com 방문하기"가 체크된 채 설치를 마친 경우. 이 칸은 처음에 체크되어 있어 체크를 풀면 열리지 않고, 조용한 설치에서는 열리지 않습니다.

## PC에 남기는 것

| 위치 | 파일 | 내용 |
|---|---|---|
| `%AppData%\BIMSASU` | `update-check.txt` | 새 버전 설정(자동으로 설치·알림만·알리지 않음)과 마지막 확인 시각 |
| | `feed.json`, `feed-revoked.txt` | 마지막으로 받은 업데이트 정보(서명된 그대로)와, 그 정보가 폐기한 서명 키 목록 |
| | `update-policy.txt` | 버전 정책 기억: 알림 창을 처음 보여 준 날, 마지막으로 확인한 시각 등. 인터넷이 없어도 정책이 이어지게 합니다. |
| | `update-prompted.txt` | "새 버전이 있습니다" 창으로 마지막에 알린 버전 |
| | `Update.xml` | 0.0.54까지의 업데이트 설정(남아 있으면 처음 한 번 "자동 확인 끔"만 이어받음) |
| | `license.txt` | 라이선스 동의 기록: 동의한 판, 날짜(UTC), 방법(설치 프로그램·첫 명령·출력·업데이트)과 BIMSASU 버전. 새 판 계약에 [동의 안 함]을 누른 버전도 적습니다. |
| | `TabColor.xml` | 탭 색 설정. 연 파일의 경로를 기억합니다(협업 모델은 중앙 파일 경로). 자동으로 정한 색은 최근 300개까지, 직접 고른 색은 지울 때까지 둡니다. |
| | `GridToCrop.xml` | Grid to Crop 설정 |
| | `SubmitCheck.xml` | Submit Check 임시 문구 검색어(찾을 말·뺄 말). 고쳐서 저장했을 때만 생깁니다. |
| | `ExportSchedule.folder` | 일람표를 내보낸 폴더 경로 |
| | `Cache\DimGuideFrame-*` | Grid to Crop 안내선 패밀리 사본(Revit 버전별, 다음 프로젝트에서 다시 씀) |
| `%LocalAppData%\BIMSASU` | `LICENSE.txt`, 제거 프로그램 | 설치 프로그램으로 설치한 경우 |
| `%LocalAppData%\BIMSASU\updates` | `BIMSASU-Setup-<버전>-<해시>.exe` | 받아 둔 새 설치 파일. 해시가 업데이트 정보와 같을 때만 씁니다. |
| | `state.txt`, `result.txt`, `install-<버전>.log` | 자동 설치 상태(받아 둔 버전, 실패 횟수, 다시 해 볼 시각), 설치 프로그램이 남긴 결과와 설치 기록 |
| | `update-error.log`, `download.lock` | 업데이트 확인·받기에서 난 오류 기록(256 KB까지), 여러 Revit이 같은 파일을 동시에 받지 않게 하는 표시 |
| | `TabColor.log` (`.old`) | 탭 색 작업 기록. 탭 이름, 열린 파일 경로, 오류 내용이 들어갈 수 있습니다. |
| | `BIMSASU-startup-error.log` | Revit 시작 중 오류가 났을 때만. 오류 내용과 Windows 사용자 이름이 든 경로가 들어갈 수 있습니다. |
| `%AppData%\Autodesk\Revit\Addins\<연도>` | `BIMSASU\BIMSASU.installed` | 설치 프로그램이 끝까지 설치했다는 표시(버전). 설치하는 동안에만 옛 BIMSASU를 `BIMSASU.previous`로 옮겨 두었다가 끝나면 지웁니다. |
| 레지스트리 `HKCU\…\RunOnce` | `BIMSASU-Recover` | 설치하는 동안에만. 설치가 중간에 끊기면(전원 꺼짐 등) 다음 로그인 때 옛 BIMSASU를 되돌리고 스스로 지워집니다. |
| `%TEMP%\BIMSASU-DimGuide` | 작업 파일 | Grid to Crop이 패밀리를 만드는 동안 쓰고 지웁니다. 남은 것은 하루가 지난 뒤 다시 쓸 때 지웁니다. |

- 경로가 든 파일에는 Windows 사용자 이름이 들어갈 수 있습니다. BIMSASU는 이 파일들을 밖으로 보내지 않습니다.
- 탭 색 설정을 읽지 못하면 옆에 `TabColor.xml.broken` 사본을 둘 수 있습니다.
- `license.txt`를 지우면 다음 BIMSASU 명령 때 동의 창이 다시 나옵니다.

## 모델(RVT) 안에 남기는 것

- Excel Table: 불러온 엑셀 파일의 경로. 모델을 다른 사람에게 주면 경로도 함께 갑니다.
- Revision Colors·Schedule Colors: 색 규칙과 설정
- Grid to Crop: 안내선 패밀리(`DEF_치수기준선`)와 유형
- 출력 보호: 인쇄·내보내기 때 실행 취소 목록에 "BIMSASU 출력용 DEF 숨기기", "BIMSASU 출력 후 DEF 되돌리기", 리비전 색 빼기·되돌리기 기록이 남습니다. 라이선스에 동의하기 전에는 [동의하고 빼고 출력]을 고른 경우에만 이 기록이 생깁니다.

## 지우는 법

- **설치 프로그램으로 설치한 경우**: Windows 설정 → 앱 → BIMSASU 제거. Revit 애드인 폴더의 BIMSASU(`BIMSASU.addin`, `BIMSASU` 폴더)와 `%LocalAppData%\BIMSASU`(받아 둔 설치 파일 포함)가 지워집니다. `%AppData%\BIMSASU`(설정·동의 기록)와 `%TEMP%`의 작업 파일은 남으므로 필요하면 직접 지웁니다.
- **ZIP으로 설치한 경우**: 제거 프로그램이 없습니다. 애드인 폴더의 파일과 위 폴더를 직접 지웁니다.
- 지우면 출력 보호도 멈춥니다. 그 PC에서 출력한 도면에 `DEF_` 메모와 리비전 색이 나올 수 있습니다.

## 문의할 때 보내는 파일

오류를 문의하면서 manager@nosasu.com으로 보낸 기록·화면 캡처·모델은 답변과 오류 수정에만 씁니다. 목적을 이루면 지우고, 그 전이라도 요청하면 지웁니다. 보내기 전에 파일 안의 비밀이나 개인정보를 확인해 주세요.

nosasu.com 웹사이트의 개인정보 처리는 그 사이트의 처리방침을 따릅니다.

---

문의: https://nosasu.com · manager@nosasu.com · 라이선스 계약 전문: [LICENSE.md](LICENSE.md)
