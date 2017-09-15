# Maximum Flow

방향 그래프에서, 간선의 Capacity만큼의 flow가 흐를 수 있다고 했을 때, source에서 sink로 가는 최대의 flow를 구하는 문제이다.

## Ford-Fulkerson

먼저 Capacity가 오로지 1또는 0인\(0인 경우는 연결되지 않은 것과 같다\) 케이스를 살펴보자.

이때는, 만약 source에서 sink로 가는 path를 찾는 다면, 그 path가 1짜리 flow가 될 것이다.

Ford-Fulkerson에서는 이 path에 해당하는 엣지들을 모두 반대방향으로 돌린다.

계속해서 path를 찾고 방향을 반대로 돌리다보면, 결국 더 이상 path를 찾을 수 없게 될 것이다.

이 때, 여태까지 반대로 돌린 path의 개수가 maximum flow가 된다.

여기서, 엣지를 아예 없애지 않고 방향만 반대로 돌리는 이유가 뭘까?

maximum flow를 구할 때, 무작정 path를 찾아 없애다 보면 그것이 항상 최적해라고 보장할 수 없다. 하지만, path를 반대로 돌리기만 하면, 한번 찾은 path는 다시 사용하지 못한다는 점을 만족함과 동시에, 다음 번 path finding에서 실수를 만회할 수 있다.

![](/assets/simple graph.png)

만약 위와 같은 모양의 그래프가 있을 때,

우리가 맨 처음 찾은 path가 s-a-b-t라면, 그 다음 path finding때는, 필연적으로 s-c-b-a-d-t가 나올 것이다. 

이 s-c-b-a-d-t path는 정말로 flow가 저 모양새로 흐르는 것이 아니라, 사실은 두 가지 의미를 내포 하고 있다.

저 path대로 간선을 반대로 재구축하면, flow가 s-a-d-t, s-c-b-t 로 흐르는 것을 볼 수 있는데, 즉, 저 path가 처음 찾은 path를 수정해버린 효과를 낳은 것이다.

