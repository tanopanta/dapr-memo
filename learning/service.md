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
  - ☆ daprのバージョン差異がある場合の挙動とか大丈夫かな
     - 同じメジャーバージョンかつサポートバージョンであれば大丈夫なように作ると思われるが、その挙動が十分にテストされているかどうか
- クラスタ横断のissue: https://github.com/dapr/dapr/issues/5389

## pub sub
- invokeだとレスポンス遅延の影響を受ける
- メッセージ基盤があればpublishするだけなのでフロントエンドに早めにレスポンスを返せる
- キューの重複排除や優先度などの恩恵も受けられる
- cloudevents形式のメタデータが付与される
  - https://github.com/dapr/go-sdk/blob/b465b1fa07211ee8a43bdd66906423d2e9e14ebd/dapr/proto/runtime/v1/appcallback.pb.go#L141

## Component
- middleware
  - https://github.com/dapr/components-contrib/tree/master/middleware/http
  - opaがいる

## tracing
- daprのサイドカーにより複雑性は増すが、リクエストをすべてキャッチ可能なのでtraceできるようになる
- アプリケーションのコードにtrace関連の処理を書かなくて良くなる
- X-Collection-ID を使う
