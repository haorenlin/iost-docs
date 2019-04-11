---
Id: SystemContract
Title: システムコントラクト
Sidebar_label: System Contract
---

## vote_producer.iost
---

### 説明
スーパーノードは投票にむけて、キャンペーンを行います。

### 情報
| コントラクトID | vote_producer.iost |
| :----: | :------ |
| 言語 | JavaScript |
| バージョン | 1.0.0 |

### API

#### applyRegister
スーパーノードの候補になるために登録を申請します。

| パラメータリスト | パラメータの型 |
| :----: | :------ |
| アカウント名 | string |
| Base5８エンコードされた公開鍵 | string |
| 所在地 | string |
| WebサイトのURL | string |
| ネットワークID | string |
| プロデューサーかどうか | bool |

#### applyUnregister
登録解除を申し込みます。

| パラメータリスト | パラメータの型 |
| :----: | :------ |
| アカウント名 | string |


#### unregister
登録を解除するには、まずapplyUnregisterを呼び出す必要があります。監査にパスしたら、このインタフェースを呼び出すことができます。

| パラメータリスト | パラメータの型 |
| :----: | :------ |
| アカウント名 | string |

#### updateProducer
登録情報を更新します。

| パラメータリスト | パラメータの型 |
| :----: | :------ |
| アカウント名 | string |
| Base5８エンコードされた公開鍵 | string |
| 所在地 | string |
| WebサイトのURL | string |
| ネットワークID | string |

#### logInProducer
オンラインにして、ノードが現在サービスを受けることができることを示します。

| パラメータリスト | パラメータの型 |
| :----: | :------ |
| アカウント名| string |

#### logOutProducer
オフラインは、現在ノードがサービスを提供できないことを意味します。

| パラメータリスト | パラメータの型 |
| :----: | :------ |
| アカウント名| string |

#### vote
投票します。

| パラメータリスト | パラメータの型 |
| :----: | :------ |
| 投票者 アカウント名| string |
| 候補者 アカウント名| string |
| 投票数 | string |

#### unvote
投票をキャンセルします。

| パラメータリスト | パラメータの型 |
| :----: | :------ |
| 投票者 アカウント名| string |
| 候補者 アカウント名| string |
| 投票数 | string |

#### voterWithdraw
投票者がボーナス報酬を受け取ります。

| パラメータリスト | パラメータの型 |
| :----: | :------ |
| 投票者 アカウント名| string |

#### candidateWithdraw
競技者がボーナス報酬を受け取ります。

| パラメータリスト | パラメータの型 |
| :----: | :------ |
| 候補者 アカウント名| string |

## vote.iost
---

### 説明
投票の作成、投票の収集、投票の集計に使われる普遍的な投票規約です。この規約に基づいて投票機能を実装できます。

### 情報
| コントラクトID | vote.iost |
| :----: | :------ |
| 言語 | JavaScript |
| バージョン | 1.0.0 |

### API

#### newVote
投票を作成します。

| パラメータリスト | パラメータの型 | 備考 |
| :----: | :------ | :------ |
| 投票作成者 アカウント名| string | 投票の作成には、1000IOSTのデポジットが必要です。これは作成者アカウントから差し引かれます。作成者アカウントには、投票するための管理者権限があります。 |
| 投票の説明 | string ||
| 投票設定 | JSONオブジェクト| 5つのキーがあります。 <br>resultNumber —— number型。投票結果の数で最大2000、<br> minVote —— number型で、投票結果を入れる候補者の最小投票数 <br>options - 文字列の配列型。候補者のセット。初期値は空([])も可、<br>anyOption - bool型。候補者以外の候補者を許可するかどうかで、falseにするとユーザーは候補者コレクション内の候補者のみに投票できることを意味します。
 whether to allow The candidate in the non-options collection, passing false means that the user can only cast candidates in the options collection; <br>freezeTime - number型。トークンの凍結時間を解除します。(秒単位)
 　呼び出しが成功すると、一意の投票IDが返ります。

#### addOption
投票候補者を追加します。

| パラメータリスト | パラメータの型 | 備考 |
| :----: | :------ | :------ |
| 投票ID| string | newVoteインターフェースで返ってきたID|
| 候補者 | string ||
| 前の投票をクリアするかどうか | bool ||

#### removeOption
投票候補者を削除しますが、投票の結果は保持して削除し、addOptionの候補者で投票数を元に戻すかどうかを選択します。

| パラメータリスト | パラメータの型 | 備考 |
| :----: | :------ | :------ |
| 投票ID| string | newVoteインターフェースで返ってきたID|
| 候補者 | string ||
強制削除かどうか | bool | falseなら候補者が結果セット内にあるときには削除しない、trueなら結果セットを強制的に削除および更新する |

#### getOption
候補者に投票します。

| パラメータリスト | パラメータの型 | 備考 |
| :----: | :------ | :------ |
| 投票ID| string | newVoteインターフェースで返ってきたID|
| 候補者 | string ||

結果はJSONオブジェクトです。

| キー | 型 | メモ |
| :----: | :------ | :------ |
| votes| string | 投票 |
| deleted| bool | 削除済みか |
| clearTime| number | 投票数が最後にクリアされたブロック番号 |

#### vote
投票します。

| パラメータリスト | パラメータの型 | 備考 |
| :----: | :------ |:------ |
| 投票ID| string | newVoteインターフェースで返ってきたID|
| 投票者 アカウント名| string ||
| 候補者 | string ||
| 投票数 | string ||

#### unvote
投票をキャンセルします。

| パラメータリスト | パラメータの型 | 備考 |
| :----: | :------ |:------ |
| 投票ID| string | newVoteインターフェースで返ってきたID|
| 投票者 アカウント名| string ||
| 候補者 | string ||
| 投票数 | string ||

#### getVote
アカウントの投票記録を取得します。

| パラメータリスト | パラメータの型 | 備考 |
| :----: | :------ |:------ |
| 投票ID| string | newVoteインターフェースで返ってきたID|
| 投票者 アカウント名| string ||

結果はJSON配列になり、それぞれ次のオブジェクトになります。

| キー | 型 | メモ |
| :----: | :------ | :------ |
| option| string | 候補者 |
| votes| string | 投票数 |
| voteTime| number | 最終投票ブロック番号 |
| clearedVotes| string | クリアされた投票数 |

#### getResult
投票結果を取得し、候補者と投票数の配列を返します。

| パラメータリスト | パラメータの型 | 備考 |
| :----: | :------ |:------ |
| 投票ID| string | newVoteインターフェースで返ってきたID|

結果はJSON配列になり、それぞれ次のオブジェクトになります。

| キー | 型 | メモ |
| :----: | :------ | :------ |
| option| string | 候補者 |
| votes| string | 投票数 |

#### delVote
投票を削除し、投票中に作成されたIOSTを作成者アカウントに返します。

| パラメータリスト | パラメータの型 | 備考 |
| :----: | :------ | :------ |
| 投票ID| string | newVoteインターフェースで返ってきたID|

## auth.iost
---

### 説明
アカウントシステムと権利管理

### 情報
| コントラクトID | auth.iost |
| :----: | :------ |
| 言語 | JavaScript |
| バージョン | 1.0.0 |

### API

#### signUp
アカウントを作成します。

| パラメータリスト | パラメータの型 |
| :----: | :------ |
| Username | string |
| ownerKey | string |
| activeKey | string |

#### addPermission
アカウントに権限を追加します。

| パラメータリスト | パラメータの型 |
| :----: | :------ |
| ユーザ名 | string |
| 権限名 | string |
| 権限のしきい値 | number |

#### dropPermission
アカウントの権限を削除します。

| パラメータリスト | パラメータの型 |
| :----: | :------ |
| ユーザ名 | string |
| 権限名 | string |

#### assignPermission
項目に権限を指定します。

| パラメータリスト | パラメータの型 |
| :----: | :------ |
| ユーザ名 | string |
| 権限名 | string |
| 項目 | string |
| 重み | number |


#### revokePermission
権限を剥奪します。

| パラメータリスト | パラメータの型 |
| :----: | :------ |
| ユーザ名 | string |
| 権限名 | string |
| 項目 | string |

#### addGroup
権限グループを追加します。

| パラメータリスト | パラメータの型 |
| :----: | :------ |
| ユーザ名 | string |
| グループ名 | string |

#### dropGroup
権限グループを削除します。

| パラメータリスト | パラメータの型 |
| :----: | :------ |
| ユーザ名 | string |
| グループ名 | string |

#### assignGroup
項目に権限グループを指定します。

| パラメータリスト | パラメータの型 |
| :----: | :------ |
| ユーザ名 | string |
| グループ名 | string |
| 項目 | string |
| 重み | number |

#### revokeGroup
権限グループから項目を削除します。

| パラメータリスト | パラメータの型 |
| :----: | :------ |
| ユーザ名 | string |
| グループ名 | string |
| 項目 | string |


#### assignPermissionToGroup
グループに権限を追加します。

| パラメータリスト | パラメータの型 |
| :----: | :------ |
| ユーザ名 | string |
| 権限名 | string |
| グループ名 | string |


#### revokePermissionInGroup
グループの権限を削除します。

| パラメータリスト | パラメータの型 |
| :----: | :------ |
| ユーザ名 | string |
| 権限名 | string |
| グループ名 | string |


## bonus.iost
---

### 説明

公式な**ノード作成報酬**管理

### 情報

| コントラクトID | bonus.iost |
| :----: | :------ |
| 言語 | JavaScript |
| バージョン | 1.0.0 |

### API

#### issueContribute

貢献値を計算します。これはシステムが自動的に呼び出します。

| パラメータリスト | パラメータの型 |
| :----: | :------ |
| data | JSON |

#### exchangeIOST

貢献値に応じて、IOSTと交換します。

| パラメータリスト | パラメータの型 |
| :----: | :------ |
| アカウント名| string |
| 量 | string |


## system.iost

---

### 説明
発行と更新、基本的な関数のための、基本システムコントラクト

### 情報
| コントラクトID | system.iost |
| :----: | :------ |
| 言語 | ネイティブ |
| バージョン | 1.0.0 |

### API

#### setCode (code)
スマートコントラクトをデプロイする。

| パラメータ名 | パラメータの説明 | パラメータの型 |
| :----: | :----: | :------ |
| code | スマートコントラクトのコード | string |

| 戻り値 | 戻り値の型 |
| :----: | :------ |
| contractID | string |

スマートコントラクトのコードには、言語やインタフェースの定義などのコードとスマートコントラクトの情報が含まれます。コードのパラメータは、JSON形式とprotobufシリアライゼーションエンコーディング形式の2つの形式をサポートします。開発者がコントラクトをデプロイするために、普通はこのインターフェースを直接呼び出す必要はありません。iwalletまたは関連する言語のSDKを使用することをお勧めします。

スマートコントラクトをデプロイすると、システムは自動的にスマートコントラクトのinit()関数を呼び出します。開発者はinit関数で初期化を行うことができます。

戻り値のcontractIDは、グローバルに固有なスマートコントラクトIDで、コントラクトをデプロするトランザクションのハッシュから生成されます。contractIDは "Contract"で始まり、大文字と小文字、および数字で構成されています。1つのトランザクションにデプロイできるスマートコントラクトは1つだけです。

#### updateCode (code, data)
スマートコントラクトをアップグレードします。

| パラメータ名 | パラメータの説明 | パラメータの型 |
| :----: | :----: | :------ |
| code | スマートコントラクトのコード | string |
| data | アップグレード関数のパラメータ | string |

| 戻り値 | なし |
| :----: | :------ |

スマートコントラクトをアップグレードします。codeはスマートコントラクトのコードです。形式はsetCodeのパラメータと同じです。

スマートコントラクトをアップグレードする場合、システムは自動的にアップグレード権限をコントラクトのcan_update(data)関数でチェックします。パラメータdataは、updateCode内の2番目のパラメータで、can_update関数が存在していて、呼び出しがtrueの場合のみ使われます。結果はコントラクトのアップグレードが成功するか、アップグレード権限がないと判断されアップグレードが失敗するかどちからになります。

#### cancelDelaytx (txHash)
遅延トランザクションを取り消します。遅延トランザクションを実行する前にこの関数を呼び出して、遅延トランザクションを取り消してください。

| パラメータ名 | パラメータの説明 | パラメータの型 |
| :----: | :----: | :------ |
| txHash | トランザクションハッシュ | string |

| 戻り値 | なし |
| :----: | :------ |

#### requireAuth (acc, permission)
トランザクションがアカウントの権限があるかどうかをチェックします。

| パラメータ名 | パラメータの説明 | パラメータの型 |
| :----: | :----: | :------ |
| acc | アカウント名| string |
| permission | 権限名 | string |

| 戻り値 | Type |
| :----: | :------ |
| ok | bool |

#### receipt (data)
トランザクションのレシートを生成します。レシートはブロックに格納されますので、トランザクションハッシュを通して照会することができます。

| パラメータ名 | パラメータの説明 | パラメータの型 |
| :----: | :----: | :------ |
| data | レシートの内容 | string |

| 戻り値 | なし |
| :----: | :------ |