## 可用性
- クラウドを使うことで高可用性を手に入れることはできるが、再起動が発生する可能性は考慮する必要がある
- インメモリーな状態を持たないようにステートレスに作るべき
- 移行性も考えるとアプリケーションは小さいほうが良い

## Infrastructure is boring
- OAMと近い考え

## サービス間通信
- セルフホストの場合はmDNSが使える
  - > These instance can be on the same machine or on different machines. .
  - https://docs.dapr.io/developing-applications/building-blocks/service-invocation/service-invocation-overview/#round-robin-load-balancing-with-mdns
  - Edgeやレガシーシステムでも使えるように対応している
    - ☆ 昔IoT的なことをやっていたときにもmDNSはよく出てきた気がするので相性良いのかな
- クラスタ横断のissue: https://github.com/dapr/dapr/issues/5389
