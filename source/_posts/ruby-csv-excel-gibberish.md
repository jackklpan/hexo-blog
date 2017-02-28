---
title: ruby csv excel gibberish
tags:
  - ruby
date: 2015-12-15 09:05:00
---

From:
http://blog.poyi.tw/blog/2014/05/06/ruby-csv-file/

export_to_csv_string 匯出csv的string格式再利用send_data下載
&nbsp; head = 'EF BB BF'.split(' ').map{|a|a.hex.chr}.join() # 加入BOM，解決excel中文亂碼

&nbsp; csv_string = CSV.generate(csv = head) do |csv|
&nbsp; &nbsp; csv &lt;&lt; header
&nbsp; &nbsp; csv &lt;&lt; body
&nbsp; end

&nbsp; # &gt; csv_string.encoding 執行這句會發現預設編碼為ACSII
&nbsp; csv_string.force_encoding('big5')
&nbsp; # BOM也可以這樣加 csv_string = "\xEF\xBB\xBF#{csv_string}" 
&nbsp; # 若不需要調整格式就直接下載
&nbsp; send_data csv_string

convert_to_wide_word 大小寫英文數字轉全形字元
def self.convert_to_wide_word(text)
&nbsp; text.gsub(/[a-v]/){|a|(a.ord + 41608).chr('big5').encode('utf-8')}
&nbsp; &nbsp; .gsub(/[w-z]/){|a|(a.ord + 41673).chr('big5').encode('utf-8')}
&nbsp; &nbsp; .gsub(/[A-Z]/){|a|(a.ord + 41614).chr('big5').encode('utf-8')}
&nbsp; &nbsp; .gsub(/[0-9]/){|a|(a.ord + 41599).chr('big5').encode('utf-8')}
end

convert_to_wide_word("0123456789abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ")
&nbsp;=&gt; "０１２３４５６７８９ａｂｃｄｅｆｇｈｉｊｋｌｍｎｏｐｑｒｓｔｕｖｗｘｙｚＡＢＣＤＥＦＧＨＩＪＫＬ
&nbsp;ＭＮＯＰＱＲＳＴＵＶＷＸＹＺ"