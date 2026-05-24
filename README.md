# pi-hex-results

円周率の16進表記について、BBP/Bellard系の式を用いて特定桁から計算した結果と、その検証用データを公開するためのリポジトリです。

このリポジトリ本体には、説明文、集計CSV、検証用スクリプト、SHA256チェックサムを置きます。大量の計算結果ファイルはGit管理には入れず、GitHub Releasesの添付ファイルとして配布します。

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
