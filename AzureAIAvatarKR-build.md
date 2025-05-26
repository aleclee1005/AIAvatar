# AI 세일즈 아바타의 탐구
——  Agora × Azure × Dify × TEN × Trulience 통합 실습 ——

이 가이드는 전 세계 🌍 기업 개발자와 개인 탐험가들을 대상으로,  
가장 간단하고 이해하기 쉬운 방법으로,  
“듣고, 말하고, 생각하고, 연기하는” AI 디지털 판매 도우미를 하나씩 만들어가는 과정을 소개합니다.  
이번에 선택한 응용 사례는: 명품차 AI 디지털 안내원이며, 그 분의 이름은 Vendy입니다.

---

정식으로 구축을 시작하기 전에, **Agora, Azure, Dify, TEN**  팀의 지도와 격려에 진심으로 감사드립니다.  
전 세계 오픈소스 커뮤니티가 추구하는 **탐구(探索), 공동창작(共創) 및 임파워먼트(賦能)**  이념덕분에,  
저와 같은 제로에서 시작한 AI 공동 구축 탐험자에게도 이 구상을 실현할 기회가 주어졌습니다.  
이 전체적인 통합 솔루션을 실현할 수 있게 되었습니다.

---

이 문서가 전 세계 더 많은 AI 탐험가들에게 실용적이고 재사용 가능한 경로를 제공하고,  
실습의 문턱을 낮추며, AX(AI 변혁)가 개인, 기업, 사회 각층에서 진정으로 구현되고 임파워먼트 될 수 있도록 돕기를 바랍니다.

문서에서 부족한 부분이나 개선할 점이 있으면 언제든지 연락 주시기 바랍니다.

---

💡 저는 믿습니다:

> **AI는 인간으로부터 출발하고, 인간에 의해 발전하며, 그 근본적인 목적은 인간의 존엄성과 자유를 지키기 위해 존재한다.**  
> 기술의 발전은 인간의 가치와 공명할 때, 비로소 진정으로 모든 사람에게 힘이 될 수 있다.

---

**저자**: Alec Lee｜AX 글로벌 전략가 & 풀스택 탐험가  
문화와 시스템을 넘어, 일기당천과 누구도 놓치지 않는 AX 시대의 창조를 위하여.

**날짜**: 2025년 5월 11일  
**이메일**: alec.lee1005@gmail.com

## 1. “듣고 말하고 생각하고 연기하는” AI 디지털 판매 도우미는 어떤 6개 플랫폼으로 구성되나요?

본 프로젝트는 **TEN 플랫폼을 중심으로**, 다음의 5개 플랫폼을 통합하여,  
완전한 대화 능력을 갖춘 고급차 AI 판매 디지털 아바타(AI Sales Avatar)인 **Vendy**를 구축합니다.

Vendy는 “**듣고, 말하고, 생각하고, 연기**”할 수 있습니다 —  
즉, **사용자의 질문을 듣고, 답변을 생각하며, 음성으로 응답하고, 디지털 아바타 형상으로 나타냅니다**.

👇 아래 그림은 시스템 전체 통합 아키텍처를 보여줍니다:

![Azure AIsalesAvatar](https://raw.githubusercontent.com/aleclee1005/AISalesAvatar/img/img/062AIsalesAvatar.jpg)

## 🧩 각 플랫폼이 시스템에서 맡은 역할

👇 아래 그림은 시스템 내 각 플랫폼의 통합 모듈과 작업 흐름을 보여줍니다.

![Azure Structure](https://raw.githubusercontent.com/aleclee1005/AISalesAvatar/img/img/063AISalesAvatarStructure.jpg)

## 📌 각 플랫폼 기능 설명

- **Dify + Azure OpenAI**: 스마트 에이전트를 구축하고, 기업 내부 데이터와 OpenAI API를 호출하여 TEN에 통합된 대화 인터페이스(API)를 제공합니다.

- **Trulience**: 디지털 인간 연기 능력을 제공하며, TEN에 디지털 인간 ID와 액세스 토큰을 제공하여 가상 형상 구현을 지원합니다.

- **Agora**: 음성 통화 및 영상 통화를 구현하며, TEN에 App ID와 Certificate(인증서)를 제공합니다.

- **Azure Speech**: 음성 인식(STT) 및 음성 합성(TTS) 서비스를 제공하며, TEN에 다음과 같은 파라미터를 제공합니다:  
  `AZURE_STT_KEY`, `AZURE_STT_REGION`, `AZURE_TTS_KEY`, `AZURE_TTS_REGION`

- **TEN (플랫폼 중추)**: 시스템의 중추 플랫폼으로, 위의 모든 플랫폼의 API, 키 및 토큰을 통합하여,  
  AI Sales Avatar — **Vendy**의 전체 지능형 대화 흐름 및 실시간 상호작용 능력을 실현합니다.
  
---

📌 **팁**: 위의 플랫폼은 실제 요구 사항에 따라 다른 오픈 소스 또는 SaaS 솔루션으로 대체할 수 있습니다.  
본 프로젝트에서 사용된 조합은 학습과 재사용을 용이하게 하기 위한 참고 예시입니다.

---

## 2. 시작 구축하기 (각 단계는 마치 레고처럼)

우리는 먼저 Dify에서 세 가지 작업을 완료하여, 내부 데이터를 기반으로 한 AI Sales Avatar "본체"를 구축할 것입니다.  
시연 사례는: **명품차 안내 디지털인**이며, 그녀의 이름은 **Vendy**입니다.

---

### 🧩 Step 1：Dify 계정 등록 및 모델 API 설정

👉 Dify 공식 웹사이트 열기: [https://dify.ai/](https://dify.ai/), 오른쪽 상단의 "Get Started"를 클릭하여 등록 절차를 시작합니다.

![Dify AI](https://raw.githubusercontent.com/aleclee1005/AISalesAvatar/img/img/003DifyAIsales.jpg)

다음 방법으로 계정에 로그인하거나 등록할 수 있습니다: **GitHub**, **Gmail**, 또는 **Hotmail**.

![Dify Email](https://raw.githubusercontent.com/aleclee1005/AISalesAvatar/img/img/004DifyEmail.jpg)

Dify에 로그인한 후, 왼쪽 메뉴에서 **「Settings > Model Provider」（모델 제공자）**를 클릭합니다.  
페이지에서 **Azure OpenAI Service Model** 모듈을 찾아 **Install**을 클릭하여 설치합니다.


![Dify Models](https://raw.githubusercontent.com/aleclee1005/AISalesAvatar/img/img/070ModelInstal.jpg)

Azure Portal을 열고, Azure 공식 포털 웹사이트에 로그인합니다:

🔗 [https://portal.azure.com](https://portal.azure.com)

홈페이지 왼쪽 상단에서 **「Create a resource（리소스 생성）」**를 클릭하고,  
검색창에 **Azure OpenAI**를 입력하여 생성 페이지로 이동합니다.

👇 생성 페이지 예시는 아래와 같습니다:

![Azure Resource](https://raw.githubusercontent.com/aleclee1005/AISalesAvatar/img/img/028Azure.jpg)

---

다음 내용을 참고하여 기본 정보를 입력합니다 (**Basics**):

![Azure OpenAI List](https://raw.githubusercontent.com/aleclee1005/AISalesAvatar/img/img/029AzureOpenAI.jpg)

---

일반적으로 **「공개 접근」**을 기본으로 선택하면 됩니다. 이 옵션을 선택하면 서비스가 인터넷을 통해 접근할 수 있습니다.

![Azure OpenAI Public](https://raw.githubusercontent.com/aleclee1005/AISalesAvatar/img/img/030AzureCreateAzureOpenAI.jpg)

🧩 선택적 단계: 리소스에 `project=ai-agent`와 같은 태그를 추가하여 후속 분류 및 관리를 용이하게 할 수 있습니다.

👇 태그 및 네트워크 설정 화면은 아래와 같습니다.

![Azure resourceset](https://raw.githubusercontent.com/aleclee1005/AISalesAvatar/img/img/031AzureNetwork.jpg)

---

📝 정보를 확인한 후, **「Create（생성）」** 버튼을 클릭하여 Azure OpenAI 서비스 리소스를 배포하기 시작합니다.

👇 배포 확인 화면은 아래와 같습니다:

![Azure createconfirm](https://raw.githubusercontent.com/aleclee1005/AISalesAvatar/img/img/032AzureReview.jpg)

👇 리소스 배포 중 화면은 아래와 같습니다:

![Azure deploy](https://raw.githubusercontent.com/aleclee1005/AISalesAvatar/img/img/033AzureDeployment.jpg)

---

배포가 완료되면, **Azure AI Foundry**로 이동하여 아래와 같은 환영 화면을 확인할 수 있습니다.  
이 화면에서는 프로젝트를 빠르게 생성하고 모델을 선택할 수 있습니다.

![Azure AI Foundry](https://raw.githubusercontent.com/aleclee1005/AISalesAvatar/img/img/034AzureAIFoundry.jpg)

ChatPlaygroundrg에 들어간 후, Create a deployment를 클릭하여 모델 배포를 생성합니다.

![Azure Create](https://raw.githubusercontent.com/aleclee1005/AISalesAvatar/img/img/055AzureAPIcreate.jpg)

Deploy Model을 클릭한 후, gpt-4o-mini를 선택하고 Confirm을 눌러 확인합니다. 모델 유형은 필요에 따라 유연하게 선택할 수 있습니다.

![Azure mini](https://raw.githubusercontent.com/aleclee1005/AISalesAvatar/img/img/056gpt-4o-mini.jpg)

gpt-4o-mini 배포 페이지에 들어간 후, 필요에 따라 Deployment name을 수정하고, 내용이 정확한지 확인한 뒤 오른쪽 아래의 Deploy 버튼을 클릭하여 배포를 진행합니다.

![Azure deploy](https://raw.githubusercontent.com/aleclee1005/AISalesAvatar/img/img/057miniDeploy.jpg)

배포가 완료되면 해당 페이지로 이동하여, 화면에 표시된 Endpoint, Key, Model Version 정보를 아래 그림과 같이 Dify 설정의 해당 항목에 입력해 주세요.

![Azure endpoint](https://raw.githubusercontent.com/aleclee1005/AISalesAvatar/img/img/058Endpoint.jpg)

다음은 Dify의 Azure 모델 설정 페이지 입력 예시입니다.
이전에 발급받은 Endpoint, Key, Deployment name 등의 정보를 참고하여, 각 항목에 알맞게 입력해 주세요.

![Azure Set](https://raw.githubusercontent.com/aleclee1005/AISalesAvatar/img/img/059DifyAzureSet.jpg)

---

모델 구성이 완료되면, 우리는 실행 환경을 준비했습니다.  
이제 Dify에서 AI Sales Avatar의 지식 본체를 구축할 수 있습니다.

---

### 🧩 Step 2：AI Sales Avatar에 필요한 내부 자료(지식 문서) 업로드

Dify 콘솔 상단 메뉴에서 **「Knowledge」**를 클릭한 후,  
**「Create Knowledge」**를 클릭하여 새로운 지식 데이터 세트를 생성합니다.

![Dify Data](https://raw.githubusercontent.com/aleclee1005/AISalesAvatar/img/img/008Difydatasets.jpg)

다음 페이지에서 자료 업로드 방법을 선택합니다. **「Import from file」** 방식을 사용하는 것이 좋습니다.

👇 아래 그림과 같이:

![DifyUpload](https://raw.githubusercontent.com/aleclee1005/AISalesAvatar/img/img/009DifydataImport.jpg)

준비한 기업 내부 자료를 업로드해주세요. 예를 들어, 제품 소개, 판매 매뉴얼, 자주 묻는 질문 문서 등입니다.  
관련 자료를 아직 준비하지 않으셨다면, ChatGPT를 사용하여 콘텐츠를 생성할 수도 있습니다.

👇 예를 들어, 우리는 ChatGPT를 사용하여 명품차 브랜드 소개 문서(렉서스, 아우디, BMW 등)를 생성했습니다:

![ChatGPTUpload](https://raw.githubusercontent.com/aleclee1005/AISalesAvatar/img/img/010DifydataChatGPT.jpg)

문서를 다운로드한 후, Dify 업로드 페이지로 돌아가 **「Import from file」**을 선택하고 해당 파일을 업로드합니다.  
업로드가 성공적으로 완료되면, 오른쪽 하단의 **「Next」**를 클릭하여 다음 단계로 진행합니다.

![Dify Next](https://raw.githubusercontent.com/aleclee1005/AISalesAvatar/img/img/011DifyImportNext.jpg)

기본 설정은 대부분의 상황에 적합하므로, 원래 설정을 유지한 채 **「Save & Process」**를 클릭하는 것이 좋습니다.  
(추후 스마트 에이전트의 이해도를 향상시키고자 할 경우, 실제 요구에 맞게 관련 파라미터를 조정할 수 있습니다.)

![Dify 知识库配置保存与处理](https://raw.githubusercontent.com/aleclee1005/AISalesAvatar/img/img/012DifyEmbedding.jpg)

✅ 아래 페이지가 보인다면, 문서가 성공적으로 업로드되어 Dify 시스템에서 분석이 완료된 것입니다.

![DifydataSet](https://raw.githubusercontent.com/aleclee1005/AISalesAvatar/img/img/013DifyDataUploadSucess.jpg)

여기까지 우리는 스마트 에이전트 지식 본체 구축을 완료했습니다.  
다음 단계로, 우리는 스마트 에이전트 애플리케이션을 생성하고 이 지식 본체를 연결할 것입니다!

---

### 🧩 Step 3：스마트 에이전트 앱 생성 및 지식 본체 연결

Dify 콘솔에 로그인한 후, 상단 메뉴에서 **「Studio」**를 클릭하고, 오른쪽 상단의 **「Create」**를 클릭하여 새 앱을 생성합니다.

팝업 창에서 다음 내용을 입력합니다:

- **App Name & Icon**：예를 들어 `AI Sales Avatar`
- **Description**：
Your name is Vendy, the AI Clerk of Luxury Cars.
Your task is to provide information about luxury cars to the customers based on the knowledge.

👇 설정 화면은 아래와 같습니다:

![DifyAvatar](https://raw.githubusercontent.com/aleclee1005/AISalesAvatar/img/img/014DifySalesAvatarSetting.jpg)

**Create**를 클릭한 후, 앱의 **Orchestrate** 편집 화면으로 이동합니다.

**INSTRUCTION** 항목에 방금 **Description**과 일치하는 내용을 입력합니다:

Your name is Vendy, the AI Clerk of Luxury Cars.
Your task is to provide information about luxury cars to the customers based on the knowledge.

그런 다음, 아래 **Knowledge** 영역에서 우리가 방금 업로드한 지식 문서를 참고 자료로 선택합니다.

👇 설정 화면은 아래와 같습니다:

![Dify AvatarData](https://raw.githubusercontent.com/aleclee1005/AISalesAvatar/img/img/015DifyAvatarData.jpg)

설정이 완료되면, 오른쪽 입력창에서 지식 본체 내용을 정상적으로 호출할 수 있는지 테스트합니다.  
업로드한 문서 기반으로 내용이 반환된다면, 스마트 에이전트가 성공적으로 연결된 것입니다.  

테스트에 문제가 없으면, 오른쪽 상단의 **「Publish」**를 클릭하여 AI 애플리케이션을 게시합니다.

![Dify AvatarTest](https://raw.githubusercontent.com/aleclee1005/AISalesAvatar/img/img/016DifyAvataRunTest.jpg)

애플리케이션을 게시한 후, 왼쪽 메뉴에서 **「API Access」**를 클릭하고, 그 후 오른쪽 상단의 **「Create Secret Key」**를 클릭합니다.  
이 API Key는 후속 TEN 플랫폼 통합 시 반드시 사용해야 하므로, 꼭 복사하여 저장해두세요.

👇 인터페이스 키 생성 화면은 아래와 같습니다:

![Dify API Key](https://raw.githubusercontent.com/aleclee1005/AISalesAvatar/img/img/018DifyAPI2.jpg)

🎉 축하합니다! 이제 우리는 AI Sales Avatar의 “스마트 에이전트 본체” 구축을 완료했으며,  
호출에 필요한 API Key를 성공적으로 획득했습니다.

다음 단계로, 우리는 **Trulience 플랫폼**에 들어가 AI Sales Avatar의 “디지털 인간 외모 및 연기 능력”을 생성할 것입니다.  
즉, 그녀의 가상 이미지를 구축하여, 그녀가 “듣고, 말하고, 생각하고” 뿐만 아니라, 실제로 사용자 앞에 나타나 사람과 상호작용할 수 있게 만듭니다!

📚 Dify에 대해 더 알아보려면, 공식 기술 문서를 참고하시기 바랍니다:
👉 [https://docs.dify.ai/en/introduction](https://docs.dify.ai/en/introduction)

---

### 🧩 Step 4：Trulience 계정 등록 및 디지털 인간 ID와 액세스 토큰 받기

이제 우리는 AI Sales Avatar에게 시각적인 “디지털 인간 형상”을 부여할 것입니다!  
Trulience 플랫폼을 사용하여 형상을 생성하고, 후속 연결을 위한 **Avatar ID**와 액세스 **Token**을 받습니다.

✅ 절차는 다음과 같습니다:

1️⃣ Trulience 공식 웹사이트 열기: [https://trulience.com](https://trulience.com)  
홈페이지에서 **「Start For Free」** 버튼을 클릭하여 계정 등록을 시작합니다.

👇 페이지 예시 화면은 아래와 같습니다:

![Trulience](https://raw.githubusercontent.com/aleclee1005/AISalesAvatar/img/img/019Trulience.jpg)

2️⃣ 등록을 완료한 후, 백엔드 화면으로 이동합니다. 왼쪽 메뉴에서 **「IMAGE AVATARS」**를 클릭하고,  
여성 캐릭터를 선택하여 **Vendy**의 외모를 설정한 후, 녹색 버튼 **「Create Avatar」**를 클릭하여 디지털 인간을 생성합니다.

👇 선택 및 생성 화면 예시는 아래와 같습니다:

![Trulience Avatar](https://raw.githubusercontent.com/aleclee1005/AISalesAvatar/img/img/020TrulienceAvatar.jpg)

---

3️⃣ **“Avatar created”** 메시지가 표시되면, 디지털 인간이 성공적으로 생성된 것입니다.

👇 생성 성공 메시지 화면은 아래와 같습니다:

![TrulienceAvatar2](https://raw.githubusercontent.com/aleclee1005/AISalesAvatar/img/img/021TrulieceAvatarCreation.jpg)

3️⃣ 왼쪽의 이름을 기본값인 **Amanda**에서 **Vendy**로 변경합니다.  
그때 아래에서 그녀만의 **Avatar ID**를 확인할 수 있습니다.

👇 아래 그림과 같이:

![TrulienceVendy](https://raw.githubusercontent.com/aleclee1005/AISalesAvatar/img/img/022TrulienceAvatarName.jpg)

---

4️⃣ 그 다음, 하단 버튼 **「Connect」**를 클릭하면 브라우저가 새 페이지로 이동합니다.  
웹 주소(URL)에서 `token=` 뒤의 문자열을 복사하세요.  
이것이 바로 당신의 **액세스 토큰**입니다.

**Avatar ID**와 **Token**을 함께 복사하여 저장해 두는 것이 좋습니다.  
나중에 TEN 플랫폼에서 사용할 예정입니다.

---

🎉 축하합니다!  
이제 우리는 AI Sales Avatar의 "**외모 구축**"을 완료했으며, 그녀의 Avatar ID와 액세스 토큰을 성공적으로 획득했습니다!

이제 마지막 단계로 들어갑니다:  
Dify의 스마트 에이전트와 Trulience의 디지털 인간을  
**TEN 플랫폼**에 통합하여, 진정한 "듣고 말하고 생각하고 연기하는" 실시간 음성 AI 에이전트를 구축할 것입니다!

📚 Trulience에 대해 더 알아보려면, 공식 기술 문서를 참고하시기 바랍니다:
👉 [https://www.trulience.com/docs#/](https://www.trulience.com/docs#/)

---

## 🧩 Step 5：TEN Agent 플랫폼을 로컬에서 구축하기 전에 준비해야 할 세 가지 설정

Dify의 스마트 에이전트와 Trulience의 디지털 인간을 TEN 플랫폼에 통합하기 전에,  
우리는 음성 통화 및 음성 인식/합성에 필요한 계정과 키를 미리 준비해야 합니다. 주요 항목은 다음과 같습니다:

---

### ✅ 1. Agora 실시간 음성 통신 파라미터

TEN은 **Agora**를 사용하여 음성 통화 기능("그녀는 말을 한다")을 구현하며, 다음의 파라미터를 준비해야 합니다:

- `AGORA_APP_ID=`（App ID）  
- `AGORA_CERTIFICATE=`（Certificate）

👉 획득 방법:  
Agora 콘솔에 로그인하여 [https://console.agora.io](https://console.agora.io)에서 새 프로젝트를 생성한 후, 위 정보를 확인할 수 있습니다.

👇 콘솔 페이지 예시는 아래와 같습니다:

![Agora Project](https://raw.githubusercontent.com/aleclee1005/AISalesAvatar/img/img/023Agora.jpg)

계정에 로그인한 후, 왼쪽 메뉴에서 **「Projects」**를 클릭하고,  
오른쪽 상단의 **「Create New」**를 클릭하여 새 프로젝트를 생성합니다.

👇 프로젝트 생성 화면 예시는 아래와 같습니다:

![AgoraNew](https://raw.githubusercontent.com/aleclee1005/AISalesAvatar/img/img/024AgoraCreate.jpg)

---

### 📝 입력 항목 설명:

- **Project Name**: `AISalesAvatar`로 입력
- **Use Case**: 적합한 용도를 선택, 예: `Enterprise Collaboration`
- **Authentication Mode**: **Secure Mode: APP ID + Token(추천)** 선택

입력이 완료되면 **「Submit」**를 클릭하여 프로젝트 생성을 완료합니다.

👇 생성 성공 후, App ID와 Certificate를 확인할 수 있습니다:

![Agora APP ID](https://raw.githubusercontent.com/aleclee1005/AISalesAvatar/img/img/025AgoraAPPID.jpg)

프로젝트 생성이 완료되면, 프로젝트 관리 페이지로 이동합니다.  
프로젝트 목록에서 **App ID** 옆의 복사 버튼을 클릭하면 **App ID**를 얻을 수 있습니다.

👇 아래와 같이 표시됩니다:

![AgoraApp IDGet](https://raw.githubusercontent.com/aleclee1005/AISalesAvatar/img/img/026AgoraAPPID2.jpg)

---

App ID를 획득한 후, 프로젝트 오른쪽의 ✏️ **연필 아이콘(편집 버튼)**을 클릭하여 프로젝트 세부 페이지로 이동합니다.

페이지 하단의 **Primary Certificate** 영역에서 오른쪽의 복사 버튼을 클릭하면,  
해당 프로젝트의 **Certificate**를 복사할 수 있습니다.

👇 아래와 같이 표시됩니다:

![Agora Certificate](https://raw.githubusercontent.com/aleclee1005/AISalesAvatar/img/img/027AgoraCertificate.jpg)

이로써, 우리는 **Agora의 App ID와 Primary Certificate**를 성공적으로 획득하였으며,  
후속 TEN 플랫폼에서 음성 통신 기능을 활성화할 준비가 완료되었습니다.

📚 추가로 더 알고 싶으시면, 공식 기술 문서를 참고하시기 바랍니다:
👉 [https://docs.agora.io/en/video-calling/get-started/manage-agora-account?platform=web#create-an-agora-project](https://docs.agora.io/en/video-calling/get-started/manage-agora-account?platform=web#create-an-agora-project)

---

### ✅ 2. Azure Speech 파라미터 (음성 인식 + 음성 합성)

**Azure**는 사용자의 음성을 텍스트(STT)로 변환하고, AI의 응답을 음성(TTS)으로 변환합니다.  
다음 4개의 환경 변수를 준비해야 합니다:

AZURE_STT_KEY= ；AZURE_STT_REGION= ；AZURE_TTS_KEY= ；AZURE_TTS_REGION= 。

---

배포가 완료되였기에, **Azure AI Foundry**로 이동하여 아래와 같은 환영 화면을 확인할 수 있습니다.  
이 화면에서는 프로젝트를 빠르게 생성하고 모델을 선택할 수 있습니다:

![Azure AI Foundry](https://raw.githubusercontent.com/aleclee1005/AISalesAvatar/img/img/034AzureAIFoundry.jpg)

---

**「Model Catalog（모델 카탈로그）」** 페이지로 이동한 후, **Azure AI Speech**를 선택합니다:

![Azure Speech model](https://raw.githubusercontent.com/aleclee1005/AISalesAvatar/img/img/035AzureModels.jpg)

**Azure-AI-Speech** 모델을 클릭한 후, 상세 페이지로 이동합니다.  
페이지 상단의 **「Use Service」** 버튼을 클릭하면 Speech Playground 페이지로 이동합니다:

![Azure Speech entry](https://raw.githubusercontent.com/aleclee1005/AISalesAvatar/img/img/036AzureUseService.jpg)

**Speech Playground**에 들어가서, 자신의 음성 서비스 리소스를 선택합니다(아래 그림과 같이).  
그러면 해당 **API Key**와 **Region**을 확인할 수 있습니다:

![Azure STT KeyRegion](https://raw.githubusercontent.com/aleclee1005/AISalesAvatar/img/img/037AzureSTTKey.jpg)

---

**「Text to Speech」** 탭을 클릭하여 **Voice Gallery**로 들어갑니다.  
여러 가지 음성 스타일을 미리 듣고, 당신의 AI 아바타에 가장 적합한 음성 유형을 선택할 수 있습니다:

![Azure TTS](https://raw.githubusercontent.com/aleclee1005/AISalesAvatar/img/img/038AzureTTSmodels.jpg)

---

**「View Code」**를 클릭하면 현재 음성 서비스의 **API Key와 Region**을 복사할 수 있습니다:

![AzureAPI KeyRegion](https://raw.githubusercontent.com/aleclee1005/AISalesAvatar/img/img/039AzureTTSKey.jpg)

---

🎉 **축하합니다!**  
이제 우리는 **TEN 플랫폼 실행에 필요한 모든 파라미터 준비 작업**을 완료했습니다.

---

### 🧱 다음 단계에서는, 로컬에서 TEN Agent 플랫폼을 공식적으로 시작하고,  
앞서 구축한 모든 모듈들을 연결합니다:

- 🧠 스마트 에이전트 (Dify)
- 🔊 음성 능력 (Azure Speech + Agora)
- 👩‍💻 가상 형상 (Trulience)

**이 모든 모듈을 완벽하게 연결하여, 진정한 "듣고, 말하고, 생각하고 연기하는" 실시간 AI 디지털 판매 도우미를 구축합니다!**

---

📚 추가로 Azure Speech와 OpenAI 서비스 배포에 대해 알아보려면, 공식 문서를 참고하세요:  
👉 [https://learn.microsoft.com/en-us/azure/ai-services/openai/how-to/create-resource?pivots=web-portal](https://learn.microsoft.com/en-us/azure/ai-services/openai/how-to/create-resource?pivots=web-portal)

## 🧩 Step 6：Mac에서 로컬 TEN Agent 개발 환경 배포

AI Sales Avatar의 음성 상호작용 시스템을 실행하고 디버깅하기 위해,  
우리는 로컬에서 **TEN Agent 개발 환경**을 준비해야 합니다.

---

### 🔧 필요한 도구 및 설치 방법 안내:

| 도구      | 기능 설명                        | 설치 방법                                  |
|-----------|------------------------------|------------------------------------------|
| Docker    | TEN의 컨테이너 환경 실행          | 공식 웹사이트에서 Docker Desktop 다운로드 및 설치 |
| Git       | TEN의 코드 저장소 클론 및 관리     | `brew install git`                        |
| Node.js   | 프론트엔드 코드 실행 (Playground) | `brew install node`                       |


---

### ✅ ① Docker 설치

💡 Docker는 TEN 플랫폼의 핵심 실행 환경으로, 모든 모듈은 컨테이너 형태로 배포됩니다.

- 공식 웹사이트 링크 열기: 👉 [https://www.docker.com/products/docker-desktop](https://www.docker.com/products/docker-desktop)  
- macOS용 `.dmg` 설치 파일을 다운로드하여 설치를 완료합니다.
- 설치 후, 애플리케이션 목록에서 Docker 아이콘을 클릭하여 실행합니다.
- 상단 메뉴 바에서 🐳 아이콘이 초록색으로 변할 때까지 기다립니다. 이는 성공적으로 실행되었음을 의미합니다.
- 터미널을 열고 다음 명령어를 입력하여 설치가 성공적으로 이루어졌는지 확인합니다. docker -v


### ✅ ② Git 설치

💡 Git은 TEN 프레임워크 코드의 클론 및 관리에 사용되는 버전 관리 도구입니다.

설치 명령어: `brew install git`; 설치 확인: `git -v`

### ✅ ③ Node.js 설치

💡 Node.js는 TEN의 프론트엔드 Playground 실행에 필수적인 환경입니다.

설치 명령어: `brew install node`; 설치 확인: `node -v`

### ✅ ④ TEN Agent 프레임워크 코드 클론

Docker, Git, Node 설치 후, 다음 단계는 TEN Agent의 소스 코드를 클론하고 .env 환경 변수를 설정하는 것입니다.

🚀 1. TEN Agent 코드 저장소 클론  
터미널에서 다음 명령어를 실행합니다:  
`git clone https://github.com/TEN-Framework/TEN-Agent.git`

실행 후, 로컬에 TEN-Agent 폴더가 생성되며,  
그 안에는 실행에 필요한 모든 코드와 구성 파일이 포함됩니다.

👇 아래와 같은 화면이 표시됩니다:

![TEN Clone](https://raw.githubusercontent.com/aleclee1005/AISalesAvatar/img/img/040TEN.jpg)

📦 2. 프로젝트 디렉토리로 이동하여 환경 변수 템플릿 복사  
`ai_agents` 서브디렉토리로 이동하고 환경 변수 파일을 복사합니다:

cd TEN-Agent/ai_agents
cp .env.example .env

`.env`는 TEN Agent 실행에 필요한 환경 변수 설정 파일입니다.  

👇 예시 화면은 아래와 같습니다:

![TEN Agent .env](https://raw.githubusercontent.com/aleclee1005/AISalesAvatar/img/img/041TEN.jpg)

✍ 3. `.env` 파일 편집하기, 아래 변수 입력

텍스트 편집기(추천: **Cursor** 또는 **VS Code**)를 사용하여 `.env` 파일을 열고 편집합니다.  
파일의 끝에 아래 내용을 추가하고 (자신의 키와 지역 정보를 입력하세요):

Agora App ID 와 Certificate
AGORA_APP_ID=your_agora_app_id
AGORA_APP_CERTIFICATE=your_agora_certificate

Azure 음성 인식(STT) 파라미터
AZURE_STT_KEY=your_stt_key
AZURE_STT_REGION=your_stt_region

Azure 음성 합성(TTS) 파라미터
AZURE_TTS_KEY=your_tts_key
AZURE_TTS_REGION=your_tts_region

👇 `.env` 파일 편집 예시는 아래와 같습니다:

![TEN .env](https://raw.githubusercontent.com/aleclee1005/AISalesAvatar/img/img/042TENCursor.jpg)

## ✅ Step ⑤：TEN Agent 컨테이너 시작, 서버 컴파일 및 실행

`.env` 환경 변수 설정이 완료된 후, 다음 단계는 **TEN Agent의 컨테이너 환경**을 공식적으로 시작하는 것입니다.

---

### 🐳 ① 컨테이너 시작

`ai_agents` 디렉토리로 이동한 후, Docker 컨테이너 서비스를 시작합니다:

cd ai_agents
docker compose up -d

이 명령어는 다음의 컨테이너 서비스를 시작합니다:

- ten_agent_dev: 에이전트를 개발하고 실행하는 용도
- ten_agent_demo: 예시 에이전트
- ten_agent_playground: 프론트엔드 상호작용 페이지

👇 프로젝트 구조 예시는 아래와 같습니다:

![TEN Agent ai_agents 目录结构](https://raw.githubusercontent.com/aleclee1005/AISalesAvatar/img/img/043TENaiagents.jpg)


🔧 ② 컨테이너에 들어가서 Agent 서버 컴파일

다음 명령어를 실행하여 개발 컨테이너로 들어갑니다:  
`docker exec -it ten_agent_dev bash`

컨테이너에 들어가면 초기화 작업 스크립트를 실행하여 Agent를 등록합니다:  
`task use`

👇 프로젝트 구조 예시는 아래와 같습니다:

![task use](https://raw.githubusercontent.com/aleclee1005/AISalesAvatar/img/img/044TENtaskuse.jpg)

이 명령어는 자동으로 Agent의 설정 파일(`manifest.json` 및 `property.json`)을 읽고 연결하며,  
필요한 의존 패키지를 자동으로 설치합니다.

👇 실행 과정 예시는 아래와 같습니다:

![TEN task run](https://raw.githubusercontent.com/aleclee1005/AISalesAvatar/img/img/045TENTaskRun.jpg)

✅ `task run`을 완료한 후, 브라우저에서 아래 주소로 접속하여 프론트엔드 페이지를 엽니다:

👉 [https://localhost:49483]

실행에 성공하면, 다음과 같은 화면이 표시됩니다:

페이지 상단의 **「Graph」** 탭을 클릭합니다.

드롭다운 메뉴에서 선택합니다:  
➡️ **`voice_assistant_intergrated_stt (Auto Start)`**  
그런 다음, 오른쪽 하단의 **「Save」**를 클릭하여 설정을 저장합니다.

👇 페이지 예시는 아래와 같습니다:

![TEN Agent Playground](https://raw.githubusercontent.com/aleclee1005/AISalesAvatar/img/img/046TEN494483.jpg)

✅ 음성 합성(TTS) 모듈을 **Azure 엔진**으로 교체하기

1. 그림에서 **TTS 모듈**(예: `tts_default`)을 찾습니다.  
2. 해당 모듈을 마우스 오른쪽 버튼으로 클릭하고, **「Replace Node with」**를 선택합니다.  
3. 팝업 목록에서 **`azure_tts`**를 선택합니다.

이로써 음성 합성 모듈이 교체되었습니다.

👇 Azure TTS 모듈 교체 예시는 아래와 같습니다:

![TEN Agent Azure TTS Change](https://raw.githubusercontent.com/aleclee1005/AISalesAvatar/img/img/047TENAzuretts.jpg)

🎙️ 디지털 인간의 음성 설정 (TTS 음성)

우리는 디지털 인간의 이미지에 맞춰 그녀의 음성을 커스터마이즈할 수 있습니다.  
Microsoft에서 제공하는 음성 서비스 페이지에는 지원되는 모든 음성 이름이 나와 있습니다.

👉 방문 주소는 아래와 같습니다:

[https://learn.microsoft.com/en-us/azure/ai-services/speech-service/language-support?tabs=tts#multilingual-voices](https://learn.microsoft.com/en-us/azure/ai-services/speech-service/language-support?tabs=tts#multilingual-voices)

---

이 예시에서는 영어 여성 음성인:  
🗣️ **`en-US-AshleyNeural`**을 선택합니다.

Azure TTS 모듈에서, 아래 필드를 다음과 같이 입력합니다:  
Azure_synthesis_voice_name=en-US-AshleyNeural

👇 Azure TTS 음성 이름 설정 예시는 아래와 같습니다:

![TEN Azure_synthesis_voice_name](https://raw.githubusercontent.com/aleclee1005/AISalesAvatar/img/img/048TENAzureVoice.jpg)

🔁 LLM 모듈을 Dify 인터페이스로 교체하여 Dify 스마트 에이전트 연결하기

1. **`llm` 모듈**을 마우스 오른쪽 버튼으로 클릭하고, **「Replace Node with」**를 선택합니다.  
2. 팝업 목록에서 **`dify_python`**을 선택합니다.

이렇게 하면 TEN Agent의 대형 언어 모델(LLM) 모듈을 Dify에서 제공하는 스마트 에이전트 인터페이스로 연결할 수 있습니다.

👇 작업 예시는 아래와 같습니다:

![TEN Agent Dify](https://raw.githubusercontent.com/aleclee1005/AISalesAvatar/img/img/049TENDifyAPI.jpg)

2️⃣ 교체 완료 후, 새로 생성된 **`dify_python`** 모듈을 마우스 오른쪽 버튼으로 클릭하고,  
**「Update Properties」**를 클릭하여 속성 설정 페이지로 이동합니다.

- **API Key** 필드에 Dify 플랫폼에서 생성한 API Key를 입력합니다.  
- **Greeting** 필드에서 필요에 따라 환영 인사(예: 음성으로 인사)를 커스터마이즈할 수 있습니다.

👇 설정 화면 예시는 아래와 같습니다:

![TEN AgentDify API KeyGreeting](https://raw.githubusercontent.com/aleclee1005/AISalesAvatar/img/img/050TENDifyAPI2.jpg)

✅ TEN Agent 시작 및 Trulience 디지털 인간 연결

---

### 🚀 프론트엔드 페이지 시작

설정이 완료된 후, 브라우저를 열고 아래 주소로 접속하여 TEN Agent 시작 화면으로 이동합니다:

👉 [http://localhost:3000](http://localhost:3000)

👇 페이지 예시는 아래와 같습니다:

![TEN Agent](https://raw.githubusercontent.com/aleclee1005/AISalesAvatar/img/img/051TEN3000.jpg)

🧠 스마트 에이전트 흐름도(그래프) 선택

1. 오른쪽 상단의 **「Select Graph」**를 클릭하고, 드롭다운 메뉴에서 선택합니다:  
   ➤ `voice_assistant_integrated_stt`

2. **「Enable Trulience Avatar」**를 체크하고, 다음 필드를 입력합니다:

   - **Avatar ID** (Trulience에서 디지털 인간을 생성할 때 얻은 ID)
   - **Avatar Token** (Connect를 클릭한 후, 브라우저 주소창에서 복사)

3. 입력을 완료한 후, **「Save changes」**를 클릭하여 설정을 저장합니다.

👇 설정 화면은 아래와 같습니다:

![TEN AgentTrulience](https://raw.githubusercontent.com/aleclee1005/AISalesAvatar/img/img/052TENTrulienceGrah.jpg)

🗣️ 음성 상호작용 시작, 디지털 인간의 연결 성공 여부 테스트

✅ 오른쪽 상단의 **「Connect」** 버튼을 클릭하여 마지막 테스트를 완료합니다.

모든 설정이 올바르게 되었다면, 다음과 같은 상황이 발생합니다:

- 🧍 디지털 인간의 형상이 자동으로 로드되어 표시됩니다.  
- 🗣️ 그녀는 자연스러운 음성으로 인사하고 질문을 합니다. 예:  
  _“어떤 고급차를 소개해 드릴까요?”_

- 🤖 그녀의 답변을 통해, Dify 지식베이스의 내용을 성공적으로 읽고 이해했는지 확인할 수 있습니다.

👇 실행 예시는 아래와 같습니다:

![TEN AgentTalk](https://raw.githubusercontent.com/aleclee1005/AISalesAvatar/img/img/053TrulienceDifyFinal.jpg)

🎯 축하합니다! 이제 완전한 **AI Sales Avatar**를 보유하게 되었습니다!

---
✅ **OpenAI / Dify**의 채팅 두뇌  
✅ **Azure**의 자연 음성 합성 능력 (여성 음성)  
✅ **Trulience**의 디지털 인간 형상  
✅ **TEN 플랫폼**에서 구축된 음성 상호작용 능력
---
🌟 이것이 바로 AI 에이전트의 가장 핵심적인 완전한 연결 고리:  
**“듣기 → 생각하기 → 말하기 → 연기하기 → 연결하기”**
---

📚 추가로 더 알고 싶으시면, TEN 공식 기술 문서를 참고하시기 바랍니다:

👉 [https://theten.ai/docs/ten_agent/architecture_flow](https://theten.ai/docs/ten_agent/architecture_flow)

## 🛠️ 다음 단계 확장 제안 (AX 아키텍처 기반)

현재 구축된 「AI Sales Avatar」를 바탕으로,  
우리는 **AX 아키텍처** 경로를 따라 실제 비즈니스 환경에서의 능력을 더욱 확장할 수 있습니다.  
점진적으로 연결을 완성합니다:  
**데이터 → 모델 → 에이전트 → 사용자 인터페이스 → 전체 비즈니스 생애 주기 관리** 의 닫힌 루프.

---

### 🧑‍💼 웹사이트 홈 페이지에 임베드하여 회사의 가상 이미지 대표로 활용

**Trulience**의 D-Human & Avatar 기능을 결합하여,  
현재 디지털 인간을 회사의 홈페이지 또는 웹 애플리케이션에 배치하고,  
자연스러운 음성 질문 응답을 통해 방문자를 안내하고 의도를 수집하며,  
사용자를 중심으로 한 입구를 구축하여 다음을 지원합니다:

- `Marketing Info`  
- `Customer Lifecycle`

---

### 📦 데이터베이스 & 주문 관리 시스템 접속, "AI 세일즈 대표"로 발전

Avatar를 회사의 내부 시스템과 연동합니다. 예를 들어:

- CRM, ERP, OA, 주문 시스템 (Salesforce, SAP, Notion DB 등)

실현할 수 있는 기능:
- 판매 리드 관리  
- 재고 조회  
- 계약서 생성 등 폐쇄형 작업
서비스 대상:

- `Contract Lifecycle`  
- `Asset Lifecycle`
---

### 🔗 기업 핵심 플랫폼과의 연동: ‘개인 활용’에서 ‘조직 단위 협업’으로

Agent PF(플랫폼)의 기능을 모듈화하여,  
각 BU의 데이터 레이크(Data Lake) 및 업무 플로우 관리 플랫폼에 유연하게 연계함으로써,  
다양한 업무 영역에서의 확장과 통합을 시도해 보았습니다:

- AI + 재무(Finance)  
- AI + 인사(HR)  
- AI + 연구개발(R&D)  
- AI + 협업(SNS)

이를 통해, 기업 전체의 AI 전환과 고도화를 조금이나마 지원할 수 있기를 바라는 마음입니다.

## ✨ 마지막으로: 한마디 감상

저는 항상 믿습니다. AI는 단지 차갑고 강력한 도구가 아니라,  
인간의 따뜻한 파트너이자, 개인 능력의 확장과 증대기능을 가진 존재가 되어야 한다고.

미래에는 아마도 “**Vendy**”와 같은 디지털 파트너들이 세계 곳곳에서 조용히 태어나게 될 것입니다.  
그들은 **듣고, 생각하고, 반응하고, 표현**하며, 기술의 힘으로 인간의 존엄성과 창의력을 지키고 있을 것입니다.

---

📣 만약 여러분도 이 글로벌 공창의 여정에 동참하고 싶다면,  
함께 탐구(探索)하고 공동창작(共創)하며, 모든 개인이 AI와 함께 성장할 기회를 가질 수 있도록　임파워먼트(賦能)하면서,  
**“일기당천, 누구도 놓치지 않는”** AX 신시대를 함께 탐험해봅시다.

---

이 문서는 작은 시도이자 기록으로 남기고자 합니다.  
그것이 작은 씨앗이 되어,  
인간과 AI가 조화롭게 공생하는 미래에서 **조용히 뿌리를 내리고, 천천히 싹을 틔우기를** 바랍니다.



