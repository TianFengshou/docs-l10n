# 코드 리뷰 가이드

이 문서의 목적은 일반적인 오픈 소스 프로젝트와 특히 XLA 오픈 소스 프로젝트에서 다년간 진행한 집단 작업 경험을 바탕으로 성장한 코드 리뷰에 대한 XLA 팀의 입장 이면의 추론 과정을 설명하는 것입니다.

서로 다른 오픈 소스 프로젝트마다 리뷰어가 코드 작성자에게 얼마나 요청할 수 있는지에 대한 문화적 기대치가 다릅니다. 일부 프로젝트에서 리뷰어는 "대부분 옳은" pull request(PR)를 취하고, 직접 수정하고 제출합니다. XLA는 접근 방식을 반대로 취합니다. 추가적인 변경 사항 없이 충분히 제출할 수 있을 때까지 PR를 반복하길 기대합니다.

이러한 접근 방식의 주요 이유는 PR 작성자가 자격을 제대로 갖춘 XLA 기여자가 되는 방법을 배우길 바라기 때문입니다. 리뷰어가 PR에서 직접 문제를 수정한다면 작성자가 배우기 더 어렵습니다. XLA 접근 방식은 리뷰어와 리뷰이 모두에게 어려울 수 있지만 이 방식이 궁극적으로 우리를 커뮤니티로 성장하길 돕는다고 믿습니다.

"자격을 제대로 갖춘 XLA 기여자"가 되는 방법을 배운다는 것은 버그가 없는 코드를 작성하는 방법을 배운다는 것이 아닙니다. 이는 "XLA 수정 방법"을 배우는 것 이상의 의미를 갖습니다. 여기에 해당하는 내용은 다음과 같습니다.

- 코딩 스타일
- 찾아야 하는 에지 케이스
- 테스트 작성을 중심으로 한 예상
- 코멘트 및 PR 설명을 중심으로 한 예상
- 변경 사항을 지원하기 위한 인프라 빌딩을 중심으로 한 예상

프로젝트에 대한 지식과 리뷰어의 신뢰를 구축하는 만큼, 작성 중인 코드가 자연스럽게 리뷰어의 예상과 더 부합하기 때문에 코멘트를 더 적게 받을 것으로 예상할 수 있습니다.

많은 오픈 소스 프로젝트와 같이, XLA는 경험이 많은 사람이 적고 상대적으로 새로운 사람이 많습니다. 우리 중 경험이 많은 사람들은 많은 시간을 필요로 합니다. 다음을 수행하여 적시에 PR을 진행하기 위해 리뷰어가 필요한 시간과 요구되는 반복 횟수를 줄일 수 있습니다.

- *전송 전 신중히 리뷰 및/또는 동료가 PR을 리뷰하도록 함:* 리뷰를 위해 PR을 보내기 전 많은 사소한 실수(코드 스타일, 스펠링 및 문법 실수 등)를 없애려고 노력하세요. 모든 테스트에서 통과하도록 합니다.
- *리뷰어의 코멘트를 신중히 읽기:* 리유어가 요청한 것이 무엇인지 이해하고 새 버전을 푸시하기 전에 모든 코멘트를 해결하길 시도하세요.
- *부적절한 논의 피하기(바이크쉐딩):* 기술적인 논의와 의견 충돌은 매우 소중하며 모두가 완벽하지 않습니다. 하지만, 차이가 없거나 그저 스타일적인 논의는 피하세요. 리뷰어의 코멘트에 동의하지 않는 경우, 길게 오가는 논의를 피하기 위해 가능한 한 정확하고 포괄적으로 사유를 상세히 알리도록 시도하세요.
- *아래 나열된 "일반적으로 묻는 리뷰 질문"을 묻는 것 피하기:* 아래에 일반적인 질문에 대한 몇 가지 답변과 근거를 나열했습니다.

일반적으로, 가능한 한 적은 시간에 PR을 리뷰해보도록 여러분을 초대합니다. 그런 다음 변경 사항을 신속히 리뷰하고자 합니다!

XLA에 기여해주셔서 감사하며 즐거운 시간되세요!

## 일반적으로 묻는 리뷰 질문

### "이 인프라 변경 사항은 내 PR과는 관계가 없습니다. 해야 하는 이유가 뭔가요?"

XLA 팀은 전담 인프라팀이 없으므로 도우미 라이브러리를 빌드하고 기술 부채를 피하도록 하는 것은 우리 모두에게 달려있습니다. XLA를 변경하는 것은 일반적인 부분이라고 간주하며 모두 참여할 것으로 예상합니다. 일반적으로 코드 작성 시 필요에 따라 인프라를 빌드합니다.

XLA 리뷰어가 작성한 PR에 맞춰 일부 인프라(또는 PR을 크게 변경)를 빌드하도록 요청할 수 있습니다. 이 요청은 변경하려는 것에 불필요하거나 맞지 않는 것으로 보일 수 있습니다. 이는 빌드하려는 인프라의 양에 대한 예상과 리뷰어의 예상이 서로 불일치할 수 있기 때문일 수 있습니다.

예상에서의 불일치는 괜찮습니다! 프로젝트를 처음으로 시작하는 경우 이러한 불일치가 일어날 수 있습니다(그리고 때때로 경험이 많은 우리에게도 일어날 수 있습니다). 과거에 작업한 프로젝트들은 예상이 다를 수 있습니다. 그것 또한 괜찮으며 예상할 수 있습니다! 이러한 프로젝트 중 하나가 잘못된 접근 방식을 가지고 있다는 것을 의미하는 것이 아닙니다. 그저 다른 것입니다. 다른 모든 리뷰 코멘트와 함께 인프라 요청을 받아 이 프로젝트에서 기대하는 것이 무엇인지 배울 수 있는 기회가 되길 바랍니다.

### "코멘트를 다음 PR에서 해결해도 될까요?"

PR에서 인프라 요청(또는 기타 다량의 요청)에 관한 잦은 질문은 원래 PR에서 반드시 변경되어야 하는지 또는 다음 PR에서 후속으로 변경해도 되는지 여부입니다.

일반적으로, XLA는 PR 작성자가 후속 PR로 리뷰 코멘트를 해결하는 것을 허용하지 않습니다. 리뷰어가 이 PR에서 뭔가 해결되어야 한다고 결정한 경우, 일반적으로 요청된 변경 사항이 많다고 하더라도 원래 PR에서 해결하길 예상합니다. 이 기준은 Google에서 외부 및 또한 내부에 적용됩니다.

XLA가 이 접근 방식을 취하는 데에는 몇 가지 이유가 있습니다.

- *신뢰:* 리뷰어의 신뢰를 얻는 것이 주요 구성 요소입니다. 오픈 소스 프로젝트에서, 기여자는 마음대로 나타나거나 사라질 수 있습니다. PR을 승인한 후, 리뷰어는 약속된 후속 조치가 실제로 수행되었는지 확신할 수 있는 방법이 없습니다.

- *다른 개발자들에 대한 영향:* XLA의 특정 부분을 건드리는 PR을 보낸 경우, 다른 사람들이 동일한 부분을 보고 있을 수 있습니다. PR에서 기술 부채를 수락한 경우, 이 파일을 보는 모든 사람은 후속 조치가 제출될 때까지 이 부채의 영향을 받습니다.

- *리뷰어 대역폭:* 후속 조치에 대한 변경을 연기하는 것은 이미 과부화 된 리뷰어에 여러 비용을 부과합니다. 리뷰어는 후속 조치를 기다리는 동안 이 PR이 무엇이었는지에 관해 아마 잊어 다음 리뷰를 더 어렵게 만듭니다. 또한, 리뷰어는 대기 중인 후속 조치를 추적하여 실제로 수행되고 있는지 확인해야 합니다. 원래 PR과 전혀 다르게 변경하고 이를 다른 리뷰어가 리뷰할 수 있다면 대역폭은 문제가 되지 않을 것입니다. 경험상, 이것은 드문 경우입니다.