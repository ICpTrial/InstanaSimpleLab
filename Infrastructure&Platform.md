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

---
## Platform
1. つぎにアプリケーションが稼働するプラットフォームを見ていきましょう。※環境によっては Kubernetesクラスタが統合されていない環境もありますので、その場合は以下の説明をご確認ください。
```
KubernetesやOpenShift環境においても、DaemonSetとして稼働するInstana Agentを導入することで、  
コンテナの定義にアノテーションを入れたり、アプリケーションを修正したりすることなく、コンテナの状況やアプリケーションの情報を取得することができます。    
手間のかかる設定は不要で、すぐにデータの取得が行われ可視化が行われる点は、多くのお客様に評価いただいているポイントです。
```
3. KubernetesやCloudFoundry、この環境には表示されていませんが vSphereや PowerVM の情報も見ていくことが可能です。vSphereはvCenterから、PowerVM の環境ではPowerHMCから情報を取得します。<img width="1816" alt="image" src="https://user-images.githubusercontent.com/22209835/234155003-0a9f6233-64e7-432e-976c-97461aeae72d.png">

1. ひとつ定義されている *demo-cluster* が確認できます。右端の**正常性**は 緑色チェックマークで 大きな問題はないようですね。  
*demo-cluster* のリンクをクリックして、見ていきましょう。<img width="1818" alt="image" src="https://user-images.githubusercontent.com/22209835/234155344-c693a432-542b-42e1-8dfe-fbc86df4ddb8.png">

1. 各クラスター全体のダッシュボードが開きます。CPUやメモリーなどのリソース状況、利用状況上位のノードや名前空間のリストがあります。<img width="1912" alt="image" src="https://user-images.githubusercontent.com/22209835/234155561-709fe4c5-ded5-47d2-87a2-cfbfe515a74e.png">

1. メニューの **スタック**をクリックすると、このクラスターに関係する アプリケーションやInfrastructure の情報がリストされて表示されます。<img width="1909" alt="image" src="https://user-images.githubusercontent.com/22209835/234155653-6f5577cc-78cf-422b-a755-481e8b13a0c7.png">
1. Kubernetesの各種リソースがタブとして整理されていますので、確認してみてください。とくに Pod のタブでは、リソースの Requests/Limitsの値をグラフィカルに表示することもできますので、どの名前空間のPodがリソースを消費する設定となっているかなど確認することができます。<img width="954" alt="image" src="https://user-images.githubusercontent.com/22209835/234155747-e346dbfb-095b-43f4-884e-6bdfe78fb19e.png">
1. 気になる Podがあれば、その Podの情報をクリックすることで、Podのダッシュボードに移動し、実際のリソース利用状況などを確認できます。<img width="1912" alt="image" src="https://user-images.githubusercontent.com/22209835/234155921-8f436eeb-8c46-444e-9436-c02b62f966af.png">

---
【参考】  
この環境には含まれていませんが、製品版ではOpen Betaのステータスで Kubernetesの各コンテナの出力するログ・メッセージをInstanaで集約表示する Kubernetes Logging 機能を提供しています。
クラスター、名前空間、Pod、コンテナーの各レベルにおいて、ログ・メッセージを表示することが可能です。また解析機能を使って、サービスごとにまとめて表示するなど、Kubernetes/OpenShift環境での問題判別が加速する機能ですね。GAして早くお届けできることを楽しみにしています。
<img width="2043" alt="image" src="https://user-images.githubusercontent.com/22209835/189812350-526eac91-67ff-44f6-9c50-b1b5e2105c88.png">
<img width="1993" alt="image" src="https://user-images.githubusercontent.com/22209835/189812434-586521f3-cd69-451f-a656-0eef6595dc6a.png">

---
これで  **インフラストラクチャ** および **プラットフォーム** の確認は終わりです。  
様々な環境に関わるリソース情報が整理され、それぞれ関連付けられて、コンソールに統合されていることが理解頂けたと思います。  
次に分散トレースとログの解析結果を可視化している [アプリケーション](https://github.com/ICpTrial/InstanaLab/blob/main/Applications.md) を見ていきたいと思います。
