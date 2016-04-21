# Broadcast

> Broadcast is a strategy where messages are sent to all instances of the actor (that) the router controls.

ブロードキャストはルーターの支配する全てのアクターインスタンスにメッセージが送られる戦略です。

> It's good for distributing work to multiple nodes that may have different tasks to perform the same work, in case any failures occur.

それは、ある一つの(同じ)動作を実現させるために異なるタスクを持つかもしれない複数のノードへ、仕事を分散させるのにはよい先約です、まあたまには障害が起きるけど。


> Since [all routees under the router] will recieve the message, their mailboxes should theoretically be equally full/empty.

あるrouterの下につく全てのrouteeがメッセージを受け取るまで、理論的には(そのrouteeたちの)mailboxは等しくいっぱいか空になっているべきである。

> The reality is that how you apply the dispatcher for fairness in message handling (by tuning the "throughput" configuration value) will determine this.

現実は、いかにしてメッセージハンドリングにおける公正さのもと分配を適用させるか(どのようにスループットの値をチューニングするか)、という方法の難しさが、これ(この理論が成り立つかどうか)を決定する。

-- ここまで --

> Try not to think of routers where the work is distributed evenly but could still occur in each routee at varying times.

作業が均等に広がり分散されるルーターについて考えないようにしてみましょう、しかし、まだそれぞれのルートで様々な時間に発生する可能性がある。(何が発生するのか？)

> See Figure 1-5 for an example.

図1-5の例を見て下さい。

# ScatterGatherFirstCompletedOf

> This is a strategy where messages are sent to all instances of the actor the router controls, but only the first response from any of them is handled.

これ(ScatterGatherFirstCompletedOf)はメッセージが全てのアクターインスタンスのルータコントロールに送られる戦略ですが、それらの中で最初にレスポンスを返したルータに扱われます。

> This is good for situations where you need a response quickly and want to ask multiple handlers to try to do it for you.

これ(ScatterGatherFirstCompletedOf)は、素早いレスポンスを必要とする場面や、あなたのためにそれ(?)をやってみる複数のハンドラに依頼したい状況で有効です。

> In this way, you don't have to worry about which routee has the least amount of work to do, or even if it has the fewest tasks queued, since those tasks won't take longer than another routee that already has more messages to handle.

この方法では、ルートはやるべき作業を最小限持っていて、もしくは、たとえキューに入った最小のタスクを持っていても、それらのタスクは他のルート(既に扱うためのより多くのメッセージを持ってる)より長くかからない、ということを心配しなくていい。

> This is particularly useful if the routees are spread among multiple JVMs or physical boxes.

もしルートが複数のJVMや物理ボックスに広がるならこれは特に役に立つ。

Each of those boxes might be utilized at varying rates, and you want the work to be performed as quickly as possible without trying to manually figure out which box is currently doing the least work.

これらのボックスのそれぞれが様々なレートで使えるかもしれない、そしてあなたはボックスが現在少なくとも作業をしていることを手動で見つけ出すことなく出来る限り速く作業を実施したい。

> Worse, even if you did check to see if a box was the least busy, by the time you figured out which box it was and sent the work, it could be loaded down chewing through other work.

悪いことに、あなたはボックスが最も忙しかったことを見て確認したとしても、その時にはあなたはそれがその作業を箱に送ったことを理解する、それは他の作業を通して咀嚼してダウンロードできる。

> In Figue 1-6, I'm sending the work across five routees.

図1−6では、私は5つのルートを横切って作業を送っている。

> I only care about whichever of the five completes the work first and responds.

私は5つのうち最初に作業を完了させ応答したことについてだけケアする。

> This trades some potential network latency (if the boxes are more than one physically close hop away) and extra CPU utilization (as each of the routees has to do the work) for getting the response the fastest.

このトレードはいくつかの潜在的なネットワークレイテンシがある(もしボックスがより多く1つの物理的に閉じて離れたら)そして、利用最も速くレスポンスを取得するために余分なCPUを利用する。(それぞれのルートが作業をしなければならない)











