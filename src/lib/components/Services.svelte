<script lang="ts">
	const services = [
		{
			icon: `<path d="M19 21V5a2 2 0 00-2-2H7a2 2 0 00-2 2v16m14 0h2m-2 0h-5m-9 0H3m2 0h5M9 7h1m-1 4h1m4-4h1m-1 4h1m-5 10v-5a1 1 0 011-1h2a1 1 0 011 1v5m-4 0h4"/>`,
			title: 'Kasko Sigortası',
			desc: 'Aracınızı her türlü riske karşı kapsamlı koruma altına alın.'
		},
		{
			icon: `<path d="M9 17a2 2 0 11-4 0 2 2 0 014 0zM19 17a2 2 0 11-4 0 2 2 0 014 0z"/><path d="M13 16V6a1 1 0 00-1-1H4a1 1 0 00-1 1v10"/><path d="M13 6h5l3 5v5h-2M3 16h1m5 0h4"/>`,
			title: 'Trafik Sigortası',
			desc: 'Zorunlu trafik sigortanızı en uygun fiyatla yaptırın.'
		},
		{
			icon: `<path d="M4.318 6.318a4.5 4.5 0 000 6.364L12 20.364l7.682-7.682a4.5 4.5 0 00-6.364-6.364L12 7.636l-1.318-1.318a4.5 4.5 0 00-6.364 0z"/>`,
			title: 'Sağlık Sigortası',
			desc: 'Siz ve aileniz için özel sağlık güvencesi planları.'
		},
		{
			icon: `<path d="M3 12l2-2m0 0l7-7 7 7M5 10v10a1 1 0 001 1h3m10-11l2 2m-2-2v10a1 1 0 01-1 1h-3m-6 0a1 1 0 001-1v-4a1 1 0 011-1h2a1 1 0 011 1v4a1 1 0 001 1m-6 0h6"/>`,
			title: 'Konut Sigortası',
			desc: 'Evinizi ve eşyalarınızı doğal afet ve hırsızlığa karşı koruyun.'
		},
		{
			icon: `<path d="M19 21l-7-5-7 5V5a2 2 0 012-2h10a2 2 0 012 2z"/>`,
			title: 'DASK',
			desc: 'Zorunlu deprem sigortanızı hızlı ve kolay şekilde yaptırın.'
		},
		{
			icon: `<path d="M3.055 11H5a2 2 0 012 2v1a2 2 0 002 2 2 2 0 012 2v2.945M8 3.935V5.5A2.5 2.5 0 0010.5 8h.5a2 2 0 012 2 2 2 0 104 0 2 2 0 012-2h1.064M15 20.488V18a2 2 0 012-2h3.064"/><circle cx="12" cy="12" r="10"/>`,
			title: 'Seyahat Sigortası',
			desc: 'Yurt içi ve yurt dışı seyahatlerinizde güvende olun.'
		},
		{
			icon: `<path d="M12 4.354a4 4 0 110 5.292M15 21H3v-1a6 6 0 0112 0v1zm0 0h6v-1a6 6 0 00-9-5.197M13 7a4 4 0 11-8 0 4 4 0 018 0z"/>`,
			title: 'Hayat Sigortası',
			desc: 'Sevdiklerinizin geleceğini garanti altına alın.'
		},
		{
			icon: `<path d="M21 13.255A23.931 23.931 0 0112 15c-3.183 0-6.22-.62-9-1.745M16 6V4a2 2 0 00-2-2h-4a2 2 0 00-2 2v2m4 6h.01M5 20h14a2 2 0 002-2V8a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z"/>`,
			title: 'Kurumsal Sigorta',
			desc: 'İşletmeniz için özel kurumsal sigorta çözümleri.'
		}
	];
</script>

<section id="sigortalar" class="py-20 lg:py-28 bg-teal-50">
	<div class="max-w-7xl mx-auto px-6">
		<!-- Section header -->
		<div class="text-center mb-16" data-aos="fade-up">
			<span class="inline-block text-sm font-semibold text-teal-700 bg-teal-100 px-4 py-1.5 rounded-full mb-4">SİGORTALARIMIZ</span>
			<h2 class="font-heading font-bold text-3xl sm:text-4xl lg:text-[40px] text-charcoal-800 mb-4">
				İhtiyacınıza Uygun Sigorta Çözümleri
			</h2>
			<p class="text-charcoal-500 max-w-2xl mx-auto text-lg">
				Geniş ürün yelpazemizle kişisel ve kurumsal tüm ihtiyaçlarınıza en uygun sigorta paketlerini sunuyoruz.
			</p>
		</div>

		<!-- Grid -->
		<div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-6">
			{#each services as service, i}
				<div
					class="group bg-white rounded-2xl p-6 card-hover cursor-pointer"
					data-aos="fade-up"
					data-aos-delay={i * 100}
				>
					<!-- Icon -->
					<div class="w-14 h-14 bg-teal-50 group-hover:bg-gold-500/10 rounded-2xl flex items-center justify-center mb-5 transition-colors">
						<svg class="w-7 h-7 text-teal-700 group-hover:text-gold-500 transition-colors" fill="none" stroke="currentColor" viewBox="0 0 24 24" stroke-width="1.5">
							{@html service.icon}
						</svg>
					</div>

					<h3 class="font-heading font-semibold text-lg text-charcoal-800 mb-2">{service.title}</h3>
					<p class="text-charcoal-500 text-sm leading-relaxed mb-4">{service.desc}</p>

					<span class="inline-flex items-center gap-1 text-sm font-medium text-teal-700 group-hover:text-gold-500 transition-colors">
						Detaylı Bilgi
						<svg class="w-4 h-4 transition-transform group-hover:translate-x-1" fill="none" stroke="currentColor" viewBox="0 0 24 24" stroke-width="2"><path d="M17 8l4 4m0 0l-4 4m4-4H3"/></svg>
					</span>
				</div>
			{/each}
		</div>
	</div>
</section>
