# 레버리지 ETF 경제학 논문 재현 코드

「국내 단일종목 레버리지 ETF의 리밸런싱 수요와 순설정의 상쇄: 되먹임 모형과 측정」의 계산 코드입니다.

- 저장소: [dokim111/letf-economics-thesis](https://github.com/dokim111/letf-economics-thesis)
- 자료 버전: **2026-11-19-v23**
- 대응 원고: **경제학 졸업논문 v18**
- 공개 범위: 경제학 계산 코드 3개, 패키지 버전, 실행 안내, 외부 입력 명세

이 저장소는 경제학 부분만으로 독립 구성되어 있습니다. 수리과학·통계학 저장소의 파일을 읽거나 그 디렉터리 구조에 의존하지 않습니다. 이전 통합 공개 묶음 v22에서 계산 코드는 바꾸지 않고, 저장소 구조와 안내·인용 메타데이터를 분리했습니다.

## 재현에 필요한 자료

**KRX 원자료는 이 저장소에 포함하지 않습니다.** 저장소를 내려받는 것만으로 계산을 실행하거나 원고의 모든 결과를 재현할 수는 없습니다. 세 입력 CSV를 별도로 확보하여 `replication/`에 배치해야 합니다.

정확한 파일명, 출처, 기간, 필수 열과 단위, ETF 16종의 목록, 자료 공표 시점의 제약은 [DATA_SOURCES.md](DATA_SOURCES.md)를 따릅니다. 원래 파일에서 11월 13일 순자산은 미공표였으므로 유효 분석 기간은 11월 12일까지 114거래일입니다. 이후에 보완된 자료를 사용하면 표본과 결과가 달라질 수 있습니다.

## 실행

Python 3.11 이상을 사용합니다. 원자료를 준비한 뒤 저장소 루트에서 실행합니다.

```bash
python3 -m pip install -r replication/requirements.txt
python3 replication/replicate.py
python3 replication/accounting_sensitivity.py
python3 replication/verify_intro_drawdown.py
```

Windows에서 Python 실행 파일 이름이 `python`이면 `python3` 대신 사용합니다. 입력·출력 경로는 스크립트 파일의 위치를 기준으로 정하므로, 위 명령을 저장소 루트에서 실행해도 세 입력 CSV는 `replication/`에서 읽습니다.

| 파일 | 역할 |
|---|---|
| `replication/replicate.py` | 표 3–8, 표 10의 입력 지표, 5.2절 보조 회귀 |
| `replication/accounting_sensitivity.py` | 표 9와 회계적 민감도 분석 |
| `replication/verify_intro_drawdown.py` | 서론의 지정된 두 날짜 사이 종가 수익률 |
| `replication/requirements.txt` | 계산에 사용된 NumPy·pandas 버전 |
| [replication/README.md](replication/README.md) | 상세 실행 순서, 출력 파일, 표와 스크립트 대응, 해석의 범위 |

출력은 기본적으로 `replication/`에 생성됩니다. 입력 CSV는 수정하지 않습니다. 기존 출력이 있으면 덮어씁니다. 세 스크립트는 난수를 사용하지 않으며 데이터를 자동으로 내려받지 않습니다.

## 포함하지 않은 범위

완성 논문 DOCX·PDF, 공식 제출 양식, 개인 학번·연락처, 원고 조판 코드, 내부 검토 기록, KRX 원자료는 포함하지 않았습니다. 기존 결과 파일과 그림 PNG도 이 저장소에는 배포하지 않습니다.

공개 코드는 표의 계산값을 출력합니다. 원고의 표·그림·수식을 포함한 전체 문서를 자동 조판하는 패키지는 아닙니다. 그림 1–2의 독립 생성 스크립트는 없으며, 표 10의 K/V 입력 지표는 출력하지만 충격 승수의 완성 표 자체를 출력하지는 않습니다. 자세한 범위는 [계산 안내의 표 대응](replication/README.md)을 참고하세요.

계산은 관측 경로를 고정한 회계적 재구성입니다. 실제 체결량, 구조적 반응계수 또는 인과적 가격효과의 추정으로 해석하지 않습니다.

## 인용과 버전

이 코드를 이용할 때에는 `VERSION`에 기재된 자료 버전과 사용한 **커밋 SHA**를 함께 기록하세요. 인용 메타데이터는 [CITATION.cff](CITATION.cff)에 있습니다. 원고에 적힌 버전과 이후 수정된 코드가 혼동되지 않도록 해당 커밋을 고정하여 사용하는 것이 좋습니다.
