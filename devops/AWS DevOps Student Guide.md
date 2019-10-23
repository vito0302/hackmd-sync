# AWS DevOps Student Guide

###### tags: `devops`

 ## Module 0: Course Overview

* 簡介

## Module 1: Introduction to DevOps

* Development + Operations = DevOps

### DevOps Overview

#### DevOps Goal

* 建立一個continous delivery 的模型，具備下列特徵
  * repeatable
  * reliable
  * stable
  * resilient
    * AWS說的彈性應該是容錯能力，例如有一台ELB壞掉，可以用另外一台來代替
  * secure

#### DevOps的優點

* Speed
  * 這邊應該是說因爲dev與ops互相合作，可以快速的進行創新、面對市場、或增加效率。
* Rapid Delivery
  * 因爲有快速的release，可以快速的改進產品，修改bug，或對付客戶需求
  * 這邊主要是說CI/CD可以自動化部署，然後可以對應上述需求。
* Reliability
  * 保證app質量與基礎架構質量，因此可以更快速的部署，並帶給user正向的經驗。
  * 使用CI/CD來測試每個變更是使用且安全的。
* Scale
  * 要有規模化的管理基礎設施與開發環境，可以利用自動化與一致性的特性，有效且風險低來管理複雜或易變動的系統
* Improved Collaboration
  * 在DevOps文化下建立有效能的團隊
* Security
  * 利用自動偵測的合規策略，精細度控制，以及configuration management來保證安全性。
    * systemConfig可以偵測相關設定是否合規

#### DevOps文化

* DevOps是要移除development與operations之間的隔閡。
* 兩方會是同一個team並互相合作
* DevOps座右銘: People over process over tools

#### 爲什麼使用AWS DevOps

* AWS Service簡化了供裝流程、基礎設施管理、程式碼部署、程式碼自動發布流程、監控application與基礎設施效能。
* 使用AWS DevOps有下列優點
  * Get Started Fast
    * 很多服務都是全託管，開箱就能用。
  * Fully Managed Services
    * 都是全託管服務，不用自行管理
  * Build for scale
    * 可以建置大規模的系統
  * Programmable
    * AWS各項服務都可以用程式控制。
  * Automation
    * AWS可以協助將各項工作自動化
  * Secure
    * 使用AWS IAM來進行權限控管

### The DevOps Practices

#### Benefits of DevOps

* Continuous Integration
  * 是一種開發者方面的實踐，時常的將程式碼Check in到repository,然後自動化的進行build與test。
* Continuous Delivery
  * 是一種開發者方面的實踐，當程式碼異動時，可以auto build,tested,並準備release.
  * CD是CI的一種擴展，當程式碼異動時，可以自動的發布到測試、正式環境。
* Microservices
  * 就是微服務
* Infrastructure as Code
  * 利用code以及軟體開發技術來管理基礎設施，例如version control以及CI。
* Monitoring and Logging
  * 監控與記錄app的性能，用來改善app.
* Communication and Collaboration
  * 是devops關鍵文化之一，將developer與operation結合在一起。

#### DevOps Tooling by AWS

* Version Control
  * AWS CodeCommit
* CI/CD
  * AWS CodePipeline
  * AWS CodeBuild
  * AWS CodeDeploy
  * AWS CodeStar
* Microservice
  * ECS
  * Lambda
* Platform as a Service
  * Elastic Beanstalk
* Infrastructure as code
  * CloudFormation
  * AWS OpsWork
  * System Manager
* Monitoring and Logging
  * Cloudwatch
  * Cloudtrail
  * AWS Config
  * AWS X-ray

#### Components of DevOps Practice

* 有三個主要面向
  * Continuous Integration
  * Continuous Delivery
  * Continuous Monitoring and Management
* 最佳實踐就是將所有的Component都自動化
  * 然後說明自動化的優點
  * 在成功的DevOps環境，Infrastructure都是被轉爲code進行管理的。

#### Continuous Integration and Delivery Pipeline

* Code->Build->Test->Provision->Deploy->Monitor
  * 前三個屬於Continuous Integration,其它可視爲Delivery,management.

#### Continuous Delivery

* 對於Continuous Delivery model，對於下述流程的自動化是非常重要的:
  * 供裝與設定測試環境與正式環境
  * 部署到測試環境與正式環境
  * 可以部署到各式環境，例如alpha,beta,staging
  * 程式測試也要分成多個面向，例如functionality,security,compliance,performance。

#### Continuous Monitoring and improvement

* 要補抓、分類、分析從應用程式與基礎設施產生的資料與log.
* 要了解性能、影響(這邊是指對用戶的影響)、與問題
* 依照metrics analysis持續改進
* 在DevOps面向與應用程式面向都有相關的metrics，在p40頁有列出來。

#### Infrastructure as Code

* 就說明IOC的優點

#### Configuration Management

* Configuration Management是用來處理將基礎設施與應用程式進行自動化流程與標準化流程的工具。
* 可作爲IOC的工具，並可以執行大部分作業系統的管理任務。
* 依賴這些自動化與標準化流程，可以極少因爲設定錯誤導致的錯誤。
* Configuration文件可以搭配版本控制，利用版本控制來記錄configuration 的改變。

## Module 2: AWS Command Line Interface

#### Module Overview

* Install and configure
* Command Line options
  * Profile
  * Output
  * Query
  * Filter
  * Wait

#### Basic Structure

* aws <service> <operation>
  * example : aws ec2 describe-instance

#### AWS CLI Configure

* AWS Access Key Id
* AWS Secret Access Key
  * 建立iam user時，
* Default Region name
* Default output format

#### Configuration settings are written out to two files

* /.aws/credentials
  * access key跟secret key會存在這邊
* ./aws/config
  * 相關設定檔會存在這邊

#### Advanced Structures on AWS CLI Command

* aws <option> <service> <operation> <parameters>
  * option包含Debugging,output format,queries,filters,profiles,region.
* Example
  * aws --region us-west-2 ec2 describe-instance i-abc123yz
* Query與Filter
  * Query
    * Use JMESPath to filter response,是在Client端處理
  * Filter
    * is used to restrict the result set,會在API endpoint上面處理，也就是在server端處理
* wait指令
  * 透過wait指令，會使用poll方式去詢問目前資源狀態，然後poll一定次數後就會回報錯誤。
  * 也可以用在cloudformation上，會在嘗試120次後回傳錯誤。
  
* 優先順序如下
  * Command line options
  * Environment variables
  * The AWS credentials file(~./aws/credentials)
  * The CLI config file
  * Container credentials (provided by the Amazon Elastic Container Service)
  * Instance profile credentials (used on EC2 )

## Module 3 Introduction to DevSecOps

#### Model Overview

* 了解在DevOps流程中，與安全相關議題的重要性
* 討論AWS Security practices
* 相關的服務
  * IAM
* 安全性等級通常由stakeholder決定要執行到那個等級。

#### Why does DevSecOps Matter

* DevSecOps
  * Validate building blocks without slowing lifecycle
* 在組織中有一些DevSecOps的方法
  * 與security teams合作，從設計時就要考慮安全問題
  * 自動化持續進行安全測試，並且將安全測試流程加入pipeline中
  * 延伸Monitor到安全性與合規性，monitor必須包含alerting,automated remediation,quarantine of resources marked as non-compliant.
    * 告警、自動修復，不合規的數量

#### DevSecOps Principles(1)

* 與所有stakeholder合作
* 將所有事物都codify
* 對所有事物都進行測試
* 將所有事物都自動化
* 對所有事物都進行監控與測量
* 持續接收回饋訊息

#### DevSecOps Principles(2)

* Security of the CI/CD pipeline
  * access role
  * Hardening build servers/nodes (這些伺服器都要進行安全強化)
* Security in the CI/CD pipeline
  * Artifact validation (應該是說不能被篡改)
  * static code analysis
* Infrastructure automation
  * 對於建立account與resource的template要有安全性
  * 彈性的資源驗證與治理 (這邊看起來應該是要管理自己的雲端資源)
  * 自動化事件整治
  * 持續的法規驗證

#### DevSecOps is Automated,Continuous and Visible

* 這邊是在說在DevOps流程中，加入DevSecOps元素　(p101)
* Code階段
  * scan for secrets
* Build階段
  * Tag Security Artifacts
    * 這邊感覺是在說透過工具，掃描是否有安全性弱點
  * Test Security meets standard
* Deploy/Porvision
  * Deploy/Register security components
    * 應該是部署時也要將security元件也部署上去
* Monitor
  * Monitor Security Standard

#### What Does DevSecOps CI/CD give us

* 確認程式碼有依循安全規則
* 避免infrastructure/application因爲不一樣的安全設定，導致部署錯誤
* 依循DevOps創新的步伐(pace of innovation)
  * 這邊的創新可能是導入DevSecOps
* Audit and Alert
* Security at scale(大規模安全)

#### Best Practices

* 將[合規狀態]做成一個容易檢視的樣子
* 自動修復critical event
* 自動deployment to production

### Identity and Access Management(IAM)

#### IAM - Quick Recap

* 建立account
* 建立long term credentials like access key
* Organize identities into common groups
  * 這邊是再說將user加入到group，然後把權限assign給group.
* provider API conditional access by iam policy
* Enable cross-account access
* Configure federated access
  * 投影片寫包含access key ,secret key,以及security token
  * [問題] 怎麼會有access key ,secret key
* Create IAM role for API access

#### Temporary Credentials

* 有三個情境可以使用
  * IAM Roles
  * Cross-account access
  * Identity federation

#### AWS Security Token Service

* https://docs.aws.amazon.com/zh_tw/IAM/latest/UserGuide/id_roles_providers_oidc_cognito.html

#### Switch Roles

* 這個主題感覺是在講不同account間的user，要存取對方資源
  * 一個情境是develop account中的user,要存取production account中的資源，這個時候就可以使用switch roles.
  * https://shazi.info/%E5%9C%A8-aws-%E7%94%A8-switch-role-%E7%9A%84%E6%96%B9%E5%BC%8F%E7%AE%A1%E7%90%86%E5%A4%9A%E5%80%8B-account/

#### Important Points About MFA Protection for APIS

* 只能使用臨時安全性方法登入(role)，透過assumeRole或GetSessionToken來取得
* 不能使用AWS account credentials來呼叫MFA保護的API
* 不能使用long-term credentials(IAM access key) 來呼叫MFA保護的API
* 不能使用federated users的權限來呼叫MFA保護的API
* API呼叫條件要包含MFA，才會強制使用MFA.
* 如果允許其它account(trusted account)來呼叫自己的資源，雖然有開MFA，但是還是要確定trusted account是否有依照MFA最佳實踐進行設定，這部分自己是管理不到的。
  * trusted account
    * 對方的account

#### AWS Organizations

* 可以建立aws account的groups
* 可以附加Service Control Policies(SCPs)到groups上
* 可以透過AWS Organization API建立新帳號，並加入Organization中
  * 這邊不確定是否需要新帳號同意才能加入。
* Organization Group稱爲: OU
* 統一管理與附加policys,可以以OU爲單位，也可以是單獨的AWS Account.
* 將多個帳號的帳單統一起來
* AWS CloudTrail支援AWS Organizations

#### AWS Security Account Structures

* https://d0.awsstatic.com/aws-answers/AWS_Multi_Account_Security_Strategy.pdf
* https://aws.amazon.com/tw/answers/account-management/aws-multi-account-billing-strategy/
* 第一份文件提到何時可以建立Security Account Structure
  * 希望用一個account管理iam users,另外一個帳號管理federated users
  * 希望統一store,secure,analyze,and report AWS 服務的log（CloudTrail,Config,S3..）
  * 在多個account下，都使用security與compliance的baseline
  * 希望統一approve EC2,AMIS,aws product等等。
* Identity Account Structure
  * 將所有使用者都建立在一個特定帳號，然後其它帳號只有資源，user透過role去執行動作。
* Logging Account Structure
  * 用於想要將log統一收容，其它account可以透過api,將cloudtrail,config,或其它服務的log丟過來。
* Publishing Account Structure
  * 將產品定在product account下，其它account來使用。
* Information Security Account
  * 是hybrid AWSS Security Account Structure的一種
  * 舉例來說，如果有一羣做安全分析的使用者，可以建立在這個account下，另外這個account還有S3可以收集其它account的log。而這個account的使用者，可以去其它account的資源，設定跟log收集或安全分析有關的設定。
* Central IT Account
  * 看起來跟information security account有點像，加入AD server.

#### AWS IAM Policy Validator

* 就是驗證iam policy是否有正確，只有支援josn

#### AWS Config

* 可以參考sysops的記錄

#### Secret Management

* 要思考如何包含credentials
  * 例如private key pairs,access/secret keys,database password,internal service credentials
* solution
  * 使用IAM Role取代access.secret keys
  * 考慮使用AWS KMS來保護key pairs
  * 使用一些host-level的加密，避免儲存明碼

#### Using AWS Systems Manager Parameter Store

* 看起來加密要透過KMS

#### Best Practices for Creating Parameters in a Parameter Store

* 建立一個長期維護的naming system

#### Additoinal Storage Options

* AWS Secrets Manager
  * 看起來是儲存機敏資料的服務，會使用kms進行加密
  * 支援credential rotation
* AWS License Manager
  * 使用 AWS License Manager，可在 AWS 和本地服务器上轻松地管理来自 Microsoft、SAP、Oracle、IBM 等软件供应商的许可证
    * [問題]所以應該只有支援特定的軟體供應商?
  * 管理员可以使用这些规则来限制许可违规
  * 主要用在ec2，文件有提到地端也可以用，看起來是偵測機器，然後進行許可或限制。

#### Amazon GuardDuty

* sysops的書上有提到一些。
* (review)投影片看起來提到更多，看題目後再回來看。
* 只有提供威脅偵測，而不會保護。

#### Amazon Macie

* 目前只有支援S3
* Macie使用machine learning 來發現、分類、保護data,可以協助用戶發現有哪些機敏資料被儲存，以及如何被存取，包含使用者認證與access pattern.
* 可以將任何發現的事情送到cloudwatch event,可以利用事件建立告警或建議系統

## Module 4: Deployment Strategies and Developer Tools

#### Module Overview

* Goal: 了解不同的部署策略與部署工具
  * Deployment strategies
    * in-place,rolling,blue-green
  * aws tools for deployment
  * 識別aws用來建立ci/cd pipeline的工具

### Deployment Strategies

#### Continuous Deployment Strategies

* In Place Updates
  * 原機升降，會有downtime
* Rolling Updates
  * 慢慢抽換，使用者可能用到舊的，也有可能用到新的
* Blue-Green
  * 逐漸的將已經存在的instance(blue)，換成新版(green)
    * 這個是投影片寫的
  * 看起來比較像是先拿出一台舊的進行更新，然後驗證，再把流量慢慢導過來
    * 跟rolling update的差別應該是導流量的部分
  * 後面投影片(p119)有寫，是建立一個相同的環境，然後切換流量
* Red-Black
  * 約定一個時間，立刻進行切換
* Immutable
  * 直接建立另一套新的，然後將流量導過來

#### Why are in-place updates benificial

* 快速部署
  * 因爲不用建立其它機器
* 花費低
* 最小downtime
* 可以使用的工具
  * CodeDepoly
  * Beanstalk
  * Opswork

#### Rolling Deployment

* zero downtime
* 可以使用的工具
  * Beanstalk
  * CodeDeploy

#### Benifits over rolling update

* zero downtime
* 部署時間會比in-place多一點
* 可降低風險

#### What is Blue/Green Deployment

* 建立一個相同的環境，然後切換流量
* 相關的元件
  * DNS
  * Load balancer
  * EC2 Auto Scaling

#### Managing Continuous Deployment Rollout

* Roll out new EC2 Auto Scaling instance
  * 這個看不太懂，感覺應該是爲新版本建立新的scaling group
* 對不同版本提供不同的load balance
  * 這樣dns只要切換不同load balance就可以
* 使用route 53慢慢將流量導過來(gradually shift traffic)
* 使用route 53 執行cutover,將流量從old version to new version

#### Blue/Green DNS Gradual Cutover

* 就是在說使用DNS+ELB，慢慢把流量導到新的版本

#### Blue/Green Deployment via EC2 Auto Scaling

* 只有使用一個elb,透過更改scaling gruop裡面的ec2個數，慢慢進行切換

#### Benifits of Blue/Green updates

* zero downtime
* 有時間可以進行客制化部署
  * 因爲部署一個新環境，如果有需要可以進行調整
* Easy rollback
* 可以使用的工具
  * CodeDeploy
  * Beanstalk
  * Opswork
  * CloudFormation

#### Dark Launches with Feature Flags

* 又稱金絲雀發布(Gray release)
* 是为了能够让用户逐步过渡到新功能一种发布方式。 一般是产品上线一个功能，希望在线上可以进行A/B testing，即让一部分用户继续用产品特性A，一部分用户开始用产品特性B，如果用户对B没有什么反对意见，那么逐步扩大范围，把所有用户都迁移到B上面来。
* 透過開關來決定是否發布新功能
  * 也可以有些機器開，有些機器關，讓用戶測試
* 允許在production 環境進行測試
* 投影片說的很簡單，這邊有更詳細的資料
  * https://blog.csdn.net/zzhongcy/article/details/99643828

#### Immutable of Disposable Upgrades

* 使用與系統有未知的依賴，當舊系統已經被patch到不知道如何更新時，可以使用這種部署。
* 欲執行不可變環境更新，Elastic Beanstalk 會於環境負載平衡器後方建立第二個臨時 Auto Scaling 群組，以容納新的執行個體。首先，Elastic Beanstalk 會於新群組內，使用新組態來啟動單一執行個體。此執行個體會處理流量，搭配執行之前組態的原始 Auto Scaling 群組中的所有執行個體運作。
* 第一個執行個體通過運作狀態檢查後，Elastic Beanstalk 會使用新組態來啟動額外的執行個體，總執行個體數量與原始 Auto Scaling 群組內執行的數量相符。所有新執行個體通過運作狀態檢查後，Elastic Beanstalk 會將其傳輸至原始 Auto Scaling 群組內，並終止臨時 Auto Scaling 群組和舊的執行個體。
* https://docs.aws.amazon.com/zh_tw/elasticbeanstalk/latest/dg/environmentmgmt-updates-immutable.html
* 是rolling update的替代選項，使用immutable會造成ec2的爆量餘額消失
* 使用情境
  * 快速且自動rollback
  * 永遠部署新的instance
  * zero downtime
  * 維護完整的capacity
    * rolling update會有一段時間的伺服器是比較少的



## Developer Tools for CI/CD

* 相關的服務
  * AWS Cloud9
  * AWS CodeCommit
  * AWS CodeBuild
  * AWS CodeDeploy
  * AWS CodePipeline
  * AWS CodeStar

#### Challenges with CI Tools

* Long build
* Huge volume of build
* complex build with dependencies
* no scalability
* Developer / QA wait time

#### How Does AWS Solve the Challenge

* Initiate build via aws codeCommit,github,amazon s3
* on-demand comput and pay-as-you-go model
* 連接codepipeline來實作ci/cd
* 經由iam限制權限
* 提供已經事先建好的build environment,並包含build tools，例如maven,npm,gradle.
* scale automatically to meet peak build request

#### AWS CodeStar

* 可以在AWS上快速開發，建立，與部署應用程式。CodeStar可以從單一位置管理軟體的開發活動，在最短時間設定整個持續交付工具鍊。
* CodeStar將程式碼放在AWS Commit,使用CodeBuild建置，使用codepile進行ci/cd.
* 與cloud9整合，也可以與eclipse,visual studio整合。

#### AWS cloud9

* 一個雲端IDE

## Module 5: Infrastructure as Code

#### Module Overview

* 了解IAC的優點
  * 討論iac的概念與優點
  * cloudformation的核心
  * 了解如何利用cloudformation實現automated infrastructure management

#### Benefits of infrastructure as code

* 像管理程式碼一樣管理infrastructure
* 重複且可靠的建立infrastructure
* 建立最新的infrastructure給app
* Cost savings (因爲人力不用花費那麼多)

#### Key Features

* DependsOn
  * 等待特定resource建立完成
  * 用 `DependsOn` 属性可以指定特定资源紧跟着另一个资源创建。在您为资源添加 `DependsOn` 属性时，该资源仅在创建 `DependsOn` 属性中指定的资源之后创建。
* CreationPolicy
  * 定義一段等待時間，等待特定資源完成(等候建立訊號)
  * 可以設定count與timeout
  * 只有支援AWS::AutoScaling::AutoScalingGroup、AWS::EC2::Instance 和 AWS::CloudFormation::WaitCondition
* UpdatePolicy
  * 定義scaling group launch時，resources如何被replace.
  * 可以用在scaling group,lambda等等。
* DeletePolicy
* UpdateReplacePolicy
  * 当资源在堆栈更新操作期间被替换时，使用 UpdateReplacePolicy 属性保留或（在某些情况下）备份资源的现有物理实例。

#### Custom Resources

* 使用lambda來決定如何呼叫custom resource，cloudforamtion則是呼叫lambda
* 看起來一般做法都是呼叫一個restful網址，然後依照回傳訊息往後續處理

#### Quality input: Making most out of parameters

* 就說宣告參數的輸入限制，例如string,int之類的。

#### Managing Stacks

* All in one ?
* Layer ? 
* Microservices ?
* 有提到nested stack,microservice,與chain stack(不同stack透過export與import讀取參數)

#### Updating Stacks

* Updates with no interruption
  * resource更新時，服務不會中斷
    * 例如更改clodwatch::alarm
* Update with Some Interruption
  * 服務會中斷
    * 例如ec2
* Replacement
  * 服務的id會變化
    * 例如更新RDS
* 相關資訊可以參考aws-template-resource-type的文件說明，裡面會描述每種服務更新時候，會用那種策略。

#### Change Sets

* Change sets提供下列功能
  * 可以preivew 異動的部分
  * 可以看到影響了哪些resources
  * 驗證是否會刪除或replace重要的資源
* 只有在確認執行，cloudformation才會執行changeset
  * 如果想要看其它的異動，要建立另外的changeset

#### AWS CloudFormation Stack Sets

* 透過一次性操作，可以跨帳戶與region來新增、異動與刪除資源
* 使用管理者帳戶定義aws template，並可以將這個template跨帳戶的進行供裝
* 只有管理員帳號可以建立stack set.

#### AWS CloudFormation Helper Scripts

* cfn-init
  * 一次性的執行cloudformation metadata,典型的情境是資訊user data
  * 看起來應該就是cloud-init
* cfn-hup
  * 監控cloudformation metadata,並在發現metadata有異動的時候執行metadata。
  * 要進行設定，否則就算metadata有異動，也不會執行。
* cfn-signal
  * 發出訊號給creationpolicy 或 wait condition
* cfn-get-metadata
  * 取得meta-data

#### How Does cfn-hub Work?

* 使用polling的方法進行偵測
* 當偵測到異動時，執行user指定的動作
* 修改metadata經由updateStack api call.

#### What is a stack policy

* 可以利用stack policy避免資源被不小心異動或刪除
* stackPolicy是用在stack異動，避免誤修改相關資源的策略。不要用stackPolicy做權限，而是使用IAM.
* stackPolicy只要設定了，這個stack裡面的資源都是被保護的，不管policy是不是有特別說明某個資源

#### What is a deletionPolicy

* 說明資源被刪除時，應該要做什麼動作
  * Delete
  * Retain
  * Snapshot

## Module6: Deep Dive into AWS Developer Tools

* 說明aws develop tools
* best practices,user case,architecture for develop tools

### AWS Cloud9 Integrated Development Environment

* 開發的東西可以透過code star進行部署

### Continuous Integration with AWS CodeCommit

* 存取CodeCommit應該還是透過IAM的access key跟secret key.
* 可以利用iam區分三種權限
  * AWSCodeCommitFullAccess
    * 最高權限
  * AWSCodeCommitPowerUser
    * 除了不能刪除repo，其它都可以
  * AWSCodeCommitReadOnly
  * 只能pull，不能push
* 透過KMS將內容加密

#### Enabling continuous integration with build automation

* 提到使用hook做觸發CI的工作

#### Scalable CI Soution with AWS CodeBuild

* 網路上提到jenkins做scalable後的優點
  * https://www.blazemeter.com/blog/how-to-setup-scalable-jenkins-on-top-of-a-kubernetes-cluster/
  * the ability to run many more build plans in parallel 
  * automatically replacing corrupted Jenkins instances
  * automatically spinning up and removing slaves based on need, which saves costs
  * distributing the load across different physical machines while keeping required resources available for each specific build plan

#### Securing Your Builds

* 要設定權限，限制存取build resources
  * 將build artifacts放在S3 bucket
  * 檢視cloudwatch logs for build
  * 建立build project的view，可以用來檢視。
* 相關權限
  * AWSCodeBuildAdminAccess
    * 最高權限
  * AWSCodeBuildDeveloperAccess
  * 不能執行build proejct
  * AWSCodeBuildReadOnlyAccess
    * 投影片就寫read only
  * AmazonS3ReadOnlyAccess
    * 可以看到在S3的output artifacts
  * iam:passrole
    * 若要設定許多 AWS 服務，您必須將 IAM 角色「傳遞」至服務。這樣可讓該服務稍後擔任該角色，並代表您執行動作.

#### Jenkins as a CI Server

* 這邊是說用ec2來建置jenkins，但是也可以用jenkins plugin來結合codebuild與jenkins

#### AWS CodeBuild Jenkins Plugin

* 可以連接codebuild與自己的jenkins build jobs
* 看起來是codeBuild支援jenkins job的格式，可以將job餵進來

#### Automatically Scaling Jenkins CI Server

* 看起來是裝在自己的jenkins master node裡面，會根據需求自動擴展ec2 instance,然後建置好了後再將instance關閉。
* 所以jenkins master node應該是先申請一台ec2,裡面裝好，然後用這台來進行。

### Continuous Delivery and Development With AWS CodeDeploy

* 可以利用codedeploy呼叫cloudformation

#### Deploying with AWS CodeDeploy

* AppSpec Configuration file
  * 說明在部署階段要執行的指令
* 有in-place,rolling,Blue-green部署模式
* 可以roll back與redeploy
* 可以進行local testing 與　debugging

#### Understanding Revision

* 就說明reversion是什麼

#### AWS CodeDeploy Deployment Groups

* 說明Deployment Groups

#### Deployment Configuration

* OneAtAtime
* HalfAtATime
* AllAtOnce
* Custom

#### LifeCycle Events

* CodeDeploy agent在部署時會經過一連串的步驟，這些步驟被稱爲lifecycle events

#### Integrating Hooks and Instance health

#### Managing Access to AWS CodeDeploy

* 使用service role，讓codeDeploy可以存取instance

#### Using triggers to Monitor Deployment

* 例如連接sns通知

### Deploying with AWS Elasic Beanstalk

#### Challenges that AWS Elastic Beanstalk solves

* 不用擔心infrastructure
* 不用expertise or time來管理configure servers,database,load balanceers,firewalls,networks
* 可以自動擴展

#### AWS Elastic Beanstalk Environment

* Web Server Environment
* Worker Environment

#### Customiing via .ebextensions

* 您可以将 AWS Elastic Beanstalk 配置文件 (.ebextensions) 添加到 Web 应用程序的源代码中，从而配置环境并自定义其中包含的 AWS 资源。配置文件是 YAML 或 JSON 格式的文档，采用 .config 文件扩展名，您将其放在名为 .ebextensions 的文件夹中，并在应用程序源包中部署它们。
* 通常會放在 .ebextensions/ 路徑下，例如要客制化cloudwatch設定,就會有一個設定檔放在.ebextensions/cloudwatch.config.

#### Saving Configurations is Recommended

* 將configruations file 存成一個yaml template
* 將目前的狀態透過console存成configurations file
* 可用於
  * restoring an environment
  * applying to a new environment during environment creation
* configuration file存在s3 bucket
* 可透過CLl下載configuration files

#### Envrionment configration precedence

* 讀取參數的優先權
* 環境參數
* saved configurations
* .ebextensions
* default value

#### Deployment Options Suported

* In-place
* Rolling updates (Beanstalk 預設值)
* rolling with additional batch
* Blue/Green
* Immutable

### AWS CodePipeline

#### CodePipeline Key Concepts

* 說明stage跟transition
* 一個stage可以執行多個action
  * action可以平行執行，也可以依照順序執行(p316,p317)
  * action也可以經過manual approval後在繼續執行(p318)

#### AWS CodePipeline Actions

* Source
  * S3,CodeCommit,Github
* Build
  * CodeBuild,Jenkinsm,teamcity
* Test
  * CodeBuild,Jenkins,Ghost Inspector(auto website testing)
* Deploy
  * Cloudformatin,CodeDeploy
* Invoke
  * Lambda
* Approval
  * SNS

#### SAM主題

#### Serverless Application Repository

* AWS Serverless Application Repository 是適用於無伺服器應用程式的代管儲存庫。它可以讓團隊、組織和個別開發人員存放和分享可重複使用的應用程式，並使用強大的新方式，輕鬆組合和部署無伺服器架構

#### Using Resources from Another Account in a Pipeline

* https://docs.aws.amazon.com/zh_tw/codepipeline/latest/userguide/pipelines-create-cross-account.html (還沒看)(review)

#### Creating Cross-Region/Cross-Account Pipeline

* https://docs.aws.amazon.com/zh_tw/codepipeline/latest/userguide/actions-create-cross-region.html (還沒看)(review)

#### Artifact Encryption in Pipeline

* 預設CodePipeline使用SSE與S3 Managed keys來加密artifacts.
* best practices
  * 使用customer managed key取代 default s3 amazon key
  * rotate the key

#### AWS Codepipeline integrated jenkins plugin

* 看起來是裝一個plugin，然後回去poll jenkins，而jenkins是裝在ec2裡面

#### Patterns and Anti-Patterns of Delivery and Deployment

* p335

### AWS CodeStar

#### AWS Codestar Development Workflow

* 增加了建立create project與add user流程，與ideas,request,bugs回饋流程，其它跟CI/CD一樣。
  * 其它流程: commit,build/test,deploy,monitor.
  * p337

#### AWS Codestar project templates

* 支援ec2,beanstalk,serverless等等。
* amazon alexa skills
  * aws echo(aws 語音助手的toolkits)

#### AWS Codestar project teams

* Owner
* Contributor
* Viewer

## Module 7: Automated Testing on AWS

#### Module OverView

* 討論用來做自動化測試的aws tools
* Describe tuning basics
* 說明log概念

### AWS Automated Testing Tools

#### Testing Scenarios in CI/CD Pipeline

* p355在講每個階段可以進行的測試
* Development
  * Unit Test
  * Static Code Analysis
* Build
  * Integration Testing
  * Component Testing
  * Regression Testing
* Stage (是一個跟product相同的測試環境)
  * System testing
  * Performance Testing
  * Load Testing
  * Compliance Testing
  * UAT(User acceptance testing)
    * 交給使用者測試功能是否正常的驗收動作
* Production
  * A/B Testing
  * Canary Analysis(金絲雀分析)

#### Some best practices for unit test

* 條列最佳實踐
* 然後後面投影片談到使用mock

#### Integration Tests

* units/modules之間的測試

  * 例如只有測試order與mso

* 整合測試的方法

  * Big Bang
    * 所有modules合在一起進行測試
  * Top Down
    * 從GUI或最上層的模組進行測試，下層模組是一個一個加進來測試
  * Bottom UP
    * 每個模組都是有上層模組發動測試，然後再慢慢加入更上層的模組

### Performance Tuning

* 良好的性能測試需求
  * 一個跟線上環境很像的驗證環境
  * 數量正確的資料
  * 多使用者
  * scale-out與scale-in的策略

#### cloudwatch 主題

#### Testing Instance Types

* micro benchmarking
  * 我们在开发中，可能会经常面临上面类似的问题，要准确回答这种性质的问题，得到让人信服的结论，不能只靠分析和猜测，正确的方法是针对不同实现策略和算法，在相同的负载或者环境下执行性能测试，比较它们的测试结果，根据性能评分得出结论。 我们把这种性能测试和评估的过程称为Micro benchmark。
  * 投影片說這個有缺點，看起來像是不是在線上環境測試，所以會受到某些影響。
* canary approach
  * netflix使用，就是直接將不同規格的ec2接到elb，然後直接線上測量

#### Elastic Load Balancing Optimization

	* 平衡不同az ec2的負載
	* 可以聯絡aws進行pre-warm
	* 不要讓elb啓用快取，因爲dns會頻繁的解析
 * 實做application-based的health checks
   	* 說可以使用route 53進行健康度檢查
 * 使用route 53 alias record with load balancer
   	* 這個應該是說 route 53的 alias是對到elb，不是對到instance
	* 設定正確的timeout時間
	* 保持keepalive連線，將逾期時間設定大於60秒
	* elb要terminate ssl，這樣在elb後面的機器就不需要使用https互相連線

### Logging with AWS

#### Logging with AWS

* P381 log架構圖，寫的很清楚
  * ec2,cloudwatch log server會有metrics監控資料,會跑到cloudwatch
  * ec2的log與cloudtrail的log，可以丟到cloudwatch log
  * aws config的資料與cloudtrail的log，也可以放到S3

#### Using amazon cloudwatch logs: Terminology

* Log Event
* Log Stream
  * 是一串連續的log event
* Log Group

#### CloudWatch Logs Insights

* 是一個全託管的cloudwatch log分析服務，可以explore,analyze,visualize your logs.

#### CloudTrail主題

## Module 8: Configuration Management with AWS OpsWorks,Chef,and Puppet

#### Module Overview

* 了解configuration management

* 學習aws opswork,chef automate,aws opswork stacks

#### Why  do you need Configuration Management

* 要如何實現下列動作
  * installed application
  * Configuration for application and services(ex: httpd.conf)
  * 大量ec2需要執行上述動作。
* 提到已經在good state，如何避免有人進行有風險的設定，導致系統有問題
  * devopswork可以防止有人修改嗎?

#### Infrastructure Requires ongoing management

* package update
* new software
* new configuration
* new app deployment
* environment specific changes
* 有提到cloudformation在建立時，可以靠着userdata跟cfn-init將東西安裝好，但是後續更新就無法做到，因爲用update stack會建出新的資源

#### How Chef Works

* Chef Workstation
  * 日常工作的機器，上面會安裝chef development kit，可以編寫cookbooks，並管理Chef server 與node.
* Chef Development Kit
* Chef Cookbook
* Chef Node
* Chef Client
  * 裝在每個node中，實際執行任務的工具
* Chef Server
  * 是一個中央倉庫，儲存cookbooks與管理的node訊息。
* Chef Repo
  * Workstation上的一個目錄，用來存儲Cookbooks、Roles、Data bags、Environments等

#### Opswork use case

* Update Configuration
* Define Policies
  * 保證instance符合原本定義的狀態，如果有更改，可以進行回覆
* Bootstrap Resources
  * 利用chef supermarket取得如何正確設定一個resource
* Build CI/CD Pipeline
  * 可以建立類似CICD的Pipeline

#### Backup與Restore

* 可以講chef server 備份到S3,也可以進行回復

### AWS Opsworks stacks

* Stacks
* Layers
* Instances
* App

#### Stacks

* 將一串資源一起管理
  * ec2,ebs,elb
* 同個stack的設定都會相同
* 建議將stack分成dev,stage,prod

#### layers

* 可以將特殊的設定套用在layers上
* Opswork有內建許多標準的layer，例如tomcat,nodejs,mysql........
* 一個instance可以屬於多個layers

#### Layer Lifecycle Events

* Setup
* Configure
* Deploy
* Undeploy
* shutdown

#### Agents Communication and Auto-Healing in instance

* auto healing(自動修復)預設是開啓的，建立layer就會有
* 每個instance都要裝一個opswork agent
* 會跟opswork server 溝通，如果超過5分鐘沒有溝通，opswork server 就會判斷這個instance故障
* 如果instance故障，opswork可以自動回復，會把故障的ec2關閉，然後供裝一個新的，再把原本的ebs掛給這個ec2

#### cookboosk and recipes

* recipes
  * cookbook的做法，看起來應該是流程之類的
* template
  * 會產出檔案，應該類似http.d之類的，搭配recipes將資料設定進去後複製到ec2上。
* attribute
  * 給recipes使用的預設值

#### AWS OpsWork and DevOps Integration

* in-place updates
  * pushed via chef cookbooks
* Blue/Green Deployments
  * 透過AWS CLI啓動一個新環境或clone一個存在的環境
  * aws OpsWorks clone stack

#### Building a Pipeline with AWS CodePipeline and AWS Opswork stacks

* p434有圖，看起來就是將opswork當成deploy階段的工具

#### Puppet on aws

* p437 說明puppet

### Comparing Deployment Tools

#### Comparing Deployment tools(CloudFormation& Opswork)

* p442 是比較CloudFormation與OpsWorks
* AWS OpsWorks
  * 是application management and configuration tools,provision infrastructure
    * [問題]這邊的provision infrastructure不太懂是供裝什麼東西?
  * 可以一次設定大規模的的資源
  * 使用stack與layer來model application
  * 每個layer可以有不同的設定，例如tomcat layer,sql layer.
  * 可以確認所有instance在同個layer都是有相同的state
  * 部署opswork stack使用CFN(cloudformation ?)，然後做update/patch/deploy時使用chef recipes
* AWS CloudFormation
  * Provision resources
  * 啓動完整的infratructure
  * Configure state of your resources(但是opswork是更好的工具)
  * Config update via cfn-init,cfn-hub
  * 不適合用來做大量更新，例如大量ec2的os需要異動

#### Comparing Deployment tools(Beanstalk& Opswork)

* Elastic Beanstalk
  * 可以供裝infrastructure，但是沒有像Cloudformation那麼強大
  * 是個部署三層架構的好工具
  * 適合快速部署(因爲相關服務會一起供裝好)
  * 可以透過.ebextensions進行設定
  * Config files 會跟application code放在一起，適合用在小團隊，另外可以用applicaiton repo來儲存設定，適合用在大團隊。
  * 與git有良好連接
    * opswork目前看到只能接S3
  * 可以連接different branch在不同環境

#### Comparing Deployment tools(CodeDeploy& Opswork)

* p444

* 沒有provision resources

* 在live ec2 instance上更新版本

* 適合用着in-place update

* 適合用在runtime config changes

  * 看起來是再講更改部署組或是appspec的設定。

* push change to a CFN stack or beanstalk environment

* Run bash script to start and stop service,install package,update dns entries

  #### A Side-by-Side Look

  * 說明beanstalk,opswork,codedeploy,cloudformation在deployment,software config,os config,provision resource4個階段是用什麼方式來處理
  * P445 要背下來

## Module 9: AMI Building and AWS Systems Manager

#### Module Overview

* 了解AMI Building 與 AWS Systems Manager概念
  * 了解custom AMIs可以被當做應用程式部署流程的一部分
  * 學習如何使用AWS CodeBuild與CodePipeline將AMI Build作爲CI/CD Pipeline的一部分
  * 學習如何進行patch (這邊應該是指os的patch)
  * 學習AWS System manager
  * Secret management with System Manager Parameter Store
* AMI Design answer
  * https://aws.amazon.com/tw/answers/configuration-management/aws-ami-design/

#### Using Custom APIs as a Base Configuration

* 就是先啓動一個instance,做好相關設定後，在匯出成Custom AMIs，之後就用這個AMIs來進行供裝。

#### AMI Building Strategies

* custom AMI with Complete stack
  * 所有東西都已經安裝好了
* Custom AMI with gold image
  * 只有包含基本的應用程式，其它需要的東西在啓動時才安裝，因此相關動作會寫在user data中
* Custom AMI with skinny(silver) image
  * 只有安裝chef or puppet client,透過configuration tools來設定

#### Which approach to take

* Build Times
* Boot Times
* Shelf life

#### AMI Approach Use Case: Netflix

* Netflix提出使用tiered image架構，總共有4層
  * AWS Linux AMI
  * Foundation AMI
  * Base AMI
  * Application AMI

#### An Architectual approach using gold AMIs

* 這邊是再說ci/cd pipeline，在cloudformation裡面用這個ami進行供裝,可以少設定許多東西。

#### Automate AMI Building with AWS CodePipeline and AWS CodeBuild

* 在說明如何用codepipeline與codebuild來完成 AMI Building 工作

#### AMI Deployment Options

* 這邊應該在說如果AMI patch後，要怎麼更新instances
* Inplace
  * Deploy all at once
  * Rolling update
* replace and retire
  * 建立一個新環境，然後使用新的AMIs並將舊的下架。

#### Issues with software / OS Patching

* OS每年都可能會有弱點被公布，需要進行更新
* 更新通常都要停止服務，因此會有downtime
* 有些應用程式需要固定時間更新(投影片例子舉java)，這時可能會導致應用程式出問題
* 有些公司傾向不進行更新，因爲怕應用程式故障
* 使用AMIs來進行更新，是個優秀的管理技術
* 這個blog有相關介紹(還沒看)(review)
  * https://blog.rackspace.com/patch-and-ami-management-for-windows-on-aws

### AWS Systems Manager

#### AWS Systems Manager

* 可以做到的事 (index: system manager base)
  * Collect software inventoy
  * OS patch
  * create system images
  * configure windows and linux system
  * 可以追蹤system configurations並且維護軟體合規性
  * 可以輕鬆管理aws與地端的instance

#### AWS Systems Manager Features

* Run command
* State Manager
  * 定義與維護OS Configurations,像是防火牆與防毒軟體設定，透過system manager的policy，可以監控大量的instances.
* Inventory
  * 可以查詢configuration,inventory information about instance,還有安裝的軟體等等
* Maintainance window (維護時段)
  * 用來進行維護使用，例如agent更新，更新應用程式等等。
* Patch Manager
  * 對大量instance進行更新
* Automation
  * 將aply patches,update drivers,update agent等工作都可以自動化
* ParameterStore
  * 將configuration data統一控制，並可透過KMS進行加密

#### AWS Systems Manager Parameter Store

* 提供設定檔安全的儲存地方
* 將設定檔參數存成文字或是儲存成加密的物件
* 應用程式中就不用放設定檔
* AWS Systems Manager的功能，例如run command,state manager,automation都可以讀取到parameter sotre的資料，其它服務例如ECS,Lambda也可以讀取
* 使用IAM來設定讀取參數的權限
* 使用KMS來進行加密
* 投影片講到用codedeploy搭配

#### AWS System Manager 主題

* 講了patch manager
* 講了automation

## Module 10: Containers: Docker and Amazon Elastic Container Service

#### Module Overview

* 學習docker 基本概念，以及使用ecs學習如何進行容器管理
  * 了解ecs的task與Service概念
  * 了解ecs scheduling customizations
    * 這個是什麼?
  * 如何使用ecs實踐CI/CD
  * 了解如何使用secret management在容器化的應用程式上
  * 在ecs上實做container application

### Deploying Applications With Docker

* 就講docker基本概念

#### CI/CD Workflow on Docker

* p495 如果有需要再來看

#### What are the Challenges

* 需要將container放在正確的instance上(這個instance的特性要能夠支援container的需求，例如container的cpu要求是高的)
* 哪些instance有足夠的記憶體與ports，可以部署container
* 如何知道container已經故障
* 如何掛載aws資源，例如elb到container上
* 如何延伸CD pipeline，或third parth schedulers.

#### Amazon Elastic Container Service

* Flexible scheduling
* Cluster management
* integrated and extensible
  * 投影片是寫可以透過api extention
* Security
* performance at scale
* task placement

#### AWS Fargate

* 只需要對用到的cpu與memory付錢

#### Networking in AWS Fargate

* fargate會跑在vpc裡面，因此也代表所有的task都跑在vpc裡面，所以網路就是設定vpc.
* elb支援fargate(有ALB與NLB)，但是傳統ELB不支援
* 可以給task公開的ip,fargate會透過nic綁定。

#### Security with AWS Fargate

* Fargate管理infrastructure,用戶管理tasks
* 無法透過ssh連到infrastructure
* cluster 層級的isolation.

### Amazon Elastic Container Service Core Concepts

#### Cluster,Container,and Agent

* Cluster
  * 是region-specific
  * scale by auto scaling
* Container
  * runs elastic continer serivce container agent
  * 只會註冊到一個cluster
  * 用來run tasks
  * 需要額外的網路存取與elastic container service endpoint通訊
* Agent
  * 裝在ec2裡面
  * 用來啓動、停止containers
  * 是open source
* Task Definition
  * 是一個json format
  * 就宣告task的文件

#### Amazon Elastic Container Service Workflow

* 說明如何使用ecs流程
  * step 1: 先使用docker file建好需要的image
  * step 2: 進行task定義與service 定義
  * step3: ECS依照task與service定義進行部署(在ecs container cluster內)

#### Aamzon Elastic Container Service Task Definitions

* Which image to use
* 需要用多少cpu與memory
* 要使用那個port
* data volume
* 環境參數
* IAM Role of your tasks
* 建議每種任務都使用各自的task definition,不要將所有任務寫在同一個task definition

#### Scheduling Amazon ECS Tasks

* 可以分成任務排程、服務排程、協助程式排程
* 投影片說ecs會利用cluster 的狀態來scheduler tasks
  * [問題]這邊的cluster state不知道是什麼?
* service scheduler
  * 保持cluster container個數，並且會跨az供裝，如果不要跨az,就要設定task replacement strategy與task replacement constaints.
* Manually running tasks
  * 可以手動執行，執行完就會關掉
* Custom schedulers
  * 可以依賴第三方排程器
* https://docs.aws.amazon.com/zh_tw/AmazonECS/latest/developerguide/scheduling_tasks.html

#### Amazon ECS Task Placement

*  Task Placement Strategy
  * 選擇instance來放置task或終止task
* Task Placement Constraints
  * 用來限制放置task的地方，例如只能放在某些az,或是某些規格的instance上面

#### How task placement works

* Cluster Contraints
  * 滿足cpu,memory,port
* Custom Constraints
  * location,instance-type.ami,or orther attributes
* Placement Strategies
* Apply Filter
  * 例如過濾instance要符合特定的type.

#### Cluster Query Language(叢集查詢語言)

* 用來與ECS API 互動
* aws文件是寫將container instance進行分組的表達式
* 建立強大的執行參數，可以直接控制應用程度的placement
* 可以用來將container instance進行group

#### Custom Scheduler for Amazon ECS

* 如果使用custom scheduler，其流程如下:
  * step1: 將所有container instance 列出來
  * step2: 輪詢每個instance,得到任務數以及state
  * step3: 找到一個instance，且擁有最少的任務，然後將新的任務放進去

#### Amazon ECS Event Stream

* p515 說明ECS 可以透過cloudwatch監控，或透過cloudwatch event接收事件，並觸發lambda
* lambda可以觸發SNS，或是丟到elasticsearch裡面

#### Amazon Elastic Continer Registry

* 是完全託管的服務，可以與ecs進行聯結
* 可以使用標準的docker tools與docker cli
* 可以與IAM進行聯結

#### CI/CD Pipeline for Containers

* p522說明其流程，要背下來

#### Integrate Amazon ECR With Your CI System

* 就說明連接架構

#### Integrate Amazon ECS with Your CI System

* 依賴service對task數量的定義進行更新，例如有需要4個task,更新時可以停掉兩個，讓service自動抓到新的task.(這個是允許minimum healthy percent 爲50%)
  * 如果是允許maxium healthy percent 爲200%,那ecs會先開啓4個task,再將舊的關掉
* 投影片是P525

#### Best Practice: Testing

* 就說明一些測試的最佳實踐

### Secrets Management

#### Runtime Secrets for Containers

* 在container app中，敏感的資訊包含api keys,password,certificates。
* 這個章節主要是講如何將這些敏感資訊送給container app。

#### Risks Involved in Managing Secrets

* Environment variables
  * 透過inspect就可以看到這些環境參數
* Volumes
  * 從已經存在的container建立image，資訊就可能從volumes泄漏出去
* Building into the container image
  * 資訊可能從build cache或是image泄漏出去(跟第二點有點像)
* p530有一個github issue,在說明這些事情

#### AWS Systems Manager Parameter Store

* 建立kms key來加密資訊，然後將參數存在裡面
* 使用iam role給ecs task,讓task可以讀取參數

* p531　有一個blog網址，有提到更多方法

#### Amazon S3 and AWS IAM Policies

* 說明用s3放db的憑證，會跟vpc,iam.s3加密,s3 read only有關係

#### Moduel 11: DevOps Customer Case Studies

#### Module OverView

* 學習客戶如何使用aws tools完成devops

#### AWS Case Study: Coursera

* 碰到的問題
  * 一個monolithic application，執行多個batch jobs
  * 每個job需要不同的cpu與meory
  * 使用apaceh mesos管理container,但是需要經驗來管理mesos cluster
* Solution
  * 使用ECS,避開底層管理
  * 使用service scheduler,將container配到合適的instance還上面

## Module 12: Course Wrap-UP

#### High Availability Factors

* 要定義跨az的架構
* 要實做HA,scalability,fault tolerance
* Automate diaster  recovery strategies
* 使用正確的服務
* 評估部署的單點故障
  * https://d1.awsstatic.com/whitepapers/architecture/AWS-Reliability-Pillar.pdf

## 要背下的主題

* P29 AWS DevOps相關工具
* p44 跟DevOps相關的工具
* P151 每個工具的安全性
* p163  部署策略
* p311 Continuous Delivery
* p335 Patterns and Anti-Patterns of Delivery and Deployment
* p337 AWS Codestart Development Workflow
* P381 log架構圖，了解log會跑去那邊
* p445 工具的side by side look，要背下來
* CodeDeploy,Beanstalk,Opswork可以執行哪些部署
* 要補lambda的知識
* CodePipeline的跨帳號與跨region的知識(p326/p239)
* 有agent的服務有哪些?
  - Opswork,codedeploy,system manager,ecs
* p465 AWS System manager可以做到的事情要背下來
  -  (index: system manager base)
- p522 說明CI/CD Pipeline for Container流程，要背下來
- P525 說明ecs連接ci server,要了解流程

## 問題

* federated access
  * 怎麼會有access key 與secret key
* 如何使用assume role
* AWS License Manager是否只有支援特定供應商
* DNS cutover
* Scaling group如何兩個合併一個
* (review)可以再回去看一下sysops cloudwatch log的說明，上次沒有看的很清楚
* (review)要回去看codedeploy,投影片p444有些東西不懂
* 映像檔更新技術
  * https://blog.rackspace.com/patch-and-ami-management-for-windows-on-aws
* ECS 參考架構
  * (review)有部署架構等等，要看一次
  * https://aws.amazon.com/tw/ecs/resources/

## 相關服務

* AWS Cloudformation
* AWS Config
* AWS GuardDuty
* AWS Macie
* AWS Cloud9
* AWS CodeStar
* CodeCommit
  * https://www.youtube.com/watch?v=9vYdORRoQdg
* CodeBuild
  * https://www.youtube.com/watch?v=6YQFcd_z4gk
* CodeDeploy
  * https://www.youtube.com/watch?v=K8J6ngMekx4
  * https://www.youtube.com/watch?v=lorT86dVuHM
* CodePipeline
  * https://www.youtube.com/watch?v=NwzJCSPSPZs
* beanstalk
  * https://www.youtube.com/watch?v=ul1tJErDEkE
  * https://www.youtube.com/watch?v=PKjbuxnispM
  * https://www.youtube.com/watch?v=81yhKCIYQYM&t=8s
* AWS SystemManager
  * https://www.youtube.com/watch?v=zUQUpmMgqDQ
  * https://www.youtube.com/watch?v=TLiLHwQ3kao
  * https://www.youtube.com/watch?v=BmpxZsk9N48(o)
* AWS Opswork
  * https://www.youtube.com/watch?v=OBcBOLgEjhs
* AWS SAM
  * https://www.youtube.com/watch?v=Gn0APMEQ2ZU
  * https://github.com/awslabs/serverless-application-model
    * 裡面有文件說明
* AWS ELB
  * https://www.youtube.com/watch?v=4gnMyhyVIg4
* AWS 開發人員工具
  * https://aws.amazon.com/tw/products/developer-tools/
* 在AWS上通过Jenkins实现持续集成和持续交付
  * https://s3.cn-north-1.amazonaws.com.cn/aws-summit-2017-beijing/5_%E5%9C%A8AWS%E4%B8%8A%E9%80%9A%E8%BF%87Jenkins%E5%AE%9E%E7%8E%B0%E6%8C%81%E7%BB%AD%E9%9B%86%E6%88%90%E5%92%8C%E6%8C%81%E7%BB%AD%E4%BA%A4%E4%BB%98.pdf
* 部署策略
  * https://www.slideshare.net/AmazonWebServices/use-elastic-beanstalk-bluegreen-deployment-to-reduce-downtime-risk-dev330r1-aws-reinvent-2018
    * (review)裡面有各項部署的優缺點，要回頭看
  * AWS Blue/Green說明
    * https://medium.com/@acharya.naveen/blue-green-deployment-with-aws-application-load-balancer-e551cd00d2c9
  * Disposable development and QA environments with AWS ALB Host-based Routing
    * https://medium.com/strigo-engineering/disposable-development-and-qa-environments-with-aws-alb-host-based-routing-7381668989e0
  * Simplify your Blue/Green deployment with AWS Application Load Balancer
    * https://medium.com/@acharya.naveen/blue-green-deployment-with-aws-application-load-balancer-e551cd00d2c9
* AWS Answers
  * https://aws.amazon.com/tw/answers/


