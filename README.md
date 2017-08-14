# Filesystem Benchmark

## btrfsのサポートがRHELで断念される
[マイナビニュース](http://news.mynavi.jp/news/2017/08/04/056/)にこのような文章が発表されました  

> Btrfsは長年にわたって作業をしているにもかかわらず、依然として技術的な問題が存在しており今後も改善が期待しにくいこと、ZFSはライセンスの関係で取り込むことができないこと、既存の技術と継続しながら新技術を実現するという観点から、当面はXFSをベースとしつつ機能拡張を進めていく「Stratis」プロジェクトを進めることが妥当ではないかと提案している。

しかし、[ArchWik](https://wiki.archlinuxjp.org/index.php/Btrfs)には、このようにもあり、btrfsの今後がどうなるかよくわからないです  
> Btrfs またの名を "Better FS" — Btrfs は新しいファイルシステムで Sun/Oracle の ZFS に似たパワフルな機能を備えています。機能としては、スナップショット、マルチディスク・ストライピング、ミラーリング (mdadm を使わないソフトウェア RAID)、チェックサム、増分バックアップ、容量の節約だけでなく優れたパフォーマンスも得られる透過圧縮などがあります。現在 Btrfs はメインラインカーネルにマージされており安定していると考えられています [1]。将来的に Btrfs は全てのメジャーなディストリビューションのインストーラで標準になる GNU/Linux ファイルシステム として期待されています。

Linuxで使えるファイルシステムは多岐に渡りますが、何が最も良いのでしょうか。 

ビッグデータの用途で、File Systemを用いたKVSか、LevelDBなどのKVSを用いることがよくあり、この用途では細かい数キロから数メガのファイルを大量に作ります  
そのため、数多くのinodeを持つことができるbtrfsを今まで用いて来たのですが、他のファイルシステムも検討することにします  

## 検討対象のファイルシステムとその実験環境
まず、条件を整えるため、ハードウェアは固定します
- CPU: RYZEN7 1700X
- Memory: 36GByte DDR4
- HDD1: インテル SSD 600pシリーズ 512GB M.2 PCIEx4 (OS起動用)
- HDD2: SanDisk SSD UltraII 480GB（検証用）

OSとそのバージョン
- ArchLinux 4.12.4-1-ARCH (x86_64)
