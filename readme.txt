BG_ALPHA_STUDIO_1.03
====================

【命名規則】
・フォルダー名：BG_ALPHA_STUDIO_1.03（英大文字）
・ファイル名：英小文字snake_caseと版数
   bg_alpha_studio_1.03.pyw
   build_exe.bat
   bg_alpha_studio_1.03.zip
・日本語UIタイトル：背景一発除去・透過MOV化 Ver.1.03
・画面タイトルと画面右上の版数は .pyw/.exe のファイル名末尾から取得。
  bg_alpha_studio_1.03.pyw にリネーム → 「Ver.1.03」
  bg_alpha_studio_1.08.exe にリネーム → 「Ver.1.08」
  ダウンロード重複名（1）等が付いても版数のみ取得する。
・アプリ名の日本語表記は変更しない。ファイル名からは「版数だけ」を抽出する。

【Ver.1.03の修正】
1. PhotoshopのJSXが現在の処理画像番号・完了枚数を記録。
2. UIの処理状況に「何枚目 / 全何枚・完了枚数・%」をリアルタイム表示。
3. ログに10枚ごとの進行状況を追記。
4. 背景除去工程では、進行バーを実際の枚数と連動。
5. フォルダー名（英大文字）とファイル名（英小文字）を命名規則へ統一。
6. .pyw/.exe の実行ファイル名から版数を抽出し、画面に追従。
7. PNG分解・Photoshop一括背景除去・音声付き透過MOV生成は維持。

【必要環境】
・Windows 10/11
・Adobe Photoshop（配布先のPCにも必須。Photoshopは同梱されません）
・FFmpeg（.pyw版ではPATHもしくはローカル配置、EXEビルド時には組み込み）
・.pyw実行PC：Python 3.10以降、CustomTkinter
・EXE作成PC：Python 3.10以降、インターネット接続（初回pip導入時）
・完成EXEの実行PC：Python、CustomTkinter不要。ただしPhotoshopは必要。

【.pywを実行する】
1. コマンドプロンプトで python -m pip install customtkinter を実行。
2. ffmpeg.exe をPATHに置くか .pyw の同じフォルダーに置く。
3. bg_alpha_studio_1.03.pyw を起動する。
4. 動画と出力フォルダーを指定して「一括変換を開始」。

【EXE化】
1. bg_alpha_studio_1.03.pyw と build_exe.bat を同じフォルダーに置く。
2. build_exe.bat をダブルクリックする。
3. 同じフォルダーにある bg_alpha_studio_*.pyw を自動検出し、
   ファイル名に合わせて dist\bg_alpha_studio_1.03.exe を出力する。
4. .pywを1.03にリネームして再ビルドするとEXE名も1.03になる。
   ただし.pywが複数あると誤選択防止のためビルドを停止する。
5. FFmpegの自動検出に失敗した場合、ffmpeg.exeをBATの隣に置いて再実行。
6. PythonとPyInstallerのインストールはEXE作成側のみ必要。

【変換工程】
① MP4等の動画を読み込み、元FPSを検出してPNG連番へ分解。
② 内蔵JSXを自動生成し、Photoshopで一括背景除去。
③ 処理結果の枚数と透過画素を検証し、QTRLE/ARGB形式の透過MOVへ戻す。
④ ONの場合、元動画の音声も収録。
⑤ 中間PNGとJSXは作業フォルダー内に保持。

【補足】
・PhotoshopのCOM自動実行に失敗したときは、作業フォルダーの
  photoshop_remove_bg.jsx をPhotoshopで手動実行して続行可能。
・QTRLE形式のMOVはファイル容量が大きく、VLCでは再生が重くなる場合あり。
  Clipchamp等の編集ソフトで確認するか、合成後にMP4化してください。
・元映像が可変フレームレートのときは、固定FPSで再構築することで
  時刻のズレが発生する場合があります。
・配布にあたりFFmpegの再配布条件、Photoshopの利用条件を確認してください。

【今回の検証範囲】
・Python構文チェック済み。
・リネーム前後の日本語タイトルと版数抽出のテスト済み。
・UIのWindows実機描画、およびPhotoshop経由の通し動作は未実施。
  交流会の前に短い動画で1本通し試験してください。

【Photoshop進捗の表示】
・JSXが作業フォルダー内の photoshop_progress.txt を随時更新。
・現在処理中の番号、完了枚数、合計枚数、成功/スキップ/エラーを記録します。
・画面上は約0.3秒間隔で更新。ログは10枚ごとに追記。
・完了後、これまで通り photoshop_result.txt に処理結果を保存します。
・Photoshopの実処理中に表示されるため、エクスプローラーを開く必要がありません。
・PNG連番分解とMOV生成中は、進行バーがアニメーションします。
