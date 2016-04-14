# Broadcast

> Broadcast is a strategy where messages are sent to all instances of the actor the router controls.

ブロードキャストはメッセージが全てのアクターインスタンスのルータコントロールに送られる。

> It's good for distributing work to multiple nodes that may have different tasks to perform the same work, in case any failures occur.

それは複数のノードの分散作業にいいことです。同じ作業を行うために異なるタスクを持つかもしれない。場合によっては何か障害を起こす。

> Since all routees under the router will recive the message, their mailboxes should theoretically be equally full/empty.

ルーターの下の全てのルートはメッセージを受け取るので、それらのメールボックスは理論的には一杯か空になってるべきである。

> The reality is that how you apply the dispatcher for fairness in message handling (by tuning the "throughput" configuration value) will determine this.

現実は、あなたがどのようにメッセージハンドリングで公正にディスパッチャーを適用するか(スループットの設定値の調整によって)が、それ(一個前の文)を決定する。

> Try not to think of routers where the work is distributed evenly spread but could still occur in each routee at varying times.

作業が均等に広がり分散されるルーターについて考えないようにしてみましょう、しかし、まだそれぞれのルートで様々な時間に発生する可能性がある。(何が発生するのか？)

> See Figure 1-5 for an example.

図1-5の例を見て下さい。

# 
