Generated set #1 from the first 16 qwarc log files of JAA's (second) playback crawl using:
`grep -Fh ' stream: ' qwarc.{1..16}.log | sed "s,'$,,; s,^.*',," | ~/little-things/uniqify >tracks-1to16-unique` + `split -l50 -a4 tracks-1to16-unique list-`


Generated set #2 from the next 4 qwarc log files of JAA's (second) playback crawl using:
grep -Fh ' stream: ' qwarc.{17..20}.log | sed "s,'$,,; s,^.*',," | ~/little-things/uniqify > tracks-17to20-unique
comm -13 <(sort tracks-1to16-unique) <(sort tracks-17to20-unique) >tracks-17to20-unique-deduped-sorted


Split for set #2 accomplished by:
zcat tracks-17to20-unique-deduped-sorted.gz | grep \.cloudfront\.net/       | split -l50 -a4 - list2-cf-
zcat tracks-17to20-unique-deduped-sorted.gz | grep \.s3\.amazonaws\.com/    | split -l50 -a4 - list2-aws-
zcat tracks-17to20-unique-deduped-sorted.gz | grep \.official\.fm/          | split -l50 -a4 - list2-ofm-
zcat tracks-17to20-unique-deduped-sorted.gz | grep \.freemusicarchive\.org/ | split -l50 -a4 - list2-fma-
zcat tracks-17to20-unique-deduped-sorted.gz | grep \.feature\.fm/           | split -l50 -a4 - list2-ffm-

