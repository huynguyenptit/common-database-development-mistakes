**9. Thiếu chuẩn hoá**

[Chuẩn hoá cơ sở dữ liệu](http://en.wikipedia.org/wiki/Database_normalization) về cơ bản thì đây là quá trình tối ưu hoá việc thiết kế cơ sở dữ liệu hoặc tổ chức các dữ liệu của bạn vào các bảng.

Chỉ trong tuần vừa rồi tôi gặp 1 đoạn code mà họ tách nó ra thành 1 mảng và thêm chúng vào như 1 trường trong cơ sở dữ liệu. Quá trình chuẩn hoá là xử lý từng phần tử của mảng đó như 1 dòng riêng biệt trong bảng 
con (tương đương 1 mối quan hệ 1 nhiều).

Điều này cũng được nhắc tới tại [Phương thức tốt nhất để lưu 1 danh sách các ID của người dùng](https://stackoverflow.com/questions/620645/best-method-for-storing-a-list-of-user-ids):

> Tôi cũng đã từng thấy 1 hệ thống khác lưu trữ danh sách trong 1 mảng tuần tự của PHP.

Tuy nhiên vấn đề thiếu chuẩn hoá vẫn còn nhiều dạng.

Xem thêm:

- [Chuẩn hoá: bao nhiêu là đủ?](http://www.techrepublic.com/article/normalization-how-far-is-far-enough/)
- [SQL by Design: Tại sao bạn cần chuẩn hoá cơ sở dữ liệu ](http://www.sqlmag.com/Article/ArticleID/4887/sql_server_4887.html)

**10. Chuẩn hoá quá nhiều**

Nhìn chung vấn đề này trái ngước với vấn đề trước nhưng việc chuẩn hoá cũng như là những việc khác, nó được xem là một công cụ. Nó không có điểm kết thúc cụ thể nào cả. Tôi nghĩ là rất nhiều những lập trình viên quên mất điều này, bắt đầu hiểu sai 1 "công cụ" thành 1 thứ có thể "kết thúc" vấn đề. Unit testing là một ví dụ điển hình về điều này.

Lúc tôi làm việc trên 1 hệ thống có hệ thống phân cấp cho người dùng cực lớn, tôi đã gặp 1 vài điều như này:

Licensee -&gt;  Dealer Group -&gt; Company -&gt; Practice -&gt; ...

giống như kiểu bạn phải join khoảng 11 bảng khác nhau trước khi bạn muốn lấy bất kỳ dữ liệu gì. Nó là 1 ví dụ rất tốt cho việc chuẩn hoá quá nhiều.

Một điều nữa, hãy cẩn thận và xem xét việc tối ưu chuẩn hoá có thể mang lại những lợi ích đáng kể nhưng bạn cũng phải cẩn thận khi làm điều này.

Xem thêm:

- [Vì sao chuẩn hoá cơ sở dữ liệu quá nhiều cũng không tốt](http://www.selikoff.net/blog/2008/11/19/why-too-much-database-normalization-can-be-a-bad-thing/)
- [Thiết kế cơ sở dữ liệu tới mức nào là đủ chuẩn?](https://stackoverflow.com/questions/496508/how-far-to-take-normalization-in-database-design)
- [Khi nào bạn không cần chuẩn hoá cơ sở dữ liệu](http://www.25hoursaday.com/weblog/CommentView.aspx?guid=cc0e740c-a828-4b9d-b244-4ee96e2fad4b)
- [Chuẩn hoá có thể không chuẩn](http://www.codinghorror.com/blog/archives/001152.html)
- [Nguyên nhân các cuộc tranh luận về chuẩn hoá trên Coding Horror](http://highscalability.com/mother-all-database-normalization-debates-coding-horror)


**11. Sử dụng các exclusive arcs ( truy vấn lòng vòng )**

Việc truy vấn lòng vòng là 1 trong những lỗi thường gặp khi 1 bảng được tạo ra với 2 hay nhiều khoá ngoại và 1 trong số đó lại có thể không null.  **Lỗi lớn đấy.** Đây là điều khiến nó trở lên khó khăn hơn nhiều trong việc duy trì tính toàn vẹn dữ liệu. Sau tất cả, ngay cả khi sử dụng các ràng buộc tham chiếu vẫn không có gì ngăn được việc đặt 2 hay nhiều hơn các khoá ngoại (mặc dù đã kiểm tra các ràng buộc phức tạp).

từ bài viết [Hướng dẫn thực hành thiết kế cơ sở dữ liệu quan hệ](http://books.google.com.au/books?id=7ZAk0YiKQV0C&pg=PA110&lpg=PA110&dq=%22exclusive+arc%22+database&source=bl&ots=AyNPWsac__&sig=gBFIerXckQlVpRdd6ycI5JEgq3U&hl=en&ei=PzGzSZfrFcPVkAWWyZDZBA&sa=X&oi=book_result&resnum=1&ct=result):

  > Chúng tôi không khuyến khích xây dựng các câu truy vấn phức tạp bất cứ khi nào có thể, vì 1 lý do rằng nó có thể rất lộn xộn khi viết code và khiến việc bảo trì khó khăn.

**12. Không phân tích hiệu suất các lệnh truy vấn**

Theo chủ nghĩa thực dụng, đặc biệt là trong môi trường cơ sở dữ liệu. Nếu bạn vẫn đang cố giữ nguyên tắc đến mức chúng trở thành một giáo điều thì bạn thực sự đang mắc sai lầm đấy. Lấy 1 ví dụ về các truy vấn sử dụng GROUP bên trên. Phiên bản sử dụng GROUP có vẻ nhìn "ổn" nhưng hiệu suất của nó thì tệ. Việc tranh luận về so sánh về hiệu suất nên kết thúc(nhưng nó không) nhưng nhớ thêm 1 điều rằng : việc sử dụng quá nhiều view thông báo xấu ngay trong vị trí đầu tiên là không ổn, thậm chí nó còn nguy hiểm.


**13. Quá phụ thuộc vào UNION ALL và đặc biệt là cấu trúc UNION**

Một UNION trong SQL chỉ đơn thuần nối các tập dữ liệu đồng nhất, có nghĩa là chúng phải có cùng kiểu và số cột. Sự khác biệt giữa chúng là UNION ALL là một sự ghép nối đơn giản và nên được ưu tiên hơn bất cứ khi nào có thể, trong khi một UNION ngầm sẽ sử dụng một DISTINCT để loại bỏ các bản sao trùng lặp.

Các UNION, như DISTINCT, có chỗ của chúng. Có các ứng dụng hợp lệ. Nhưng nếu bạn thấy mình đang sử dụng chúng rất nhiều, đặc biệt trong các truy vấn phụ, thì có thể bạn đang làm sai gì đó. Đó có thể là trường hợp xây dựng truy vấn kém hoặc mô hình dữ liệu được thiết kế kém buộc bạn phải làm những việc như vậy.

UNION, đặc biệt khi sử dụng trong các kết nối hoặc các truy vấn phụ phụ thuộc, có thể làm tê liệt cơ sở dữ liệu. Cố gắng tránh sử dụng chúng bất cứ khi nào có thể.

**14. sử dụng các điều kiện or trong câu truy vấn**

Cái này có vẻ vô hại. Và sau tất cả, ANDs cũng OK. Vậy mệnh đề OR liệu có thực sự tốt? Sai rồi. Thông thường điều kiện AND sẽ **hạn chế** tập dữ liệu trong khi điều kiện OR **làm tăng** tập dữ liệu nhưng không phải theo cách khiến chúng được tối ưu. Đặc biệt là khi các điều kiện OR khác nhau có thể giao nhau khiến cho việc tối ưu hóa hiệu quả hơn với các phép DISTINCT.

Bad:

... WHERE a = 2 OR a = 5 OR a = 11

Better:

... WHERE a IN (2, 5, 11)

Bây giờ việc tối ưu lênh SQL của bạn có thể hiệu quả từ câu truy vấn đầu tiên tới câu thứ 2. Nhưng cũng có thể không. Đừng làm như thế.

**15. Không thiết kế các mô hình dữ liệu để vay mượn các giải pháp hiệu suất cao**

Đây là 1 điểm khó đánh giá. Nó thường được đánh giá thông qua hiệu quả cửa nó. Nếu bạn thấy mình đang viết các lệnh truy vấn cho các việc đơn giản hoặc các truy vấn chỉ để tìm kiếm các thông tin tương đối đơn giản nhưng lại không có hiệu quả, bạn chắc chắn đang sử dụng một mô hình dữ liệu tệ ( mô hình dữ liệu có hiệu suất kém).

Bằng 1 cách nào đó điều này bao gồm cả các điều trước đó nhưng nó lại có thêm 1 cảnh báo là các câu truy vấn đên được tối ưu đầu tiên trong khi nó chỉ nên hoàn thành thứ 2. Đầu tiên và cũng là quan trọng nhất, bạn nên chắc chắn mô hình dữ liệu của bạn tốt trước khi cố gắng tối ưu hiệu suất. Giống như Knuth đã nói:

> Tối ưu hóa sớm là nguồn cơ của mọi rắc rối.

**16. Sử dụng Database Transactions sai**

Tất cả các sự kiện thay đổi dữ liệu trong 1 tiến trình nên tuân thủ mô hình nguyên tử (atomic). Ví dụ nếu các hành động thực hiện thành công, nó sẽ cập nhật đầy đủ. Nếu nó không thành công, dữ liệu sẽ không thay đổi. Không để các thay đổi kiểu "hoàn thành 1 nửa".

Lý tưởng nhất, cách tốt nhất để đạt được điều này là thiết kế toàn bộ hệ thống nên cố gắng hỗ trợ toàn bộ thay đổi dữ liệu qua từng câu lệnh INSERT/UPDATE/DELETE. Trong trường hợp này, không có xử lý transaction đặc biệt nào cần thiết cả, vì engine cơ sở dữ liệu của bạn nên làm điều này tự động.

tuy nhiên, nếu bất kì tiến trình nào yêu cầu nhiều câu lệnh thực hiện như là 1 đơn vị lưu trữ dữ liệu trong trạng thái thích hợp, khi đó việc quản lý các giao tác (Transition Control) là cần thiết.

- Bắt đầu một giao dịch trước câu lệnh đầu tiên.
- Commit giao dịch sau câu lệnh cuối cùng.
- Trong bất kì hoàn cảnh nào, hãy phục hồi giao dịch. Đừng quên skip/abort tất cả câu lệnh theo lỗi đó.

 *And very NB = And very Note Bene = And very Note Well*
 
Also recommended to pay careful attention to the subtelties of how your database connectivity layer, and database engine interact in this regard. 
Gợi ý khác nữa là hãy chú ý tới các dịch vụ phụ khác trong việc kết nối các lớp và engine tương tác của cơ sở dữ liệu trong vấn đề này.

**17. Không hiểu mô hình 'set-based'**

  Ngôn ngữ SQL tuân theo mô hình cụ thể phù hợp với các loại vấn đề cụ thể. Mặc dù cung cấp nhiều phần mở rộng cụ thể, việc xung đột ngôn ngữ đẻ giải quyết vấn đề này là không đáng kể trong các ngôn ngữ như Java, C#, Delphi,...

Sự thiếu hiểu biết này thể hiện theo một vài cách.

- Áp dụng quá nhiều thủ tục hay bắt buộc logic trong CSDL
- Việc sử dụng không phù hợp hoặc quá mức của các con trỏ. Đặc biệt là khi một câu truy vấn đơn nhất là đủ.
-Giả định không đúng kích hoạt một lần mỗi hàng bị ảnh hưởng trong cập nhật nhiều hàng.

Để xác định phân chia các trách nhiệm rõ ràng, và cố gắng sử dụng các công cụ thích hợp để giải quyết từng vấn đề.