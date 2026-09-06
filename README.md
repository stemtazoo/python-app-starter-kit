# Python App Starter Kit

AIと一緒に、小さなPython業務改善アプリを完成させるための初心者向けスターターキットです。

このリポジトリでは、最初から詳細な仕様を作り込むのではなく、次の流れを大切にします。

1. 困りごとと最初の完成条件を決める
2. 最小限の試作品を作る
3. 実際に動かして確認する
4. 必要な部分だけ改善する
5. 分かったことをREADMEや設計メモへ残す

> Prototype first, document as you learn.  
> まず試作品を作り、分かったことを後から記録する。

初心者がセットアップで迷わないよう、仮想環境は標準では使用せず、利用者から指示があった場合にだけ使用します。

Windows向けアプリでは原則として`start.bat`を用意し、ダブルクリックで起動できる状態を目指します。

## ドキュメント

- [AGENTS.md](AGENTS.md)  
  AIがアプリ制作を支援するときに守る、具体的な進め方と判断基準です。
- [開発原則](docs/development-principles.md)  
  初心者が途中で迷わず、小さな業務改善アプリを完成させるための基本方針です。
- [推奨ディレクトリ構成](docs/project-structure.md)  
  Pythonコード、設定、文書、テスト、業務データの標準的な置き場所です。

## 現在の状態

開発原則、AI向けの指示、推奨ディレクトリ構成を整備しました。今後、開発の始め方、記録用テンプレート、サンプルを順次追加します。

## 参考資料

このスターターキットは、次の資料を参考にしています。ただし、初心者が小さな業務改善アプリを早く完成させる目的に合わせて、手順や構成を簡略化しています。

- [GitHub Spec Kit](https://github.com/github/spec-kit)  
  仕様、計画、タスク、実装をつなげるSpec-Driven Developmentの考え方を参考にしています。本リポジトリでは、試作までの負担を減らすため「小さく試作してから記録する」流れへ調整しています。
- [Custom instructions with AGENTS.md](https://learn.chatgpt.com/docs/agent-configuration/agents-md)  
  Codexが`AGENTS.md`を読み込む範囲や、階層ごとに指示を分ける方法を確認できます。
- [PyPA sampleproject](https://github.com/pypa/sampleproject)  
  Pythonプロジェクトで使われる基本的なファイルやディレクトリ構成の参考です。
- [srcレイアウト対フラットレイアウト](https://packaging.python.org/ja/latest/discussions/src-layout-vs-flat-layout/)  
  Pythonコードを`src/`へ分ける場合の利点と注意点を学べます。本リポジトリでは、事前インストールを必須にしない形へ簡略化しています。
- [pip User Guide：Requirements Files](https://pip.pypa.io/en/stable/user_guide/#requirements-files)  
  `requirements.txt`を使って必要なライブラリをインストールする方法の公式資料です。
- [Python公式ドキュメント：`__main__`](https://docs.python.org/ja/3/library/__main__.html)  
  Pythonプログラムの起動地点と、`if __name__ == "__main__":`の考え方を確認できます。
- [GitHub公式 Python.gitignore](https://github.com/github/gitignore/blob/main/Python.gitignore)  
  PythonプロジェクトでGitHubへ登録しないファイルを判断するための基準です。

## ライセンス

このリポジトリは[MIT License](LICENSE)で公開しています。
