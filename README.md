# pi-hex-results

円周率の16進表記について、BBP/Bellard系の式を用いて特定桁から計算した結果と、その検証用データを公開するためのリポジトリです。

このリポジトリ本体には、説明文、集計CSV、検証用スクリプト、SHA256チェックサムを置きます。大量の計算結果ファイルはGit管理には入れず、GitHub Releasesの添付ファイルとして配布します。

## Results

本リポジトリでは、円周率の整数部 `3` は数えず、16進小数部の桁位置を1始まりで数えます。

計算には、OpenCL/HSPで実装したCLBellardを使いました。

https://github.com/toropippi/CLBellard

主な計算結果は次のとおりです。

| 位置 | 開始位置 | 2回の計算で一致した桁列 |
| --- | ---: | --- |
| 2000兆桁 | `2×10^15` | `653728f1d92ef9802795ab97da55` |
| 1京桁 | `1×10^16` | `9077e0164b9c613fd6c7f170c99` |
| 2京桁 | `2×10^16` | `1021b52fb719ada36b81d6cecc9` |
| 10京桁 | `1×10^17` | `a937eb59439e485e2eb4f5feb7820` |

検証は、同じ開始位置からの計算と、5桁手前からの計算を比較する形で行いました。1回目は `N` から、2回目は `N-5` から計算し、2回目の先頭5桁を読み飛ばした位置から1回目と比較しています。

特に10京桁目については、16進小数部の `10^17` 桁目から次の29桁が2回の計算で一致しました。

```text
a937eb59439e485e2eb4f5feb7820
```

この先頭16桁は、高橋大介氏が公開している10京桁目からの16桁 `A937EB59439E485E` と一致しています。

詳細な計算記録、計算時間、エラー発生回数、参考文献はZenn記事「GPUで円周率の16進10京桁目から29桁を計算した記録」にまとめます。

## Data

計算結果ZIPは v1.0 Release からダウンロードできます。

https://github.com/toropippi/pi-hex-results/releases/tag/v1.0

Release assetsとして、次のZIPファイルを配布しています。

- `pi-hex-1999-trillion.zip`
- `pi-hex-3999-trillion.zip`
- `pi-hex-4000-trillion.zip`
- `pi-hex-1e16.zip`
- `pi-hex-1e16-minus-5.zip`
- `pi-hex-2e16.zip`
- `pi-hex-2e16-minus-5.zip`
- `pi-hex-1e17.zip`
- `pi-hex-1e17-minus-5.zip`

各ZIPには、計算結果のテキストファイルと、集計用CSVが含まれます。

## Checksums

ZIPファイルのSHA256は `checksums-sha256.txt` に記録しています。

Windows PowerShellでは、次のように確認できます。

```powershell
Get-FileHash .\pi-hex-1e17.zip -Algorithm SHA256
```

出力された `Hash` が `checksums-sha256.txt` の値と一致すれば、ダウンロードしたZIPが公開時のファイルと一致していることを確認できます。

## Summary CSV

Excel由来のメタデータを避けるため、集計表はCSV形式で保存しています。

CSVには、各計算デバイスごとの仕事量、計算時間、1 batchあたりの時間などを記録しています。

## Scripts

検証や集計に使ったHSPスクリプト類を保存しています。

- `hexsademical.as`
- `hikaku.hsp`
- `hikaku2.hsp`
- `workmodeSum0_6.hsp`
- `計算時間統計.hsp`

## Notes

- 元のExcelファイルは公開対象に含めません。
- 大量の `.txt` ファイルはGitHubの通常コミットには含めず、Release assetsとしてZIP配布します。
- 再現性確認では、ZIPのSHA256と、同じ桁位置を別開始位置から計算した結果の重なりを確認します。
