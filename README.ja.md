# mgrs

[
![npm version](https://badge.fury.io/js/mgrs.svg)
](https://badge.fury.io/js/mgrs)
[
![Build Status](https://travis-ci.org/proj4js/mgrs.svg?branch=master)
](https://travis-ci.org/proj4js/mgrs)

WGS84の緯度経度とMGRS座標を変換するためのユーティリティです。[proj4js](https://github.com/proj4js/proj4js)から派生しました。

## インストール

npmからパッケージをインストールします:

```bash
npm install mgrs
```

## 使用方法

### Node.js (CommonJS)

```javascript
const mgrs = require('mgrs');

const mgrsString = '33UXP04';
const point = mgrs.toPoint(mgrsString);
console.log(point);
//=> [ 16.414501..., 48.249492... ]

const bbox = mgrs.inverse(mgrsString);
console.log(bbox);
//=> [ 16.35842, 48.20443, 16.4705, 48.29443 ] (概算)
```

### ES Module

CDNから直接モジュールをインポートできます:

```javascript
import * as mgrs from "https://code4fukui.github.io/mgrs/mgrs.js";

const mgrsStr = "33UXP04";
const point = mgrs.toPoint(mgrsStr);
console.log(point);
```

## API

### `mgrs.forward(coordinates, [accuracy])`

WGS84座標をMGRS文字列に変換します。

-   `coordinates` `<Array<number>>`: `[経度, 緯度]` の配列。
-   `accuracy` `<number>` (オプション): MGRS文字列の希望する精度。`5` は1m（デフォルト）、`4` は10m、`3` は100m、`2` は1km、`1` は10km。
-   **戻り値** `<string>`: MGRS文字列。

```javascript
const point = [16.4145, 48.2495];
const mgrsString = mgrs.forward(point, 5);
//=> '33UXP0500444997'
```

### `mgrs.inverse(mgrsString)`

MGRS文字列をWGS84のバウンディングボックスに変換します。

-   `mgrsString` `<string>`: MGRS文字列。
-   **戻り値** `<Array<number>>`: バウンディングボックスの配列 `[左, 下, 右, 上]` （または `[minLon, minLat, maxLon, maxLat]`）。

```javascript
const bbox = mgrs.inverse('33UXP04');
//=> [ 16.358..., 48.204..., 16.470..., 48.294... ]
```

### `mgrs.toPoint(mgrsString)`

MGRS文字列を、MGRSグリッドスクエアの中心を表すWGS84のポイントに変換します。

-   `mgrsString` `<string>`: MGRS文字列。
-   **戻り値** `<Array<number>>`: `[経度, 緯度]` の中心点。

```javascript
const point = mgrs.toPoint('33UXP04');
//=> [ 16.41450..., 48.24949... ]
```

## 開発

ローカルでこのプロジェクトを開発するには、リポジトリをクローンし、開発用の依存関係をインストールします:

```bash
npm install
```

### テスト

テストスイートを実行します:

```bash
npm test
```

### ビルド

配布用ファイルをビルドします:

```bash
npm run build
```

## 参考資料

-   Wikipedia: [Military Grid Reference System](https://en.wikipedia.org/wiki/Military_Grid_Reference_System)
-   GEOTRANS: [Geographic Translator](https://earth-info.nga.mil/#geotrans)

## ライセンス

以下を除き、MIT licenseの下でライセンスされています:

本ソフトウェアの一部は、OpenMapの com.bbn.openmap.proj.coords Javaパッケージのコンポーネントの移植に基づいています。初期の移植はPatrice G. Cappelaereによって作成され、Community Mapbuilder (http://svn.codehaus.org/mapbuilder/) に含まれていました。これは http://www.gnu.org/copyleft/lesser.html にある通り、LGPL licenseの下でライセンスされています。OpenMapは[こちらのライセンス契約](openmap.md)の下でライセンスされています。
