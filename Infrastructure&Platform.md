## ダッシュボード
1. Instana にログインすると、以下のような画面が表示されます。<img width="1814" alt="image" src="https://user-images.githubusercontent.com/22209835/234153424-a1d3d2a3-519e-4623-8ecc-827c2a1ea6ff.png">

1. 左のメニューにあるように Instanaでは、インフラストラクチャ から、プラットフォーム、アプリケーション さらには ウェブサイトおよびモバイル(エンドユーザー・モニタリング）まで多様な環境を見ていくことが可能です。<img width="1814" alt="image" src="https://user-images.githubusercontent.com/22209835/234153484-6d70872e-b199-4d4a-9ad7-ec3fcaea97ec.png">

1. この環境で IBM Instana Observability を、順に見ていきましょう。  
まず 取得した各種メトリックが統合されている **インフラストラクチャ** および **プラットフォーム** の足回りから見ていきます。  
なお、この環境は実際に IBM Cloud 上で動いていて、擬似的に問題も発生させている環境ですので、ハンズオンのタイミングによって 表示される内容や発生するエラーは異なりますので、ご留意ください。

---

## Infrastructure 
1. インフラストラクチャでは、エージェントが導入されている各ホスト・ノードが 一元化されて把握できるようになっています。  
エージェントには、ゾーンを関連づけ、カスタマイズすることができます。東京データセンター、大阪災体データセンターなど、自由に関連付けて管理することが可能です。
AWSなどのパブリック・クラウド環境においては、インスタンスが配置されている ゾーンがデフォルトとして設定されます。<img width="2054" alt="image" src="https://user-images.githubusercontent.com/22209835/234195517-fabf74f3-bcba-4f97-a796-4972e56bcca2.png">

1. 色が付いているブロックがあれば、そこは問題が発生している環境です（環境のタイミングによって、存在するとはかぎりません）。例えば、下の黄色のブロックは CPU IO Wait が発生し、問題が疑われるノードです。<img width="2054" alt="image" src="https://user-images.githubusercontent.com/22209835/234194765-e4cc222e-ec98-4a0e-88e3-3261dd6d2c70.png">

1. 当該ノードの ダッシュボードを開くを押すことで、当該OSの 詳細なメトリックの状況がわかります。<img width="2046" alt="image" src="https://user-images.githubusercontent.com/22209835/234195099-f30d3462-9e8d-4e90-87f1-7307312482bd.png">

1. 検知されているノードにカーソルを当てると、Instanaエージェントが検知して メトリックを取得している各種テクノロジーが 表示されます。関心のあるコンポーネント（WebSpehre ASやJVM、Db2など)を選択して、 **ダッシュボードを開く** を選択してみましょう。<img width="2053" alt="image" src="https://user-images.githubusercontent.com/22209835/234195934-75fea409-e04e-4418-9564-50a637db6c9b.png">


1. 各テクノロジーのメトリックが表示されます。Instanaは過去のお客様のフィードバックをベースに、各テクノロジーにおいて取得すべき重要なメトリックをあらかじめ定義し、(認証設定などをのぞき）できる限り自動的にメトリックを収集できるように設計されています。<img width="2053" alt="image" src="https://user-images.githubusercontent.com/22209835/234196796-442d11cb-d8bf-4833-8755-0a0e7672d5e1.png">

1. 各テクノロジーのページにおいて **スタック** を開くと、当該ページテクノロジーが関連するアプリケーション および その稼働する基盤としての技術スタックが表示されます。　　それぞれがリンクとなっていますので、各アプリケーション、技術スタックの詳細ページに飛ぶことが可能です。<img width="2056" alt="image" src="https://user-images.githubusercontent.com/22209835/234197061-68f0883e-ffaa-4924-9a8a-9ac918138ae0.png"><img width="2050" alt="image" src="https://user-images.githubusercontent.com/22209835/234197360-879e4058-3233-4153-80e3-46b12b98fc64.png">

1. 再び **Map**に戻ります。　　　
1. 上の **比較表** をクリックすると、一覧表示の形で、デフォルトではホスト（エージェントの導入されたOS環境）が表示されていますが、各種コンテナーやJavaなどもリストアップできます。<img width="1815" alt="image" src="https://user-images.githubusercontent.com/22209835/234154413-90e3b77d-e449-463d-9b53-e7e2b9824b34.png">

1. **選択したホストのメトリックの視覚化** を選ぶと、特定のメトリックをグラフ表示することができます。ここで表示したメトリックはCSV に落とすことも可能です。**CPU > 使用中** を選んで、 apnode01 と apnode 02 を選択してみましょう。<img width="1815" alt="image" src="https://user-images.githubusercontent.com/22209835/234154473-c7386c36-bb71-4b2d-97e9-9ac7a4c6388b.png">

これで  **インフラストラクチャ** および **プラットフォーム** の確認は終わりです。  
様々な環境に関わるリソース情報が整理され、それぞれ関連付けられて、コンソールに統合されていることが理解頂けたと思います。  
次に分散トレースとログの解析結果を可視化している [アプリケーション](https://github.com/ICpTrial/InstanaSimpleLab/blob/main/Applications.md) を見ていきたいと思います。
