<!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="UTF-8">
    <title>自作TRPGキャラシ</title>
</head>
<body>
    <h1>キャラクター作成</h1>
    
    <div>
        <label>名前: <input type="text" id="name"></label><br>
        <label>性別: <input type="text" id="gender"></label><br>
        <label>身長: <input type="number" id="height">cm</label><br>
        <label>体重: <input type="number" id="weight">kg</label><br>
        <label>階級: <input type="text" id="rank"></label>
    </div>

    <button onclick="copyToCcfolia()">ココフォリア用データをコピー</button>

    <script src="script.js"></script>
</body>
</html>

function copyToCcfolia() {
    // フォームの入力値を取得
    const name = document.getElementById('name').value;
    const gender = document.getElementById('gender').value;
    const height = document.getElementById('height').value;
    const weight = document.getElementById('weight').value;
    const rank = document.getElementById('rank').value;

    // ココフォリア用のデータ構造を作る（V1形式）
    const charaData = {
        kind: "character",
        data: {
            name: name,
            memo: `性別: ${gender}\n身長: ${height}cm\n体重: ${weight}kg\n階級: ${rank}`,
            initiative: 0,
            params: [],
            commands: ""
        }
    };

    // JSON文字列に変換
    const jsonText = JSON.stringify(charaData);

    // クリップボードにコピー
    navigator.clipboard.writeText(jsonText).then(() => {
        alert("ココフォリア用データをコピーしました！\nココフォリアの盤面でCtrl+V(Cmd+V)してください。");
    }).catch(err => {
        alert("コピーに失敗しました: " + err);
    });
}
