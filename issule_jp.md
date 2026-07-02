# Auto-reloadが初回のみ成功し、2回目以降検知されないことがある（3.5.0以降に発生したregression）

## Summary

3.5.0以降で、ホットリロード（`./gradlew -t build`）が、サーバ起動後の最初のソースコード変更&保存では正常に動作しますが、2回目以降の変更では正常に動作しないことがある。

## Expected Behavior

3.4.1以前と同様に、ホットリロードが正常に動作する。

## Description

Summaryのとおり。

ログを添付する。

<details>
<summary>log</summary>

TODO: ここにはる

</details>

2回目であっても、

- 保存そのものには反応してログが流れている。
- BUILD SUCCESSFUL自体は表示されている
- 問題のある二度目の変更&保存時、「Waiting for changes to input files...」以降に流れるべき「」が流れない。Ktorはアクセス時に更新するという認識。

なお、サーバを再起動すると、同じ問題が発生する。

## Steps to Reproduce

1. [start.ktor.io](https://start.ktor.io/)でシンプルなプロジェクトを取得
   - Build system: Gradle
   - Engine: Netty
   - Configuration: HOCON File
2. [公式のAuto-reload](https://ktor.io/docs/server-auto-reload.html)どおりの設定・編集を行う
3. 紹介されている`./gradlew -t build`でサーバを立ち上げる
4. 適当にコードを変更&保存

各種バージョンでの検証を行うための[シンプルなリポジトリ](https://github.com/unSerori/ktor-relaod-bug)を公開しています

## Investigation Note

最初に「Kotlin: 2.4.0, Ktor: 3.5.0」プロジェクトを立ち上げる過程でうまく動作しないことに気づいた。
調査した結果、この[「Kotlin: 2.1.10, Ktor: 3.2.2」なサンプル](https://github.com/Tomoki108/ktor-sample)を見つけたため、過去のバージョンで動作していることは確認できた。

次に、KotlinとKtorどちらが原因かを調査するため、「Kotlin: 2.1.10, Ktor: 3.5.0」と「Kotlin: 2.4.0, Ktor: 3.2.2」で確認した。
前者はそもそもkotlinバージョンに対してktorのバージョンが高いようでビルドが通らない、後者は動作した。
そのため、Kotlinのバージョン2.4.0が問題なのではなく、Ktor3.5.0付近が問題でありそうだとした。

最後に、Ktorの3.2.2~3.5.0バージョンを二分探査で調査した。
結果は以下

| Kotlin Version | Ktor Version                             | 結果                                                                                                                          |
| -------------- | ---------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------- |
| 2.1.10         | 3.2.2                                    | 正常に動作した                                                                                                                |
| 2.1.10         | 3.5.1                                    | そもそもkotlinバージョンに対してktorのバージョンが高いようでビルドが通らない（Kotlin Metadataの非互換であり、今回は関係ない） |
| 2.4.0          | 3.2.2                                    | 正常に動作した->Kotlin 2.4.0は問題ではなさそう                                                                                |
| 2.4.0          | 3.3.3, 3.4.0, 3.4.1, 3.4.2, 3.4.3, 3.4.1 | 正常に動作した                                                                                                                |
| 2.4.0          | 3.5.0                                    | 正常に動作しなかった                                                                                                          |
| 2.4.0          | 3.5.1                                    | 正常に動作しなかった                                                                                                          |

3.4.1までは正常動作、3.5.0から動作しなくなっている。
念の為、3.5.1でも試したが、同様の問題が確認された。

## Suspected Cause

検証で想像できる原因は以下

1. 3.5.0のなんらかの変更の副作用で、元々不安定なauto-reloadが死んだ？->Auto-reloadはたびたび不具合が発生している（[例えば](https://youtrack.jetbrains.com/projects/KTOR/issues/KTOR-8821/Autoreloading-module-function-refs-not-working-since-3.2.0)）
2. kotlincが吐き出す.classファイルの中身が不正で、前回の成功状態を返している？ -> ホットリロード時に.classファイルのタイムスタンプおよび中身が更新されているため違いそう、そもそも「BUILD SUCCESSFUL」は表示されている
3. 2の検証のために、タイムスタンプや中身の確認を行ったが、その確認プロセスを行うと正常にホットリロードが動作した->レースコンディションの問題か？[これ](https://github.com/ktorio/ktor/issues/4717)に似ている。あるいは、確認によってDocker特有のファイルキャッシュの不整合が解消されるとか？
4. サーバへのリクエストが反映処理の起動を行えていない、トリガーが動作していない？->3.5.0で修正が入った[call event loop・worker event loopのPR](https://youtrack.jetbrains.com/projects/KTOR/issues/KTOR-9542/Netty-The-request-handler-runs-on-worker-event-loop-instead-of-call-event-loop-since-3.4.3)の副作用などの可能性はないだろうかとかが関係してないだろうか。

## Environment

OS: MacOS
VSCode: 1.125.0
Docker Client: 27.4.0
Docker Server（Engine）: 27.4.0
Java: 21
Kotlin: 2.4.0
Ktor: 3.5.0

## Additional Context

Apologies for any unclear parts due to machine translation.

Please let me know if you have any other questions or need any additional information.
I'll get back to you promptly.

Also, I can submit pull requests within my capabilities.
Considering the guidelines, what kind of changes should I commit?

I'm looking forward to the future development of this project. Thank you.
