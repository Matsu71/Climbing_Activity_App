# Product Specification — Climbing Activity App

## 1. Product goal

クライマーが日々の登攀を短時間で記録でき、その記録がモンスター／キャラクターの成長として返ってくるアプリを作る。

主目的は詳細なトレーニング管理ではなく、次の3点を同時に満たすこと。

- 記録を続けやすい
- 自分のクライミング傾向が見える
- 記録したくなるゲーム的フィードバックがある

## 2. Product principles

### 2.1 入力負担を最小化する

課題ごとの入力項目を増やしすぎない。詳細情報は原則任意にする。

目標：慣れたユーザーなら1課題5〜10秒程度で記録可能。

### 2.2 クライミングの上手さだけを競わせない

最高グレードだけでゲーム進行・ランキングを決めない。

初心者でも、継続、成長、自己ベスト、完登、課題タイプの幅などでゲームを楽しめる設計にする。

### 2.3 休養を失敗扱いしない

休養日はキャラクター回復やトレーニング適応の日として扱う。

### 2.4 自己申告データは厳密性より手軽さを優先

課題のPhysical / Balance / Technical等は科学的な絶対評価ではなく、ユーザー自身の主観的記録として扱う。

---

## 3. Main navigation

スマートフォン下部タブを基本とする。

1. **Today** — 今日のキャラクター、回復状態、直近の活動
2. **Log** — セッション開始・課題登録
3. **Growth** — キャラクター能力、成長履歴
4. **History** — クライミング履歴・分析
5. **Profile** — 設定、グレード表記等

MVPではToday / Log / Growth / Historyの4タブでもよい。

---

## 4. Session flow

### 4.1 セッション開始

最小入力：

- 日付：自動
- 種目：Boulder / Lead

任意：

- ジム / 岩場
- セッションメモ

同一セッション内では種目・場所を引き継ぎ、課題ごとに毎回入力しない。

### 4.2 課題追加

#### 必須または初期表示する項目

1. **Grade**
2. **Result**
   - Send
   - Not sent / Project
3. **Attempts**
4. **First try / Flash系フラグ**
5. **Inclination**
6. **Physical / Balance / Technical**

#### 任意・折りたたみ

- メモ
- 写真
- 課題名 / 番号
- ホールド色
- 壁名

### 4.3 Grade入力

ユーザー設定により表示体系を切り替えられるようにする。

例：

- ボルダー：V-grade / Fontainebleau / 国内ジム独自表記への対応余地
- リード：French / YDS等への対応余地

初期版では利用地域に合わせて対象を絞ってよい。

---

## 5. Quick input UI

### 5.1 Attempts

`−  3  ＋` のようなステッパーを基本とし、連続タップしやすくする。

1トライ目で完登した場合はFirst tryを自動候補にする。

### 5.2 Inclination

5段階程度の大きな選択ボタンまたは横スライダー。

- Slab
- Vertical
- Slight Overhang
- Overhang
- Steep / Roof

選択時に壁の簡単なシルエットを変えると直感的。

### 5.3 Physical / Balance / Technical

3本のバーを縦積みまたは横並びで表示。

スマホ操作では細い通常スライダーより、**5つの区切りを直接タップできるSegmented Bar**を推奨。

例：

Physical  ■■■■□
Balance   ■■□□□
Technical ■■■□□

各項目0〜5または1〜5。

初期値は中間値ではなく「未設定」にし、任意入力としてもよい。3項目すべてを必須にするとログ登録が重くなる可能性があるため、利用率を見て調整する。

---

## 6. Game / growth system

### 6.1 Core stats

キャラクター内部能力の例：

- Power
- Balance
- Technique
- Endurance
- Recovery
- Persistence

ただし画面上に最初から6項目をすべて出す必要はない。

### 6.2 Growth inputs

成長量は以下を材料にする。

- グレード
- ユーザー本人に対する相対難度
- 完登 / 未完登
- トライ数
- First try / Flash
- Boulder / Lead
- Inclination
- Physical / Balance / Technical
- セッション頻度
- 適切な休養

### 6.3 Relative difficulty

絶対グレードだけで経験値を決めない。

例：

`Relative Difficulty = 課題グレード − 最近のユーザー基準グレード`

これにより、初心者の自己ベスト更新も上級者の自己ベスト更新も同様に価値を持たせられる。

### 6.4 Example growth mapping

- Physicalが高い課題 → Power XP
- Balanceが高い課題 → Balance XP
- Technicalが高い課題 → Technique XP
- Lead → Endurance XPを追加
- Steep / Roof → Power XP補正
- 低トライ数完登 → Efficiency / Technique系のボーナス候補
- 多トライ後の完登 → Persistenceボーナス

### 6.5 Flash / first try

First tryは明確なゲーム的報酬を与えやすい。

ただしLeadのOn-sightとFlash、BoulderのFlash等は競技上の意味が異なるため、将来厳密に扱う場合は種目別に名称・条件を整理する。

MVPではUIを複雑にしないため「First try」中心の簡易表現でもよい。

---

## 7. Rest day system

### 7.1 Automatic rest

ユーザーがその日にクライミングセッションを記録しなかった場合、原則として自動Rest Day候補とする。

毎日の手動入力は要求しない。

### 7.2 Recovery

Rest Dayでは以下を行う。

- Fatigue低下
- Recovery上昇
- 前回セッションで獲得した一部成長値の定着演出
- キャラクターの休息アニメーション

「何もしなかった日」ではなく「回復して強くなった日」として見せる。

### 7.3 Other activities

将来オプションとして追加可能：

- Strength training
- Running
- Mobility / Stretching
- Hangboard
- Other

ただしMVPでは非表示またはToday画面の`+ Other activity`からのみ入力できる任意機能とする。

入力しなくても不利にならない。

---

## 8. Character concept

### 8.1 Growth reflects climbing style

同じ初期キャラクターでもログによって能力・見た目・進化先が変わる設計を候補とする。

例：

- Physical主体 → Power型
- Balance主体 → Balance型
- Technical主体 → Technique型
- Lead主体 → Endurance型
- バランス良く成長 → All-round型

### 8.2 Evolution

進化条件候補：

- 総経験値
- 特定能力値
- 初めて特定難度を完登
- 一定数のセッション
- 複数タイプの課題を一定数完登

単純な連続ログイン日数だけでは進化させない。

---

## 9. History / analysis

最低限表示するもの：

- セッション数
- 完登数
- トライ数
- Grade分布
- Boulder / Lead比率
- Flash / First try数
- Physical / Balance / Technical分布
- Inclination分布
- 自己ベスト推移

長期的には「自分はTechnical課題の成功率が高い」「強傾斜ではトライ数が増える」等の分析に拡張できる。

---

## 10. Ranking policy

最高グレードのみの単一ランキングは採用しない。

候補：

- Weekly Growth
- Personal Best Improvement
- Sends this week
- First-try sends
- Session consistency
- Challenge score

初心者と上級者が完全に同条件で直接競争するランキングは限定的にする。

自己申告ベースであることを前提に、ゲーム進行の主要報酬をランキング依存にしない。

---

## 11. Data model draft

### User

- id
- displayName
- preferredBoulderGradeSystem
- preferredLeadGradeSystem
- createdAt

### ClimbingSession

- id
- userId
- date
- discipline: boulder | lead
- locationId? / locationName?
- memo?
- startedAt?
- endedAt?

### ClimbLog

- id
- sessionId
- grade
- gradeSystem
- sent: boolean
- attempts: number
- firstTry: boolean
- inclination: slab | vertical | slight_overhang | overhang | steep
- physical?: 0..5
- balance?: 0..5
- technical?: 0..5
- routeName?
- memo?
- createdAt

### CharacterState

- userId
- characterId
- level
- xp
- power
- balance
- technique
- endurance
- recovery
- persistence
- fatigue
- evolutionState

### DailyState

- userId
- date
- activityType: climbing | rest | other
- recoveryDelta
- growthApplied

---

## 12. MVP acceptance criteria

MVPとして最低限、次を成立させる。

- スマホで課題を素早く記録できる
- Boulder / Leadを記録できる
- Grade / Send / Attempts / First tryを記録できる
- Inclinationを記録できる
- Physical / Balance / Technicalを直感的に入力できる
- 登録直後にキャラクターへ成長フィードバックが返る
- 履歴を確認できる
- 非活動日は自動的に休養として扱える
- 休養による回復がゲーム上プラスになる
- 他アクティビティ入力を強制しない

---

## 13. Avoid in initial release

初期版では以下を避ける。

- 入力項目を大量に必須化する
- 毎日の休養入力を要求する
- 詳細なトレーニングメニュー管理
- 複雑なSNS
- リアルタイム対戦
- 最高グレードだけで決まるランキング
- 他スポーツの詳細ログ
- 医療的な怪我診断やトレーニング処方

---

## 14. Next implementation priority

1. モバイル縦画面のLog画面プロトタイプ
2. Physical / Balance / TechnicalのSegmented Bar操作
3. セッション→複数課題登録の高速フロー
4. 仮キャラクター1体と簡易XPロジック
5. Today画面で成長／休養を見せる
6. History画面
7. 実際に数セッション記録して入力負荷を検証

最初に検証すべきなのはゲームの規模ではなく、**実際のクライミング中・直後でも面倒に感じず記録できるか**です。
