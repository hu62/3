
まずカメラを使って名刺をスキャンする.背景が何もなくてが暗いところに名刺を置いてカメラに写すと
青い線が出てくる.その青い線が四角く名刺を囲ったところで'escキー'か'q'を押すとその名刺を読み取り
名刺だけの画像を表示するというプログラム.

カメラから画像を読み取り,二値化行って明るいところと暗い所にわけ
その明るいところでも面積が大きくなっているところを発見し,
それを囲うことでスキャンしている.

読み取った画像は

#読み取った名刺を表示
dst = []

pts1 = np.float32(areas[0])
pts2 = np.float32([[600,300],[600,0],[0,0],[0,300]])

M = cv2.getPerspectiveTransform(pts1,pts2)
dst = cv2.warpPerspective(frame,M,(600,300))

で枠の各点を対応する座標にあわせて射影変換する.
そして回転をしているがこれはなぜか毎回反転した画像が表示されるので
わかりやすいように180度回転して表示するようにした.

自分が実装したのは,サイトは元からある画像を読み取っていたので
自分はカメラから読み取り,それを終了させてから枠で囲ったところを表示させるように変えた.

引用しているのは,コード内の
#二値化,#輪郭抽出,#面積の大きいもののみ選出,#読み取った名刺を表示(rota = ...以外)
はほぼそのまま使用させてもらった.


実際に動作した動画: https://youtu.be/ZxY-Xog8CyA

参考にしたサイト:https://qiita.com/mix_dvd/items/5674f26af467098842f0
