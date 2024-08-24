<version>
python                    3.9.7
bokeh                     2.4.1
plotly                    5.14.1
pandas                    1.3.4
networkx                  2.6.3

<概要>
本内容は、サプライチェーン業務改革を中心に、約20年に渡る私のコンサル経験をもとに、特定の顧客の現場から離れた汎用化したモデルとして、
グローバル・サプライチェーンの計画モデルをpythonで実装することで、コンセプト検証( PoC:Proof of Concept)を行っています。
ご紹介するGlobal Supply Chain Planner(Global Weekly PSI Planner)の機能概要については、note記事の以下のURLを参照ください。
https://note.com/osuosu1123/n/n6e97b29049ca
  
note記事には、過去にGlobal Weekly PSI Plannerに関連する記事を何本か公開していますが、今回の変化点の大きな部分は、高速処理を行うために以下のような実装を行っています。
1) Forward PlanningとBackward Planingの部分はサプライチェーン・ツリー構造上の各node事業拠点をrecursive callする。
2) データ可視化のグラフィック・ライブラリは、いままでplotlyを使用していますが、webGL対応など高速描画の観点からbokehも使っています。

githubにuploadした現行version V0R2では、以下の二点の機能を追加しています。
1) サプライチェーンのツリー構造データをネットワーク最適化ライブラリnetworkXにマッピングして、最適化処理とネットワーク表示
2) サプライチェーン・ネットワークから各事業拠点nodeをクリックすると「ロット積上げ方式」PSIを表示
なお、売上・利益・利益率の推移グラフ化は、時系列グラフ機能を工夫して、もう少し見栄えを良くしてから公開したいと思います。

本件について、お気づきの点、疑問点などあれば、下記のgmailにお気軽にご連絡ください。
※レスポンスには時間がかかると思いますが、できるかぎり返信させていただきたいと思います。
ohsugi1031@gmail.com

Following URL(Japanese) show you a slight overview of this Global Weekly PSI Planner. 
https://note.com/osuosu1123/n/n6e97b29049ca
If you have some questions on this matter, feel free to reply to me. 

# supplychain_planner_PoC
Following perspectives are practical for modeling the supply chain:  1. Plan with a weekly granularity 2. Align with Common Planning Units across entire supply chain 3. Consider bottlenecks 4. Consider the cost structure and value linkage 5. Apply optimization functions  To verify these concepts, a simple planning tool is modeled in Python, as PoC.
# ****
When considering the planning functions of a global supply chain, I believe it is necessary to model the supply chain from the following perspectives:

- Starting from the method and timing of providing product services to customers
- Considering the balance of supply and demand across the entire supply chain
- Maintaining consistency between overall supply chain management and the order processing operations of individual business locations

Next, as the main considerations when modeling the supply chain, I believe that by advancing the modeling from the following perspectives, it is possible to realize a supply chain planning function that is practicalc:

1. Plan with a weekly granularity
2. Align with common product lots (common planning units) across the entire supply chain
3. Consider bottlenecks on both the supply side and the demand side
4. Consider the cost structure and value linkage of each business location
5. Apply optimization functions (mainly supply allocation problems, location problems, routing problems, etc.)

To verify these concepts (Proof of Concept: PoC), I have created a simple planning tool modeled in Python, which I would like to introduce.

