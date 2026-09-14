# オフライン環境でPythonパッケージを準備する

会社PCでは、プロキシ、ファイアウォール、インターネット接続制限などにより、`pip install` がPyPIへ接続できない場合があります。

このスターターキットでは、その場合に備えて、必要なパッケージを別の環境で取得し、アプリの `packages/` フォルダからインストールできるようにします。

## 基本方針

- `requirements.txt` はオンライン・オフラインのどちらでも共通して使用する
- アプリ直下の `packages/` は、ローカルインストール用のパッケージ置き場とする
- `packages/` にパッケージがある場合は、ネットワークへ接続せずローカルからのインストールを優先する
- `packages/` が空または存在しない場合は、通常の `pip install -r requirements.txt` を使用する
- 会社で使用する場合は、勤務先のソフトウェア利用・持ち込み・ライセンス・セキュリティ規程を優先する

## 1. インターネットへ接続できるPCで取得する

`requirements.txt` があるフォルダで、次を実行します。

```powershell
python -m pip download --destination-directory packages -r requirements.txt
```

このコマンドは、`requirements.txt` に書かれたパッケージだけでなく、必要な依存パッケージも `packages/` へ取得します。

可能であれば、実際に使用する会社PCと同じPythonのバージョン、OS、CPUアーキテクチャに近い環境で取得してください。

## 2. `packages/` を会社PCへコピーする

USBメモリ、社内で承認されたファイル共有、その他勤務先で許可された方法を使用します。

会社の許可なく外部媒体や外部クラウドサービスを使用しないでください。

コピー後は、例えば次のような構成になります。

```text
my-python-app/
├── requirements.txt
├── start.bat
├── main.py
└── packages/
    ├── package_a-1.0.0-py3-none-any.whl
    ├── package_b-2.0.0-py3-none-any.whl
    └── ...
```

## 3. ローカルだけからインストールする

次の形式でインストールします。

```powershell
python -m pip install --no-index --find-links=packages -r requirements.txt
```

`--no-index` はPyPIなどのパッケージインデックスへ接続しない指定です。`--find-links=packages` は `packages/` の中からパッケージを探す指定です。

## `start.bat` での扱い

Windows向けアプリでは、`packages/` にパッケージファイルがある場合はローカルインストールを優先します。

```bat
if exist packages\*.whl (
    echo ローカルパッケージから必要なライブラリを準備します。
    python -m pip install --no-index --find-links=packages -r requirements.txt
) else (
    echo インターネットから必要なライブラリを準備します。
    python -m pip install -r requirements.txt
)
```

`.whl` 以外の配布ファイルも利用するアプリでは、AIがその構成に合わせて判定方法を調整します。

## Wheelファイルについて

`.whl`（Wheel）は、Pythonパッケージのインストール用ファイルです。オフライン環境では、ソースコードからビルドする必要があるパッケージより、対応するWheelを使用できる方が初心者には扱いやすくなります。

ただし、Wheelによっては次の条件が決まっています。

- Pythonのバージョン
- Windows / macOS / Linux
- 32bit / 64bit
- CPUアーキテクチャ

「このプラットフォームではサポートされていないWheel」などのエラーが出た場合は、パッケージファイルが使用するPCの環境に合っているか確認します。

## うまく取得できない場合

`pip download` でソース配布しか取得できず、会社PC側でビルドツールが必要になるパッケージもあります。その場合は、利用可能なWheelがあるか確認します。

必要に応じて、インターネットへ接続できる環境で次の方法も検討できます。

```powershell
python -m pip wheel --wheel-dir packages -r requirements.txt
```

ただし、Wheelの作成自体にコンパイラなどが必要になる場合があります。初心者向けアプリでは、可能な限り公式に配布されているWheelを利用できる依存関係を優先します。

## GitHubへ登録するか

`packages/` の中身は、ファイルサイズ、ライセンス、社内利用規程、第三者パッケージの再配布条件などを確認する必要があるため、標準ではGitHubへ登録しません。

このスターターキットの `.gitignore` では `packages/` の実ファイルを除外します。必要であれば `packages/README.md` や `.gitkeep` だけを登録し、パッケージ本体は利用するPCへ別途配置します。
