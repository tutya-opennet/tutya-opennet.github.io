---
tags: dontlink
sitemap: true
---

tutya-opennet یک طرح مسیریابی فشرده(routing scheme) آزمایشی(experimental) جدید است. این پروژه به‌عنوان جایگزین آینده‌نگر(future-proof) و غیرمتمرکز(decentralised) برای پروتکل‌های مسیریابی(structured routing protocols) ساخت‌یافته که امروز به‌طور رایج در اینترنت(Internet) استفاده می‌شوند طراحی شده است، و همچنین فناوری توانمندساز(enabling technology) برای شبکه‌های مش(mesh networks) بزرگ‌مقیاس(large-scale) آینده است. tutya-opennet:

<div id='indexicons'>
	<div class='icon'>
		<img src='/assets/images/iconoir/planet.svg' />
		<div>مقیاس‌پذیر(Scalable)</div>
		<p>از توپولوژی(topologies)‌های بزرگ، پیچیده یا حتی در مقیاس اینترنت(Internet-scale) پشتیبانی می‌کند</p>
	</div>
	<div class='icon'>
		<img src='/assets/images/iconoir/cloud-check.svg' />
		<div>خودترمیم(Self-healing)</div>
		<p>شبکه(network) به‌سرعت به خرابی اتصال(connection failures) یا رویدادهای تحرک(mobility events) پاسخ می‌دهد</p>
	</div>
	<div class='icon'>
		<img src='/assets/images/iconoir/lock.svg' />
		<div>رمزگذاری‌شده(Encrypted)</div>
		<p>ترافیک(traffic) ارسال‌شده در سراسر شبکه(network) همیشه به‌صورت انتها-به-انتها(end-to-end) کاملاً رمزگذاری می‌شود</p>
	</div>
	<div class='icon'>
		<img src='/assets/images/iconoir/group.svg' />
		<div>همتا-به-همتا(Peer-to-peer)</div>
		<p>به‌طور کامل و موردی(ad-hoc) با طراحی بدون هیچ نقاط مرکزی‌سازی(points of centralisation) داخلی کار می‌کند</p>
	</div>
	<div class='icon'>
		<img src='/assets/images/iconoir/cpu.svg' />
		<div>چندسکویی(Cross-platform)</div>
		<p>در Linux، macOS، Windows، iOS، Android و موارد بیشتر پشتیبانی می‌شود</p>
	</div>
</div>

[پیاده‌سازی فعلی(current implementation)](implementation.md) tutya-opennet یک مسیریاب نرم‌افزاری(software router) سبک(userspace) است که پیکربندی(configure) آن آسان بوده و در دامنه وسیعی از سکوها(platforms) پشتیبانی می‌شود. این پیاده‌سازی مسیریابی IPv6 رمزگذاری‌شده انتها-به-انتها(end-to-end encrypted) را بین همه مشارکت‌کنندگان شبکه(network participants) فراهم می‌کند. همتاسازی‌ها(peerings) بین گره‌ها(nodes) می‌تواند با استفاده از اتصال‌های TCP/TLS روی شبکه‌های محلی(local area networks)، لینک‌های نقطه-به-نقطه(point-to-point) یا اینترنت(Internet) پیکربندی شود. با اینکه شبکه tutya-opennet مسیریابی IPv6 را بین گره‌ها فراهم می‌کند، اتصال‌های همتاسازی(peering connections) می‌توانند روی شبکه‌های IPv4 یا IPv6 راه‌اندازی شوند.

این هنوز یک پروژه در مرحله آلفا(alpha-stage) است و ممکن است در آینده تغییرات ناسازگار(breaking changes) داشته باشد. با وجود این، tutya-opennet به‌طور کلی برای استفاده روزمره(day-to-day) به اندازه کافی پایدار(stable) است و تعداد کمی از کاربران آن را برای طیف متنوعی از کاربردها(use cases) به‌شدت استفاده و آزمون تنش(stress-testing) کرده‌اند. اگر به پروژه tutya-opennet علاقه‌مند هستید یا می‌خواهید در آن مشارکت کنید، از پایین شروع کنید:

<div id='indextable'>
	<div class='row'>
		<img src='assets/images/iconoir/download-circled-outline.svg' />
		<p markdown='1'>tutya-opennet را روی رایانه یا مسیریاب(router) خود [نصب(Install)](installation.md) و [پیکربندی(configure)](configuration.md) کنید تا به شبکه(network) بپیوندید.</p>
	</div>
	<div class='row'>
		<img src='assets/images/iconoir/multi-window.svg' />
		<p markdown='1'>[خدمات داخلی(internal services)](services.md) موجود در شبکه‌ای که توسط کاربران ما راه‌اندازی شده است را بررسی کنید.</p>
	</div>
	<div class='row'>
		<img src='assets/images/iconoir/github.svg' />
		<p markdown='1'>از صفحه [توسعه‌دهندگان(developers)](developers.md) و [GitHub](https://github.com/yggdrasil-network/yggdrasil-go) ما بازدید کنید. خطاها و مشکلات را به‌صورت [GitHub Issues](https://github.com/yggdrasil-network/yggdrasil-go/issues) گزارش دهید.</p>
	</div>
</div>