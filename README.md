
# ایجاد و تست Certificate Authority و TLS با استفاده از Wireshark

این راهنما شرح مراحل ایجاد یک Certificate Authority (CA) و صدور گواهینامه TLS برای سرور را فراهم می‌کند. این مراحل برای ایجاد و تست ارتباطات امن TLS با استفاده از ابزار Wireshark ارائه شده‌اند.

## 1. ایجاد یک Certificate Authority (CA)

- از ابزار OpenSSL برای ایجاد یک CA استفاده کنید.
- ایجاد کلید خصوصی و گواهینامه CA:
‏ 
‏  openssl genpkey -algorithm RSA -out rootCA.key
‏  openssl req -x509 -new -key rootCA.key -out rootCA.crt


## 2. صادر کردن گواهینامه برای سرور

- ایجاد یک کلید خصوصی و درخواست گواهینامه برای سرور:

‏  openssl genpkey -algorithm RSA -out server.key
‏  openssl req -new -key server.key -out server.csr

- امضای درخواست گواهینامه توسط CA:
‏  
‏  openssl x509 -req -in server.csr -CA rootCA.crt -CAkey rootCA.key -CAcreateserial -out server.crt -days 365


## 3. تنظیم و اعمال گواهینامه در سرور

- گواهینامه و کلید را در سرور خود نصب کنید.

## 4. انجام تست

- تنظیم مرورگر یا برنامه ای که ترافیک ارسال می‌کنید تا از گواهینامه شما استفاده کند.
- با استفاده از ابزارهایی مانند Wireshark یا tcpdump ترافیک را بررسی کنید و رمزنگاری شده را مشاهده کنید.

 مراحل زیر را دنبال کنید:

## 1. انتخاب رابط شبکه

- باز کنید Wireshark و از لیست رابط‌های شبکه موجود، رابط موردنظر خود را انتخاب کنید.

## 2. فیلتر کردن بر اساس IP

- اگر می‌خواهید ترافیک را بر اساس IP خاصی ببینید، از فیلترهایی مانند `ip.src==192.168.1.1` یا `ip.dst==192.168.1.1` استفاده کنید.

## 3. فیلتر کردن بر اساس پروتکل TLS

- اگر می‌خواهید ترافیک TLS را مشاهده کنید، از `tls` یا `ssl` به عنوان فیلتر استفاده کنید.

## 4. ضبط ترافیک

- روی دکمه "شروع ضبط" کلیک کنید تا Wireshark شروع به ضبط ترافیک کند.

## 5. اجرای ترافیک

- اجرای ترافیک برنامه یا اطلاعات مورد نظر خود را در شبکه.

## 6. تحلیل ترافیک

- پس از اجرا، مشاهده ت رافیک در قسمت های مختلف Wireshark امکان پذیر است.

از Wireshark می‌توانید اطلاعات بیشتری را در مورد ارتباطات شبکه، پروتکل‌ها، و امنیت ترافیک به دست آورید. توجه داشته باشید که استفاده از این اطلاعات باید با محدودیت‌ها و قوانین محلی مطابقت داشته باشد.
