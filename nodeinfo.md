---
tags: dontlink
---

# اطلاعات گره(NodeInfo)

tutya-opennet از اعلان(advertising) مقدار کمی اطلاعات به‌صورت عمومی برای شبکه(network) پشتیبانی می‌کند. کل بند(stanza) نباید از 16KB بیشتر شود. نباید هیچ اطلاعاتی را منتشر کنید که نمی‌خواهید توسط خزنده‌های شبکه(network crawlers) جمع‌آوری شود یا آن را خصوصی(private) می‌دانید. NodeInfo می‌تواند هر قالبی داشته باشد، هرچند این سند برخی انواع رایج(common types) را برای هم‌کنش‌پذیری(interoperability) توضیح می‌دهد — لطفاً تا حد امکان به این قالب‌ها پایبند باشید.

اگر فایل پیکربندی(configuration file) شما در قالب HJSON باشد (که استاندارد است)، باید NodeInfo خود را در قالب HJSON مشخص کنید و tutya-opennet هنگام درخواست به‌طور خودکار آن را به JSON تبدیل می‌کند. اگر فایل پیکربندی شما در قالب JSON است، باید NodeInfo را نیز در قالب JSON مشخص کنید.

نمونه‌های زیر همگی در قالب HJSON هستند.

## انواع شناخته‌شده(Well-known types)

#### برچسب‌های بیلد گره(Node build tags)

این گزینه‌ها به‌صورت خودکار در NodeInfo پر می‌شوند، بنابراین لازم نیست آن‌ها را پیکربندی کنید. می‌توانید با تنظیم گزینه پیکربندی `NodeInfoPrivacy` روی `true` یا با تنظیم مقادیر زیر روی `null` آن‌ها را به‌اشتراک‌گذاری‌نشده(unshared) کنید.

```
NodeInfo:
{
	buildname: yggdrasil
	buildversion: 0.3.3
	buildplatform: darwin
	buildarch: amd64
}
```

#### نام گره(Node name)

یک نام دوستانه(friendly name) برای گره که ممکن است روی نقشه‌ها(maps) یا در کلاینت‌های GUI نمایش داده شود. این نام اغلب در قالب نام دامنه کامل(fully-qualified domain name (FQDN)) مشخص می‌شود، هرچند این ضروری نیست و می‌توان به‌جای آن از متن آزاد(free-flowing text) استفاده کرد.

```
NodeInfo:
{
	name: some-name.net
}
```

#### جزئیات همتاسازی عمومی(Public peering details)

اگر می‌خواهید گره خود را به‌عنوان یک گره عمومی(public node) اعلان کنید، می‌توانید اطلاعاتی درباره اینکه دیگر کاربران چگونه می‌توانند از طریق شبکه‌های دیگر با آن همتا شوند فراهم کنید.
yggdrasil
سطح اول کلید `\"public\"` باید کلاس شبکه(network class) را شامل شود، و سپس هر کلاس شبکه باید فهرستی از رشته‌های اتصال(connection strings) در قالب پیکربندی tutya-opennet باشد.

```
NodeInfo:
{
	public:
	{
		internet: [
			tcp://a.b.c.d:e
			tcp://[a:b:c::d]:e
		]
		tor: [
			socks://localhost:a/b.c.d.e:f
		]
	}
}
```

کلاس‌های شناخته‌شده فعلی عبارت‌اند از `\"internet\"`، `\"tor\"`، `\"i2p\"` و `\"cjdns\"`.
