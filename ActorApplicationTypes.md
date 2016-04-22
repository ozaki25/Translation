# Broadcast

> Broadcast is a strategy where messages are sent to all instances of the actor (that) the router controls.

ブロードキャストはルーターの支配する全てのアクターインスタンスにメッセージが送られる戦略です。

> It's good for distributing work to multiple nodes that may have different tasks to perform the same work, in case any failures occur.

それは、ある一つの(同じ)動作を実現させるために異なるタスクを持つかもしれない複数のノードへ、仕事を分散させるのにはよい戦略です、まあたまには障害が起きるけど。


> Since [all routees under the router] will recieve the message, their mailboxes should theoretically be equally full/empty.

あるrouterの下につく全てのrouteeがメッセージを受け取るまで、理論的には(そのrouteeたちの)mailboxは等しくいっぱいか空になっているべきである。

> The reality is that how you apply the dispatcher for fairness in message handling (by tuning the "throughput" configuration value) will determine this.

現実は、いかにしてメッセージハンドリングにおける公正さのもと分配を適用させるか(どのようにスループットの値をチューニングするか)、という方法の難しさが、これ(この理論が成り立つかどうか)を決定する。

> Try not to think of routers where the work is distributed evenly but could still occur in each routee at varying times.

作業が均等に広がり分散されるが、(作業が)それぞれのrouteeで様々なときに発生し続けるようなrouterについては考えないようにしましょう。

> See Figure 1-5 for an example.

図1-5の例を見て下さい。

# ScatterGatherFirstCompletedOf

> This is a strategy where messages are sent to all instances of the actor the router controls, but only the first response from any of them is handled.

routerがコントロールしている全てのアクターインスタンスに対してメッセージが送られるが、いくつかのアクターからの最初の返答のみを扱う戦略です。

> This is good for situations where you need a response quickly and want to ask multiple handlers to try to do it for you.

これ(ScatterGatherFirstCompletedOf)は、素早いレスポンスを必要とする場面や、あなたのためにresponseを返してくれる複数のハンドラ(アクター)に(作業を)依頼したい状況で有効です。

> In this way, you don't have to worry about which routee has the least amount of work to do, or even if it has the fewest tasks queued, since those tasks won't take longer than another routee that already has more messages to handle.

この方法では、どのrouteeが最も抱えている仕事が少なくて、かつキューに入ったタスクが小さくて、既にたくさんのメッセージを持っている他のアクターよりも仕事の完了が早いかどうか、ということを考える必要はなくなります。

> This is particularly useful if the routees are spread among multiple JVMs or physical boxes.

もしルートが複数のJVMや物理ボックスに広がるならこれは特に役に立つ。

> Each of those boxes might be utilized at varying rates, and you want the work to be performed as quickly as possible without trying to manually figure out which box is currently doing the least work.

それぞれのboxはいろんな用途に使いたいし、現在抱えている仕事が最も少ないboxはどれかということを手動で明らかにすることなく、可能な限り速く仕事を完了させたいですよね。

> Worse, even if you did check to see if a box was the least busy, by the time you figured out which box it was and sent the work, it could be loaded down chewing through other work.

悪いことに、あなたがあるboxが最も忙しくなかったことを目視で確認したとしても、あなたが、メッセージを送った暇なboxがどれなのか確認した瞬間には、そのboxは他の仕事を咀嚼することで手一杯になるだろう。

> In Figue 1-6, I'm sending the work across five routees.

図1−6では、私は5つのrouteeを横切って作業を送っている。

> I only care about whichever of the five completes the work first and responds.

私は5つのうち最初に作業を完了させ応答したrouteeだけ相手をする。

> This trades some potential network latency (if the boxes [are more than one] physically close hop away) and extra CPU utilization (as each of the routees has to do the work) for getting the response the fastest.

この戦略は、レスポンスを最速で取得するために、いくらかの潜在的なネットワークレイテンシとCPUの更なる利用を犠牲にする。
相手されなかったけどresponse返そうとしたrouteeの分だけCPUを無駄に使う









