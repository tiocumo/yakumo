# Yakumo
JavaScript用の複数ファイルからビルドするやつ
Kagura.jsを開発するときに、Webpackがめんどくさかったので作成
## 使い方
importは、```import yakumo```
### とりあえずビルド
```python
ran=yakumo.Yakumo(config-json) #インスタンス作成
print(ran.build()) #ビルド
```
それか、単にファイルを作るなら
```python
yakumo.build(config-json-path, output-path)
```
で。
### CONFIGの書き方
jsonで書きます。  
```"root"```: ソースファイルのルートを指定します。  
```"main"```: もととなるファイルを指定します。ここからさまざまなスクリプトを埋め込みます。  
```"files"```: リスト形式で指定します。使うファイルを指定します。ここに書いていないファイルは読み込めません。  
```"split"```: 読み込むときの記号をしていします。例えば、```{{}}```で囲んだものを外部ファイルとしたい場合は、
```json
"split":{
  "start":"{{",
  "end":"}}"
}
```
とします。
### スクリプトの書き方
ConfigのSplitで指定した文字列で外部ファイルを囲みます。  
例:  
configに
```json
{
  "split":{
    "start":"{{",
    "end":"}}"
  },
  "root":"./",
  "files":["index.js","a.js"],
  "main":"index.js",
}
```
と書きます。
```"hello"```を a.js に入れます。  
index.jsに```alert({{a.js}})```と書きます。  
そしてbuildすると、
```js
alert("hello")
```
となります。