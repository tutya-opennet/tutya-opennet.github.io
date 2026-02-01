---
tags: dontlink
sitemap: true
---

# API ادمین(Admin API)

سوکت ادمین(admin socket) یک رابط(interface) برای پرس‌وجو(query) و پیکربندی(configure) tutya-opennet در زمان اجرا(runtime) فراهم می‌کند. به‌طور پیش‌فرض، tutya-opennet برای اتصال‌های ادمین(admin connections) روی `localhost:9001` گوش می‌دهد.

## ابزار کنترل(Control Utility)

ابزار `yggdrasilctl` یک رابط CLI کاربرپسند(human-friendly CLI interface) برای سوکت ادمین(admin socket) tutya-opennet فراهم می‌کند. این ابزار می‌تواند به نمونه‌های(instances) محلی و راه‌دور(remote) tutya-opennet متصل شود و همان فعل‌ها(verbs)ی پایین را می‌پذیرد. هر فیلد(field) با قالب `field=value` مشخص می‌شود.

نمونه‌ها شامل موارد زیر است:
```
yggdrasilctl getDHT
yggdrasilctl getPeers
````

برای گرفتن فهرست فرمان‌های پشتیبانی‌شده:
```
yggdrasilctl list
```

برای انجام یک عمل(action) روی یک گره(node) راه‌دور tutya-opennet، پارامتر `-endpoint` را مشخص کنید:
```
yggdrasilctl -endpoint=tcp://10.0.0.1:9001 getPeers
yggdrasilctl -endpoint=unix:///var/run/yggdrasil.sock getDHT
```

برای گرفتن بدنه پاسخ JSON به‌جای خروجی «دوستانه(friendly)»، پارامتر `-json` را مشخص کنید:
```
yggdrasilctl -json getPeers
```

## سوکت ادمین(Admin Socket)

سوکت ادمین(admin socket) tutya-opennet برای قالب‌های درخواست و پاسخ از JSON استفاده می‌کند.

یک درخواست باید:
- یک بند JSON کامل(complete JSON stanza) باشد
- و با کاراکتر خط‌جدید(newline) `\n` دنبال شود

پس از دریافت یک درخواست معتبر(valid request)، بند پاسخ(response stanza) بازگردانده می‌شود.

### درخواست(Request)

ساختار یک درخواست نمونه به‌صورت زیر است:
```
{
	"request": "XXX",
	"foo": "bar",
	"baz": "qux"
}
```

یک درخواست:
- *باید* یک فیلد `\"request\"` (`string`) داشته باشد - مقداری که فعل(verb) درخواست را در خود دارد
- *می‌تواند* یک فیلد `\"keepalive\"` (`bool`) داشته باشد - مقدار `true` یا `false` که می‌گوید آیا اتصال برای درخواست‌های بیشتر زنده نگه‌داشته شود یا نه (اگر مشخص نشود، tutya-opennet پس از بازگرداندن پاسخ اتصال ادمین(admin connection) را می‌بندد)
- *باید* هر فیلد موردنیاز دیگری برای درخواست داشته باشد
- *می‌تواند* هر فیلد اختیاری دیگری برای درخواست داشته باشد

### پاسخ(Response)

یک پاسخ نمونه به این شکل ساختاربندی می‌شود:
```
{
	"request":
	{
		"request": "XXX",
		"foo": "bar",
		"baz": "qux"
	},

	"response":
	{
	},

	"status": "success"
}
```

یک پاسخ:
- *همیشه* یک فیلد `\"request\"` (`string`) دارد که بدنه درخواست اصلی را در خود دارد
- *همیشه* یک فیلد `\"status\"` (`string`) دارد که یا `\"success\"` است یا `\"error\"`
- *اختیاری* می‌تواند یک بخش `\"response\"` داشته باشد که داده پاسخ درخواست را شامل می‌شود
- *اختیاری* می‌تواند یک فیلد `\"error\"` (`string`) داشته باشد که متن خطا(error text) را شامل می‌شود

### انواع درخواست(Request Types)

فیلد `\"request\"` یک فعل(verb) دارد که توضیح می‌دهد کدام درخواست اجرا شود.

#### `getDHT`

نیاز به فیلدهای اضافی درخواست ندارد.

گره‌های شناخته‌شده در DHT را برمی‌گرداند.
- `key` (`string`) شامل `PublicKey` گره راه‌دور است
- `port` (`int`)
- `rest` (`int`)

#### `getPeers`

نیاز به فیلدهای اضافی درخواست ندارد.

یک یا چند رکورد(record) شامل اطلاعات درباره نشست‌های همتا(peer sessions) فعال برمی‌گرداند. اولین رکورد معمولاً به گره فعلی اشاره دارد.

برای هر آدرس IPv6:
- `key` (`string`) شامل `PublicKey` گره راه‌دور است
- `port` (`uint8`) شامل شماره درگاه سوییچ محلی(local switch port) برای آن همتا است
- `coords` (`[]int`) شامل مختصات گره روی درخت گسترده(spanning tree) است
- `remote` (`string`) شامل URI همتاسازی(peering URI) همتای راه‌دور است

#### `getSelf`

نیاز به فیلدهای اضافی درخواست ندارد.

دقیقاً یک رکورد شامل اطلاعات درباره گره tutya-opennet فعلی برمی‌گرداند.

برای آدرس IPv6 فعلی:
- `key` (`string`) شامل `EncryptionPublicKey` گره فعلی است
- `build_name` (`string`) شامل نام بیلد(build name) است، اگر موجود باشد (مثلاً `yggdrasil`، `yggdrasil-develop`)
- `build_version` (`string`) شامل نسخه بیلد(build version) است، اگر موجود باشد (مثلاً `0.3.0`، `0.2.7-0091`)
- `coords` (`[]int`) شامل مختصات گره روی درخت گسترده(spanning tree) است
- `subnet` (`string`) شامل زیرشبکه IPv6 مسیریابی‌شده(routed IPv6 subnet) برای این میزبان(host) است

#### `getSessions`

نیاز به فیلدهای اضافی درخواست ندارد.

صفر یا چند رکورد شامل اطلاعات درباره نشست‌های باز(open sessions) بین گره tutya-opennet فعلی و گره‌های دیگر برمی‌گرداند. نشست‌های باز نشان می‌دهد که اخیراً با گره راه‌دور ترافیک رد و بدل شده است.

برای هر آدرس IPv6:
- `key` (`string`) شامل `EncryptionPublicKey` گره راه‌دور است

#### `getTunTap`

نیاز به فیلدهای اضافی درخواست ندارد.

دقیقاً یک رکورد شامل اطلاعات درباره آداپتور(adapter) TUN/TAP گره فعلی برمی‌گرداند.

برای هر آداپتور:
- `mtu` (`uint8`) شامل MTU آداپتور TUN/TAP محلی است

#### `getMulticastInterfaces`

نیاز به فیلدهای اضافی درخواست ندارد.

صفر یا چند رشته(string) شامل رابط‌های همتاسازی چندپخشی(multicast peering interfaces) فعال را برمی‌گرداند.

اگر هیچ رشته‌ای بازگردانده نشود، یعنی همتاسازی چندپخشی(multicast peering) روی هیچ رابطی مجاز نیست.

#### `getNodeInfo`

انتظار دارد:
- `key=` `string`، کلید عمومی(public key) هگز(hex-encoded) گره راه‌دوری که باید پینگ(ping) شود، با همان قالبی که مثلاً در خروجی پرجزئیات(verbose output) از پاسخ `getDHT` دیده می‌شود

از یک گره راه‌دور می‌خواهد که با nodeinfo خود پاسخ دهد.

یک بخش `nodeinfo` با nodeinfo برمی‌گرداند. این می‌تواند در هر قالبی باشد و هر کلیدی داشته باشد.