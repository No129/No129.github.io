
除了使用 CustomControl 組件的專案之外，
啟動系統的專案也「必須」參照 CustomControl 組件，
不然就會擲出找不到組件的訊息。

[可以看這篇文章，重點在樓主的自答部分：「... I needed to add the WindowTemplates Assembly in my Login Assembly since my Login Assembly is 'Main' (my starup Project) Assembly ...」](https://stackoverflow.com/questions/26366546/error-xamlparseexception-adding-a-reference-from-my-wpf-custom-control-library-t)