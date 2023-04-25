## ダッシュボード
Instana にログインすると、以下のような画面が表示されます。  
<img width="1814" alt="image" src="https://user-images.githubusercontent.com/22209835/234153424-a1d3d2a3-519e-4623-8ecc-827c2a1ea6ff.png">

左のメニューにあるように Instanaでは、Infrastructure から、Platform、アプリケーション さらには Web Site & Mobile Apps (エンドユーザー・モニタリング）まで多様な環境を見ていくことが可能です。
<img width="1814" alt="image" src="https://user-images.githubusercontent.com/22209835/234153484-6d70872e-b199-4d4a-9ad7-ec3fcaea97ec.png">

この環境で IBM Instana Observability を、順に見ていきましょう。  
まず 取得した各種メトリックが統合されている Infrastructure & Platform の足回りから見ていきます。  
なお、この環境は実際に IBM Cloud 上で動いていて、擬似的に問題も発生させている環境ですので、開いたタイミングによって 表示される内容や発生するエラーは異なりますので、ご留意ください。

---

## Infrastructure 
1. インフラストラクチャでは、エージェントが導入されている各ホスト・ノードが 一元化されて把握できるようになっています。  
エージェントには、ゾーンを関連づけ、カスタマイズすることができます。東京データセンター、大阪災体データセンターなど、自由に関連付けて管理することが可能です。
AWSなどのパブリック・クラウド環境においては、インスタンスが配置されている ゾーンがデフォルトとして設定されます。
<img width="1811" alt="image" src="https://user-images.githubusercontent.com/22209835/234153645-4820b02e-c581-4069-ac9f-eb7128315e8c.png">

1. 上の **比較表** をクリックすると、一覧表示の形で、デフォルトではホスト（エージェントの導入されたOS環境）が表示されていますが、各種コンテナーやJavaなどもリストアップできます。
<img width="1815" alt="image" src="https://user-images.githubusercontent.com/22209835/234154413-90e3b77d-e449-463d-9b53-e7e2b9824b34.png">

1. **選択したホストのメトリックの視覚化** を選ぶと、特定のメトリックをグラフ表示することができます。ここで表示したメトリックはCSV に落とすことも可能です。  **CPU > 使用中** を選んで、 apnode01 と apnode 02 を選択してみましょう。
<img width="1815" alt="image" src="https://user-images.githubusercontent.com/22209835/234154473-c7386c36-bb71-4b2d-97e9-9ac7a4c6388b.png">

再び **Map**に戻ります。　　
<img width="1818" alt="image" src="https://user-images.githubusercontent.com/22209835/234153778-922e7999-7060-4fec-9707-cf86a0beeb60.png">

1. 色が付いているブロックがあれば、そこは問題が発生している環境です（環境のタイミングによって、存在するとはかぎりません）。例えば、上の黄色のブロックは TCP再送が永久に繰り返されてノード自体の問題が疑われるノードです。
  ![image](https://user-images.githubusercontent.com/22209835/114138096-168d8300-9948-11eb-9ce3-5b17856c369f.png)



1. **hmadison** や **k8sdemo** は、Kubernetes環境のノードです。クリックすると、そのノードで検知されているテクノロジーのスタックが表示されます。  
左にはそのノードの詳細が表示されます。ホスト名から分かるように gkeで稼働するKubernetesの WorkerNodeです。
![image](https://user-images.githubusercontent.com/22209835/114138304-68cea400-9948-11eb-9692-e26f9c429d62.png)
1. ノード情報の下の方には、そのノードで稼働する各種サービスのスタックが表示されています。それそれリンクになっていますので、検知されたサービスのダッシュボードへと飛ぶことも可能です。
![image](https://user-images.githubusercontent.com/22209835/114138551-c4992d00-9948-11eb-92b3-fa60ffe25499.png)
1. ノード情報の上の方にある 緑色の **Open Dashboard** の画面を開きます。ノードのリソースの詳細情報が確認できます。  
CPUやメモリの利用量から、Open Files数、File Systemの情報、ネットワークのアクティビティなど、基盤的な情報を確認することができます。メトリックは１秒単位の高精細なデータで、スパイクを見逃しません。
![image](https://user-images.githubusercontent.com/22209835/114138732-032ee780-9949-11eb-8091-28005f6e4a71.png)
1. 上の **Stack**タブをクリックすると、このノードで稼働している アプリケーションやKubernetesのスタックの情報が確認できます。
![image](https://user-images.githubusercontent.com/22209835/114139481-142c2880-994a-11eb-8bd1-541edfcc335a.png)

---
## Platform
1. つぎにアプリケーションが稼働するプラットフォームを見ていきましょう。  ※ 環境によっては Kubernetesクラスタが統合されていない環境もありますので、その場合は以下の説明をご確認ください。　　
1. KubernetesやCloudFoundry、この環境には表示されていませんが vSphereや PowerVM の情報も見ていくことが可能です。
vSphereはvCenterから、PowerVM の環境ではPowerHMCから情報を取得します。
<img width="1816" alt="image" src="https://user-images.githubusercontent.com/22209835/234155003-0a9f6233-64e7-432e-976c-97461aeae72d.png">

1. ひとつ定義されている demo-cluster が確認できます。右端の*正常性*は 緑色チェックマークで 大きな問題はないようですね。  
demo-cluster のリンクをクリックして、見ていきましょう。
<img width="1818" alt="image" src="https://user-images.githubusercontent.com/22209835/234155344-c693a432-542b-42e1-8dfe-fbc86df4ddb8.png">

1. 各クラスター全体のダッシュボードが開きます。  
CPUやメモリーなどのリソース状況、利用状況上位のノードや名前空間のリストがあります。
<img width="1912" alt="image" src="https://user-images.githubusercontent.com/22209835/234155561-709fe4c5-ded5-47d2-87a2-cfbfe515a74e.png">

1. メニューの **スタック**をクリックすると、このクラスターに関係する アプリケーションやInfrastructure の情報がリストされて表示されます。
<img width="1909" alt="image" src="https://user-images.githubusercontent.com/22209835/234155653-6f5577cc-78cf-422b-a755-481e8b13a0c7.png">
1. Kubernetesの各種リソースがタブとして整理されていますので、確認してみてください。  
とくに Pod のタブでは、リソースの Requests/Limitsの値をグラフィカルに表示することもできますので、どの名前空間のPodがリソースを消費する設定となっているかなど確認することができます。
<img width="954" alt="image" src="https://user-images.githubusercontent.com/22209835/234155747-e346dbfb-095b-43f4-884e-6bdfe78fb19e.png">
1. 気になる Podがあれば、その Podの情報をクリックすることで、Podのダッシュボードに移動し、実際のリソース利用状況などを確認できます。
<img width="1912" alt="image" src="https://user-images.githubusercontent.com/22209835/234155921-8f436eeb-8c46-444e-9436-c02b62f966af.png">

---
【参考】  
この環境には含まれていませんが、製品版ではOpen Betaのステータスで Kubernetesの各コンテナの出力するログ・メッセージをInstanaで集約表示する Kubernetes Logging 機能を提供しています。
クラスター、名前空間、Pod、コンテナーの各レベルにおいて、ログ・メッセージを表示することが可能です。また解析機能を使って、サービスごとにまとめて表示するなど、Kubernetes/OpenShift環境での問題判別が加速する機能ですね。GAして早くお届けできることを楽しみにしています。
<img width="2043" alt="image" src="https://user-images.githubusercontent.com/22209835/189812350-526eac91-67ff-44f6-9c50-b1b5e2105c88.png">
<img width="1993" alt="image" src="https://user-images.githubusercontent.com/22209835/189812434-586521f3-cd69-451f-a656-0eef6595dc6a.png">

---
これで **Infrastructure & Platform** の確認は終わりです。  
様々な環境に関わるリソース情報が整理され、それぞれ関連付けられて、コンソールに統合されていることが理解頂けたと思います。  
次にトレースとログの解析結果を可視化している [Application](https://github.com/ICpTrial/InstanaLab/blob/main/Applications.md) を見ていきたいと思います。

